# Deploy and configure Azure Database for MySQL

### you start.

Please use  PowerBI-VM to execute this lab.

Throughout this hands on lab there are many cli commands given. Some of these contain values that are listed with like this [vaule], in instances where this square bracket notation is used you must provide an apropriate value.

### Provision the Azure Resources ###

1. Create the Azure resources.
    
  Simply click the Deploy to Azure button below and follow the wizard to create the resources. You will need to log in to the Azure Portal, Use the lab azure credentials to login.
                                                                     
  [![Deploy to Azure](https://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FSpektraSystems%2FAzure-CosmosDB-and-Mysql-Postgres-Hands-on-Lab%2Fmaster%2Ftemplate%2Fmysql-resources.azuredeploy.json)

  Please select existing resource group for deployment.


### Scenarios ###

Azure Database for MySQL

Scenario 1: Provision Azure Database for MySQL

>Scenario 2: Deplopy website code

Scenario 3: Popluate MySQL with data

Scenario 4: Scale up

Conclusion


# Azure Database for MySQL

Azure Database for MySQL provides a fully managed database service for application development and deployment allowing you to provision a MySQL database instance in minutes and scale it on the fly.
With comprehensive pricing models, and configurable sizing, you get all the features you need such as high-availability, monitoring and security, and backup and recovery, all with reduced management overhead.  These features are built into the service and are aligned to a simple, predictable pricing model. 

# Provision MySQL Server 

## Create a database using Azure CLI

1. Open a PowerShell command prompt, you can find a shortcut on the taskbar, and run:

    <span style="color:blue">az login

1. When the prompt window instructs your to open [https://aka.ms/devicelogin](https://aka.ms/devicelogin) and enter the code shown in the console window  
    ![Device Login code](images/az-login-code.png)

1. Sign in with your Azure username and password

1. You now have an Azure CLI session open against the Azure Subscription hosting your lab

1. You will now use the CLI to provision an Azure Database for MySQL. In the open PowerShell  prompt, use the following command to provision an new Azure Database for MySQL:
    > Note: It would be best to provision this in the Resource Group created using the Azure Deploy tool.

     <span style="color:blue"> az mysql server create --resource-group [MyResourceGroupName] --name [mysqlDatabaseName] --location westus --admin-user mysqlAdminUser --admin-password mysqlAdminPassw0rd! --performance-tier Basic --compute-units 50 --ssl-enforcement Disabled

1. By default the database is completely locked down and cannot be accessed, so we need to add a firewall rule to allow us to connect to the database server. The rule we're creating here allows all traffic, in production scenarios the rule would be much more restricted.

   <span style="color:blue"> az mysql server firewall-rule create --resource-group [MyResourceGroupName] --server [mysqlDatabaseName]--name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255

1. Congratuations. You now have somewhere to store your data.


## Deploy the website

We now need to change some configuration code for the WordPress website so that it is able to consume data from the database which we have just provisioned. Once we have updated the code we'll deploy it to an Azure App Service which has already been provisioned.

1. First we need to acquire a copy of the code for the website. To do this we will clone it from an existing GitHub repository. In the open PowerShell command prompt run the following commands:

    <span style="color:blue"> cd \  
    <span style="color:blue"> mkdir code  
    <span style="color:blue"> cd code  
    <span style="color:blue"> git clone https://github.com/gavinbarron/bikeshop.git

1. Next we need to set some git configuration values so that we can push any changes which are made to remote repositories. To do this run the following commands in the command prompt:

    <span style="color:blue"> cd bikeshop  
    <span style="color:blue"> git config user.name "holuser"  
    <span style="color:blue"> git config user.email "me@me.net"  

1. Now we need to update the code to use the MySQL databse which was previously provisioned. To do this, Open Visual Studio Code

1. Using the file menu choose Open File
    ![Open File](images/vscode-open-file.png)

1. Open the `wp-config.php` file at `C:\code\bikeshop\`

1. On line 44 replace `[Username]` with **mysqlAdminUser@[mysqlDatabaseName]**, the value of the username for your database administrator account [previously provisioned](1.md)

1. On line 47 replace `[Password]` with **mysqlAdminPassw0rd!**, the value of the password for your database administrator account [previously provisioned](1.md)

1. On line 51 replace `[Servername]` with **[mysqlDatabaseName]**, the server name for your database [previously provisioned](1.md)
   ![wp_config changes](images/wp_config.png "wp config changes")

1. Save the changes

1. To deploy this code to the website that has been provisioned you will need to set up some deployment credentials for your user account. To do this, switch back to the open PowerShell prompt

1. Execute this command to set your deployment username and password:
    > Note that the username here needs to be globally unique for all of Azure, so you do need to choose your own values.

    <span style="color:blue"> az webapp deployment user set --user-name [myDeploymentUserName] --password [MyGitDeployPassw0rd!]

1. Next we need the URL for the git repository which is configured for the website which will host the WordPress code. Open [https://portal.azure.com](https://portal.azure.com)

1. Open the Resource Groups blade and then open the resource group available to you.

1. Verify that there are:
    - An Azure Database for MySQL
    - An Azure App Service
    - An App Service Plan
   ![ResourceGroup Items](images/resourcegroup_items.png "Resource Group Items")

1. Open the App Service blade

1. In on the overview section copy the **Git clone url**
   ![Git Clone URL](images/git_clone_url.png "GIT Clone URL")

1. Now we need to configure the local git repository to know about the website. To do this we will add a new remote to the repository:

    <span style="color:blue"> git remote add website [copiedGitUrl]

1. Commit your changes to the local git repository:

    <span style="color:blue"> git add .  
    <span style="color:blue"> git commit -m "Updating config to point at new Azure Database for MySQL"

1. Deploy your changes to the Azure App Service:

    <span style="color:blue"> git push website

1. In the pop-up enter the deployment credentials password that you set previously and click OK
    ![Git Credentials](images/git-credentials-pop-up.png)

1. Wait for the push to the website to complete

1. The website is now updated and just needs data


## Populate Data

Before our WordPress website will work we need to populate the database with data.  To do this, we are going to use The MySQL Workbench to connect to our ``Azure Database for MySQL`` that we already have up and running and use a script to restore data into the database.

1. Open MySQL Workbench  
    ![Open MySQL Workbench](images/open-mysql-workbench.png)

1. Click OK and ignore the unsupported operating system warning

1. Click on the + icon to add a new MySQL Connection  
    ![Add new connection](images/add-mysql-connection.png)

1. Setup the new connection to MySQL using the server name, username, and password [previously provisioned](1.ProvisionServer.md)

1. Click on "Store in Vault..." to enter password, then click OK  
   ![Workbench DB Connection](images/wb_db_connection.png "Workbench DB Connection")

1. Click on Test Connection to verify that you have configured the connection correctly. If you have issues check that you have provided the all of the details correctly. Once the test connection action succeeds click on OK

1. Double click on the connection name to open a session against your MySQL database  
   ![DB connection](images/wb_open_connection.png "DB connection")

1. Choose **File > Run SQL Script**  
    ![Run SQL Script](images/mysql-run-script.png)

1. Open the sql file from `C:\code\bikeshop\bikeshop.sql` and click the Run  
   ![Workbench run query](images/running_query_create_schema.png "Run Query in Workbench")

1. Once the script has been executed the database schema "bikestore" will have been created, click the Close button

1. Click the refresh icon to see it listed in the set of availble schema  
   ![Schema created](images/workbench_schema_created.png "DB Schema Created")

1. Return to Azure portal and in the App Service blade click on the URL for the website  
   ![Open website](images/appservices.png)

1. The website should be up and running  
   ![Running website](images/running_website.png "Running website")
   
   ## Scale Up Azure Database for MySQL

Microsoft Azure offers a variety of pricing tiers for the Azure Database for MySQL service. In the earlier stages of this hands on lab, the lowest priced teir was used. In the real world, there may be times the application which relies upon your MySQL database will come under heavy load. In turn, this load may consume all of the resources available to your MySQL database instance, causing degraded performance. Scaling up your Azure Database for MySQL will help to noticeably improve performance in many of these cases, allowing you to keep processing your data efficiently.

Refer to these documentation articles for more infomation on [Pricing Tiers](https://docs.microsoft.com/en-us/azure/mysql/concepts-service-tiers) and [Compute Units](https://docs.microsoft.com/en-us/azure/mysql/concepts-compute-unit-and-storage) should you want to get more information on scaling your MySQL databases.

There are two options to scale up or scale down the Azure Database for MySQL service, either using the portal or via CLI.

### Using the Azure Portal

1. Open [https://portal.azure.com](https://portal.azure.com)

1. Open All Resources blade and click on the MySQL database that you want to scale

1. Click **Pricing Tier** option  
    ![Pricing Tier](images/mysql-pricing-option.png)

1. Change the **Compute Units** up or down as need and click OK to save changes.
    > Note that currently only the Basic level at either 50 or 100 compute units is available  

    ![Compute units](images/mysql-compute.png)

### Using the Azure CLI 2.0

1. Using the PowerShell prompt that you have open and connected to the Azure subscription

1. Using Azure CLI get information about the MySQL databases that you have access to:

    <span style="color:blue"> az mysql server list

1. The cli will provide a list of your MySQL databases, there should only be one. Note the resourceGroup and name values  
    ![MySQL Server List](images/az-mysql-server-list.png)

1. On the command prompt, run below command to scale up to 100 compute units

    <span style="color:blue"> az mysql  server update --resource-group [MyResourceGroupName] --name [mysqlDatabaseName] --compute-units 100

1. Run below command to scale down to 50 compute units

    <span style="color:blue"> az mysql  server update [MyResourceGroupName] --name [mysqlDatabaseName] --compute-units 50
    
    
    # CONCLUSION
As a fully integrated service, Azure Database for MySQL plugs you into Microsoft’s global network of value-add services, datacenters, security features, and round-the-clock monitoring.  Azure Database for MySQL is designed to deliver highly available MySQL Compatibility at scale to the forefront, all backed by a best of class SLA.   Trust Azure to keep your enterprise-ready MySQL applications up and running.
