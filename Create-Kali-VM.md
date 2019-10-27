# Creating a Kali Virtual Machine (VM)

Yes, there are plenty of other guides like this. I am creating this as a place to store helpful tips for the folks I know looking to get started. I could like to other "how-to" posts or videos, but those may disappear over time. This guide is also written with certain assumed prerequisites (hardware and software) that may interfere with some of these steps for you. At a high level, this guide is written assuming you have 16GB of memory, as well as VMware Workstation installed. In general, we'll want to execute the following:

1. [Download the latest VMware/Virtual Box image from Offensive Security](#download-image)
2. [Configure Virtual Machine resources](#configure-resources)
3. [Change the root password and SSH keys](#change-keys)
4. [Download and install updates](#updates)
5. [Take a snapshot ("Golden Image") as a restore point](#snapshot)
6. [USB Network Interface Card](#usb-nic)
7. [Video Demo](#video-demo)

## <a name="download-image"></a>1. Downloading the Image

1. You'll want to download the latest stable VMware image from:  https://www.offensive-security.com/kali-linux-vm-vmware-virtualbox-image-download/. At the time of this writing this is the image named "Kali Linux VMware 64-Bit" Version "2019.3". 
2. The SHA256 checksum of this download is " 288324d243865b77099585f4952fadd790c8fc10414820eb57f39414d686c0c0 " which we will use to verify the integrity of the downloaded file.
3. To verify the checksum, rick click on the file "kali-linux-2019.3-vmware-amd64.7z" > CRC SHA > SHA-256 which should present a pop-up window (after a few seconds) with the following test:
```
Name: kali-linux-2019.3-vmware-amd64.7z
Size: 2287213608 bytes (2181 MiB)
SHA256: 288324D243865B77099585F4952FADD790C8FC10414820EB57F39414D686C0C0
```

4. Once the checksum is verified, we need to extract the .7z archive. Right click on the "kali-linux-2019.3-vmware-amd64.7z" file > 7-Zip > Extract to "kali-linux-2019.3-vmware-amd64.7z/" Note: You can move this to another location, such as your Documents folder.

## <a name="configure-resources"></a>2. Configure Virtual Machine Resources

1. Within VMware Workstation select the File menu, and click on "Open" 
2. Open the file "Kali-Linux-2019.3-vmware-amd64.vmx"
3. Select "Edit virtual machine settings"
4. Change "Memory" to 4GB 


## <a name="change-keys"></a>3. Change the root password and SSH keys

You are now ready to start your VM. From the VMware Workstation landing page, click "Power on this virtual machine"

1. Select "I Copied it"
2. The default username is "root" (no quotes) and the default password is "toor" (no quotes)
3. Open Terminal and enter 'passwd'. You will be prompted to select your own password and enter it twice to confirm you did not have a typo. Store this password in your password manager/password vault.
4. Change your SSH keys with the following commands:

```
#This will Change Directories to the appropriate location

cd /etc/ssh/

#Make a folder to save the default keys

mkdir default_keys

#Move the default keys to this new folder

mv ssh_host_* default_keys/

#Create new keys

dpkg-reconfigure openssh-server

```

## <a name="updates"></a>4. Download and install updates

Open Terminal and run the commands below. You may be prompted to answer a few questions. After reading the information, you should be OK to proceed with the defaults. You do not have to enter any text with a line starting with "#" these are comments to explain what each command is doing.

``` 
# This first command is going to update the apt list of packages in need of an updating

apt-get update  

# This command updates all the packages identified in the last command that require updating. This will also resolve dependency conflicts

apt-get dist-upgrade

# Moving forward you can run the following for regular updates, until you are prompted to re-run apt-get dist-upgrade

apt-get update && apt-get dist-upgrade
```

## <a name="snapshot"></a>5. Take a snapshot

1. Click on the icon for "Take a snapshot of this virtual machine"
2. Create a name for this snapshot, and add a useful description. Generally, include the date and any relevant information such as "Intial build and update on 26 OCT 2019"
3. You can now restore to this snapshot if you have issues with future installs or configuration changes.
4. You must restore to a "clean" snapshot and apply all updates before connecting to test networks.

## <a name="usb-nic"></a>6. USB Network Interface

When using the virtual machine to test a physical network, we want to use the USB Network Interface Card (NIC) so that the virtual machine is directly connected to the network. This accomplishes two things: 

1. your host machine (physical laptop) is not connected to the network to be tested; and 
2. you do not have to worry about conflicts with tools when using a bridged interface.

To change the network settings to use the USB NIC:
1. In VMware Workstation select the VM Menu > Removable Devices > Select your USB NIC
2. Within the VM update your network connection to use the newly enabled ethernet interface

## <a name="video-demo"></a>7. Video Demo
Here is a quick video showing the above steps to show you the necessary steps in order to keep the written steps shorter.

[Link to Demo Video]()