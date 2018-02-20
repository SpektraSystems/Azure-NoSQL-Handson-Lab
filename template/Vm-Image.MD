### Create virtual machine
1.	Click the **New** button found on the upper left-hand corner of the Azure portal.<br/>
2.	Select Compute, and then select **Ubuntu Server 16.04 LTS**.<br/>
3.	Enter the virtual machine information. For Authentication type, select **Password** and enter the Password. When complete, click **OK**.<br/>
<img src="images/vm1.png"/><br/>
4.	Select a size for the VM. To see more sizes, select View all or change the Supported disk type filter.<br/>
<img src="images/vm2.png"/><br/>
5.	Under Settings, keep the defaults and click **OK**.<br/>
6.	On the summary page, click Ok to start the virtual machine deployment.<br/>
7.	The VM will be pinned to the Azure portal dashboard. Once the deployment has completed, the VM summary automatically opens.<br/>

### Create ubuntu vm images 
1.	Click on the **Resource Group** icon on the Menu navigation bar.<br/>
<img src="images/image1.png"/><br/>
2.	From azure portal, go to virtual machine and select the **JumpVM**. In Overview section, click on **Connect** button. It will show username with IP address copy that IP address.<br/>
<img src="images/image2.png"/><br/>
3.	Now run putty.exe from your PC.
4.	This is the application window that pops up when you run putty.exe. Paste the Username with Public IP address of the VM that you copied in step 2 to the Host Name (or IP address) box of the putty. Port will be 22 by default. Click on **Open**.<br/><br/>
<img src="images/image3.jpg"/><br/>
5.	The PuTTY Security Alert will pop up. Click on **Yes**.<br/>
<img src="images/image4.jpg"/><br/>
6.	Login using your password for the Virtual Machine provided while creating virtual machine.<br/>
<img src="images/image5.jpg"/><br/>
7.	Ubuntu ensures the authenticity of software packages by verifying that they are signed with GPG keys, so we first must import they key for the official MongoDB repository.<br/>
```
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2930ADAE8CAF5059EE73BB4B58712A2291FA4AD5
```
<img src="images/custom.jpg"/><br/>
8.	Next, we have to add the MongoDB repository details so apt will know where to download the packages from.Issue the following command to create a list file for MongoDB.<br/>
```
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.6 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.6.list
```
<img src="images/custom1.png"/><br/>
9.	After adding the repository details, we need to update the packages list.<br/>
```
sudo apt-get update
```
<img src="images/custom2.jpg"/><br/>
10.	Now we can install the MongoDB package itself.<br/>
```
sudo apt-get install -y mongodb-org
```
<img src="images/custom3.jpg"/><br/>
11.	 Start the mongodb Service by running the following command:<br/>
```
sudo service mongod start
```
<img src="images/custom4.jpg"/><br/>
12.	 Verify the mongoDB database while running the mongo as shown below.<br/>
```
mongo
```
<img src="images/custom5.jpg"/><br/>
13.	You can also verify the records in mongoDB database while running the following commands.<br/>
```
shows dbs
use contosoairdb3
db.contoairdb3.insert({"test":"test"})
exit
```
<img src="images/custom6.jpg"/><br/> 
14.	Run the command for git clone:<br/>
```
git -C /home/demouser/ clone https://github.com/SpektraSystems/CosmosDB-Hackfest.git
```
<img src="images/cusom7.jpg"/><br/>
15.	Run the following command, it will update the package lists for upgrades for packages that need upgrading, as well as new packages that have just come to the repositories.<br/>
```
sudo apt-get update && sudo apt-get -y upgrade
```
<img src="images/custom8.jpg"/><br/>
16.	Run following command for installing the Personal Package Archive. This will give you access to its contents:<br/>
```
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
```
<img src="images/custom9.jpg"/><br/>
17.	Run the following command for installing Node.js:<br/>
```
sudo apt-get install -y nodejs
```
<img src="images/customa.jpg"/><br/>
18.	Check the available Node.js versions with following command.<br/>
```
npm -v
```
<img src="images/customb.jpg"/><br/>
19.	After installing we need for verifying the application with given commands:<br/>
```
ls
cd CosmosDB-Hackfest/ContosoAir/src/ContosoAir.Services/
sudo npm install
npm start
```
<img src="images/customc.jpg"/><br/>
20.	To start the ContosoAir Website layer, run the below commands:<br/>
```
cd
cd CosmosDB-Hackfest/ContosoAir/src/ContosoAir.Website/
sudo npm install -g @angular/cli
```
<img src="images/customd.jpg"/><br/>
21.	Install repository and key with the following script:<br/>
```
cd
curl https://packages.microsoft.com/keys/microsoft.asc | gpg --dearmor > microsoft.gpg
sudo mv microsoft.gpg /etc/apt/trusted.gpg.d/microsoft.gpg
sudo sh -c 'echo "deb [arch=amd64] https://packages.microsoft.com/repos/vscode stable main" > /etc/apt/sources.list.d/vscode.list'
```
<img src="images/custome.jpg"/><br/>
<img src="images/customf.jpg"/><br/>
22.	Then update the package cache and install the package using following commands:<br/>
```
sudo apt update
sudo apt install code
```
<img src="images/update.jpg"/><br/>
<img src="images/installcode.jpg"/><br/>
23. Run the below command for installing vscode:
```
sudo sed -i 's/BIG-REQUESTS/_IG-REQUESTS/' /usr/lib/x86_64-linux-gnu/libxcb.so.1
```
<img src="images/codenew.jpg"/><br/>
23.	Install a desktop environment on your Linux VM. Next, install xfce using apt as follows: <br/>
```
sudo apt-get update
sudo apt-get install xfce4 -y
```
<img src="images/update.jpg"/><br/>
<img src="images/xfce.jpg"/><br/>
24.	Install xrdp on your Ubuntu VM as follows:<br/>
```
sudo apt-get install xrdp -y
```
<img src="images/xrdp.jpg"/><br/>
25.	Configure xrdp to use xfce as your desktop environment as follows:<br/>
```
echo xfce4-session >~/.xsession
```
<img src="images/session.jpg"/><br/>
26. Restart the xrdp service for the changes to take effect as follows:<br/>
```
sudo service xrdp restart
```
<img src="images/google.jpg"/><br/>
27. Go to azure portal and select **Resource Group>Virtual Machine>Networking**. Add Inbound rule under networking as shown below:<br/>
<img src="images/inbound.jpg"/><br/>
28. Provide the following parameters for creating Inbound Rule:<br/>
<img src="images/port3389.jpg"/><br/>
29. Go back to putty and use netstat on your Linux VM to verify that your VM is listening for RDP connections as follows:<br/>
```
sudo netstat -plnt | grep rdp
```
<img src="images/netstat.jpg"/><br/>
30. The following example shows the VM listening on TCP port 3389 as expected:<br/>
<img src="images/netset2.jpg"/><br/>
31. After adding the remote desktop details, we need to update the packages list with following command.<br/>
```
sudo apt-get -f install -y
```
<img src="images/installrdp.jpg"/><br/>

