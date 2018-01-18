# Deploy and configure Azure Database for MySQL

### Pre-requisites for the lab ###

Please login to PowerBI-VM to execute this lab.

### Before you start.

Throughout this hands on lab there are many cli commands given. Some of these contain values that are listed with like this [vaule], in instances where this square bracket notation is used you must provide an apropriate value.

### Provision the Azure Resources ###

1. Create the Azure resources.
    
  Simply click the Deploy to Azure button below and follow the wizard to create the resources. You will need to log in to the Azure Portal.
                                                                     
  [![Deploy to Azure](https://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FSpektraSystems%2FAzure-CosmosDB-and-Mysql-Postgres-Hands-on-Lab%2Fmaster%2Ftemplate%2Fmysql-resources.azuredeploy.json)

  The resources will be deployed to a Resource Group. You can delete the resource group in order to remove all the created resources at any time.


### Scenarios ###

Azure Database for MySQL

<a href="./story_a_deploy/content/1.md">Scenario 1: Provision Azure Database for MySQL</a>

<a href="./story_a_deploy/content/2.md">Scenario 2: Deplopy website code</a>

<a href="./story_a_deploy/content/3.md">Scenario 3: Popluate MySQL with data</a>

<a href="./story_a_deploy/content/4.md">Scenario 4: Scale up</a>

<a href="./story_a_deploy/content/conclusion.md">Conclusion</a>


# Azure Database for MySQL

Azure Database for MySQL provides a fully managed database service for application development and deployment allowing you to provision a MySQL database instance in minutes and scale it on the fly.
With comprehensive pricing models, and configurable sizing, you get all the features you need such as high-availability, monitoring and security, and backup and recovery, all with reduced management overhead.  These features are built into the service and are aligned to a simple, predictable pricing model. 
