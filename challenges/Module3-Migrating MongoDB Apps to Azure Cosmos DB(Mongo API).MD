# Module 3: Migrate MongoDB Application to Azure Cosmos DB(SQL API) 
## Access Cosmos DB account with SQL API (created in Module-1)
1. **Launch** a **browser** and navigate to https://portal.azure.com. **Login** with your **Microsoft Azure** credentials.<br/>
2. **Click** on **Resource Group** provided which contains the all the resources, click on created **Azure Cosmos DB account**(with SQL API) under **Overview** tab.<br/>
<img src="images/sqlcosmos.jpg"/><br/>
3. **Click** on **Keys** option present under Cosmos DB Account blade, and copy **URI** and **PRIMARY KEY**.<br/>
<img src="images/sqlkey.jpg"/><br/>
4. **Go** back to **Visual Studio Code** IDE and paste the **URI** value against **DOCUMENT_DB_ENDPOINT**, **PRIMARY KEY** against **DOCUMENT_DB_PRIMARYKEY**, **DOCUMENT_DB_DATABASE** and change the **API_MODE** to **SQL** in the **config.js**.<br/>

5. **Navigate** back to the Azure Portal's Resource groups option present in the favourites menu on the left side panel and select the **resource group** and click on **Azure Cosmos DB Account** then, click on **Replicate data globally** option present under **SETTINGS** section in **Cosmos DB Account** blade.<br/>

6. Copy the **WRITE REGION** and paste it against **DOCUMENT_DB_PREFERRED_REGION** in **config.js** file which is already opened in **Visual Studio Code** IDE and save this file.<br/>
<img src="images/sqlconfig.jpg"/><br/>
7. **Go** to /home/CosmosDB-Hackfest/ContosoAir/src/ContosoAir.Services in file system, right click and select **Open Terimal Here** as shown below:<br/>
<img src="images/jumpvm4.jpg"/><br/>
8. Now execute the following commands one by one in command prompt.<br/>

```bash
node sql_db_flightinsert.js
node sql_db_insert.js
npm start
```
<img src="images/sqlcommands.jpg"/><br/>

9. Now, to start the **ContosoAir Website** layer, go to /home/CosmosDB-Hackfest/ContosoAir/src/ContosoAir.Website. Open terminal from there and run **ng serve** command in terminal. Minimize the terminal once command is executed, do not exit or CTRL+C.<br/>

```bash
ng serve
```
<img src="images/jumpvm6.jpg"/><br/>

10. It will create three different collections named **SeatsCollection**, **DealsCollection** and **BookingsCollection** with sample data.<br/>

11. Switch to **Azure Portal**, navigate to **Resource groups** option present in the favourites menu on the left side panel and select the resource group then click on **Azure Cosmos DB Account** named.<br/>

12. **Click** on **Data Explorer** option. It will display the collection created in **Azure Cosmos DB Account**.<br/>
<img src="images/sqldataexplore.jpg"/><br/>

## Launch the Application
1. Copy the **localhost URL** [http://localhost:4200](http://localhost:4200) from the **terminal** and paste it in **Web Browser** and press enter. There's a shortcut created for your already on desktop for this, you can open website using that as well.<br/>
1. You will see the **sign-up** page. You need to **login** to App using your **Microsoft Account**(formerly live-id). If you do not have a live-id, you can create one by following instructions given on page.<br/>
<img src="images/signup.jpg"/><br/>
1. Once you get login, you will be redirected to **ContosoAir app**.<br/>
<img src="images/contoso1.jpg"/><br/>
1. Enter **Departure date** and **Return date** in **YYYY-MM-DD** format and click **Find Flights** button.<br/>
<img src="images/contosoapp.jpg"/><br/>