32.	Configure google chrome while running following commands one by one:<br/>
```
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
sudo dpkg -i google-chrome-stable_current_amd64.deb
```
<img src="images/google.jpg"/><br/>
<img src="images/google1.jpg"/><br/>

33.	Connect to your Linux VM using an SSH client. In the SSH window, type the following command:<br/>
```
sudo waagent -deprovision
```
<img src="images/installrdp1.jpg"/><br/>
34.	From azure portal, go to virtual machine and select the JumpVM. In Overview section, click on Capture button.<br/>
<img src="images/rdp1.jpg"/><br/>
35.	 Click on Create button for creating image.<br/>
<img src="images/rdp2.jpg"/><br/>
36.	 Once the image deployed click on the it and go to image.<br/>
<img src="images/rdp3.jpg"/><br/>
37.	Click on Create VM for deploying virtual machine with created image.<br/>
<img src="images/rdp4.jpg"/><br/>

### Connect to Virtual Machine
1. From azure portal, go to virtual machine and select the JumpVM. In Overview section, click on **Connect** button. It will show username with IP address copy that IP address.<br/>
<img src="images/jumpvm1.jpg"/><br/>
1. Click on start button and search for **Remote Desktop Connection** and click on it.<br/>
1. Remote Desktop Connection window will pop-up in that provide the IP Address that you copied in above step.<br/>
<img src="images/rdc.jpg"/><br/>
1. Click on **Yes** button in Remote Desktop Connection Wizard.<br/>
<img src="images/rdc2.jpg"/><br/>
1. Enter the credentials provided in the mail to connect to VM.<br/>
<img src="images/xrdp.jpg"/><br/>

    > Note If you get err:connecting at first login: Click OK and try again.
1. Once you are logged in the Ubuntu OS click on Application for accessing visual studio code as shown blow.<br/>
<img src="images/jumpvm2.jpg"/><br/>
1. Go to **File** and select the **Open Folder**.
<img src="images/vscode1.jpg"/><br/>
1. Select demouser and Click on CosmosDB-Hackfest.<br/>
<img src="images/vscode2.jpg"/><br/>
1. Now, open **scr** folder in VS code.<br/>
<img src="images/vscode3.jpg"/><br/>
1. Notice the folders hierarchy in VS code.<br/>
<img src="images/vscode3.jpg"/>.<br/>
