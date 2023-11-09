# Archipelago.gg Ubuntu 22.04 Server Installation Guide
This guide was written assuming the user has Ubuntu Server 22.04 installed in a virtualized environment using an SSH client to communicate with the server. 
Please note we will not go over how to install Ubuntu Server 22.04 or how to use an SSH client. These steps will likely work with other versions of Ubuntu
or another Debian based system.

## Step 1: Get the latest Archipelago server software and unpack

1. Navigate to https://github.com/ArchipelagoMW/Archipelago/releases

2. Find the latest tar.gz asset (ex. Archipelago_0.4.3_linux-x86_64.tar.gz)

3. Right click the latest tar.gz and copy the link

4. Login to your server with your SSH client and navigate to where you want to install Archipelago and issue the following:
```
cd /home/YOUR_USER/
```
* Navigates to your user home directory
  - Ex. ```cd /home/brian/```
```
sudo wget PASTE_URL
```
* Grabs the tar.gz file from the internet
  - Ex. ```sudo wget https://github.com/ArchipelagoMW/Archipelago/releases/download/0.4.3/Archipelago_0.4.3_linux-x86_64.tar.gz```
```
sudo tar -xvzf FILE.tar.gz
```
* Unpacks the tar.gz file
  - Ex. ```sudo tar -xvzf Archipelago_0.4.3_linux-x86_64.tar.gz```
 
## Step 2: Installing Python tkinter & unzip packages

1. Check to make sure Python is installed on your server
```
python3 --version
```
* If it outputs a version, you're solid to move forward

2. Make sure you update your packages
```
sudo apt-get update
```

3. Install tkinter package to your server
```
sudo apt-get install python-tk
```

4. Install unzip package to your server
```
sudo apt-get install unzip
```

## Step 3: Generating player yaml files
Each player needs to do the following:

1. Navigate to https://archipelago.gg/
2. Click "Supported Games"
3. Click on a supported game and click "Settings Page"
4. Adjust settings and click "Export Settings"
   - Make sure you use a unique name for multiworld
5. Give your PLAYER_NAME.yaml files to the server host

## Step 4: Generating the player .ap12ac files and server .archipelago file
This part of the guide assumes you know how to move files in and out of your server.. for now.

1. For each game being hosted, import rom files to your /Archipelago/ folder

2. For each PLAYER_NAME.yaml file, import to your /Archipelago/Players/ folder

3. Issue the following command from the /Archipelago/ folder
```
sudo ./ArchipelagoGenerate
```
* This create a .zip file in /Archipelago/output/ which contains everything you need

4. Navigate to the /Archipelago/output/ folder and unpack that shit
```
sudo unzip FILE.zip
```
* Ex. ```sudo unzip AP_31742271521511105738.zip```

5. The folder /Archipelago/output/ now contains the following files
* .archipelago file for the server
* .ap12ac files for each player

6. Move the .archipelago file to the /Archipelago/ folder
```
sudo mv FILE.archipelago /home/YOUR_USER/Archipelago
```
* Ex. ```sudo mv AP_31742271521511105738.archipelago /home/brian/Archipelago/```

7. Distribute the .ap12ac files to each corresponding player

## Step 5: Starting your server
I'm a newblett and don't know how to run this as a service in the background... so you're stuck with it in your terminal until you're done with it. I'm going to work on a docker configuration in the future for this project.

1. While in your /Archipelago/ folder issue the following command:
```
sudo ./ArchipelagoServer FILE.archipelago
```
* Ex. ```sudo ./ArchipelagoServer AP_31742271521511105738.archipelago```

2. The output will tell you the IP address and port for users to connect to
