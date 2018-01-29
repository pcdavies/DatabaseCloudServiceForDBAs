Update January 22, 2018

# Setup

This workshop requires several setups steps that are normally done in advance as part of an automated process prior to running the labs.  In cases where a customer wishes to run through the workshop themselves on their own without the support of Global Services Engineering (GSE) they must first walk through the following steps.  

### **STEP 1**: Log into the Cloud Console and create DBCS_WorkshopImage

The following creates a new DBCS Enterprise instance with backup to cloud.  Use your own SSH key or generate a new one.  

-	Log into your identitity domain/trial account.

	![](images/setup/001.png)

-	Select the appropriate account type and data center.

	![](images/setup/002.png)

	![](images/setup/003.png)

	![](images/setup/004.png)

-	Customize dashboard if you do not see any current services.

	![](images/setup/005.png)

-	Select show Database

	![](images/setup/006.png)

-	Select Database, and then Open Service Console

	![](images/setup/007.png)

	![](images/setup/008.png)

-	Create Service

	![](images/setup/009.png)

-	Enter Service Name and Software Release.  Be sure to select Oracle Database 12c Release**2**.

	![](images/setup/010.png)

-	Enter Administration passwords (Alpha2018_) and then select SSH Key

	![](images/setup/011.png)

-	Select Create a New Key Pair.

	![](images/setup/012.png)

-	Download the key pair and save to your hard drive.  Extract the zip file afterwards.

	![](images/setup/013.png)

	![](images/setup/014.png)

-	Enter Backup and Recovery Configuration.  Be sure to select Cloud Storage Only and use this URL for storage.  Substitute your identity domain in the <IDENTITY DOMAIN> part below, and also replace us2 with your data center.  Select create the storage container.
	- `https://storage.us2.oraclecloud.com/v1/Storage-<IDENTITY DOMAIN>/oracle-data-storageg-1`

	![](images/setup/015.png)

-	Then select 'create'.  This will take about 30 minutes to create.

	![](images/setup/016.png)


### **STEP 2**: Download Files and transfer to DBCS_WorkshopImage

-	Go to the following site to download opc_installer.zip:  `http://www.oracle.com/technetwork/database/availability/oracle-cloud-backup-2162729.html`

	![](images/setup/001.1.png)

-	Go to the following site and download the adobe repository: `https://get.adobe.com/flashplayer/`.  Do not select the default - select download for a different operating system (Linux 64 bit).

	![](images/setup/003.1.png)

-	Select the version YUM.

	![](images/setup/004.1.png)

	![](images/setup/005.1.png)

-	Go to the database console and retrieve the IP address.

	![](images/setup/017.png)

	![](images/setup/018.png)

-	Create a ppk (windows compatible) version of the existing downloaded keys.  If you are on a Linux platform this is not necessary.  Open Puttygen (free download from the Internet).

	![](images/setup/019.png)

-	Go to the directory and select/import the private key.  You must first unzip the key bundle.

	![](images/setup/020.png)

-	Save Private key.

	![](images/setup/021.png)

-	Save without a passphrase.

	![](images/setup/022.png)

	![](images/setup/023.png)

-	Open WinSCP (internet download) and log in to the IP address noted above from the Cloud Console with your private ppk key.

	![](images/setup/024.png)

-	Ignore the warning.

	![](images/setup/025.png)

-	Drag the following files to the oracle folder.

	![](images/setup/026.png)

	![](images/setup/027.png)

### **STEP 3**: Login and run install scripts

-	Open Putty and log into the DBCS instance.

	![](images/setup/028.png)

-	Select your SSH private key

	![](images/setup/029.png)

-	Log in as opc

	![](images/setup/030.png)

-	Switch to oracle user and unzip the install.zip file and then exit oracle login
	- `sudo su - oracle`
	- `unzip install.zip`
	- `./install.sh`
	- `exit`

	![](images/setup/031.png)

-	Log in as root and install the adobe rpm
	- `sudo su -`
	- `cd /home/oracle`
	- `rpm -ivh adobe-release-x86_64-1.0-1.noarch.rpm`

	![](images/setup/032.png)

-	Install packages for desktop and VNC (this will take a few minutes).
	- `./yum.sh`

	![](images/setup/035.png)

### **STEP 4**: Setup Desktop

-	Log back into the Cloud Console and select Database Service.

	![](images/setup/036.png)

	![](images/setup/037.png)

-	Select Access Rules on the right.

	![](images/setup/038.png)

	![](images/setup/039.png)

-	Create rule.  Note you need to refresh your screen to see the new rule after selecting create.

	![](images/setup/040.png)

### **STEP 5**: Start VNC Viewer and log into the desktop

-	Go back to your SSH session (or open a new one if you closed it) and start VNC Server.  You can adjust the geometry to match your screen.  You will be prompted to enter a password.  Do not use the password that we have been specifying in other places in this lab document.  **VNC is open to the internet.  Select your own secure password**.
	- `vncserver -geometry 1280x1024`

	![](images/setup/041.png)

-	Start your VNC Viewer and log in.

	![](images/setup/042.png)

-	You will see a prompt to log into root.  Cancel this.  This pops up from time to time, always cancel.

	![](images/setup/043.png)

-	We need to disable the screen saver to prevent a screen unlock prompt.  Go to the system menu on the desktop and de-activate screen saver.  If you delay in this step and the screen locks up you will need to kill the vncserver (`vncserver -kill :1`) and restart it (`vncserver`) in your terminal window.

	![](images/setup/044.png)

	![](images/setup/045.png)

### **STEP 6**: Set up shortcut to SQLDeveloper and import connections

-	Right click on the desktop and create a new launcher on the desktop
	- `/u01/app/oracle/product/12.2.0/dbhome_1/sqldeveloper/sqldeveloper/bin/sqldeveloper`

	![](images/setup/046.png)

	![](images/setup/047.png)

-	Select the sqldeveloper icon from the following directory: `/u01/app/oracle/product/12.2.0/dbhome_1/sqldeveloper/`

	![](images/setup/048.png)

	![](images/setup/049.png)

-	Double click on the desktop icon to start sqldeveloper. Select no to import connections.

	![](images/setup/050.png)

-	Right click on connections and select import connections.

	![](images/setup/051.png)

-	Browse for connections file.

	![](images/setup/052.png)

	![](images/setup/053.png)

	![](images/setup/054.png)

	![](images/setup/055.png)