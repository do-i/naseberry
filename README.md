Naseberry
=========

Network Attached Storage on Raspberry Pi 3
------------------------------------------

#### Install Open Media Vault
###### copy the image to sdcard
```
 sudo dd bs=4194304 if=omv_2.2.5_rpi2_rpi3.img of=/dev/sdx
```
###### sync to make sure all data is copied
```
sync
```
#### Boot up pi
Insert sdcard to raspberry pi, connect cat5 and power it on.

#### Connect to WebUI
Find out IP address of the pi
Open browser at the IP address

###### default WebUI login/password
* login: admin
* password: openmediavault

###### default ssh login/password
* login: root
* password: openmediavault

#### Install LUKS plugin
In OMV WebUI;
###### OMV-Extras
Navigate to ```System -> OMV-Extras.org```.
Then, make sure ```OMV-Extras.org``` and ```OMV-Extras.org Testing``` are enabled

###### Plugins
Navigate to ```System -> Plugins```. Select ```openmediavault-luksencryption 2.1.2```.
And click ```Install``` button.

###### Prepare USB Drive
Plug USB Hard drive to the pi.
Navigate to ```Storage -> Physical Disks``` in WebUI.
Select the device something like ```/dev/sda```.
Then, click on ```Wipe``` button.

###### Encription
Navigate to ```Storage -> Encryption```.
Click ```Create``` button. Select the device from the dropdown.

###### Unlock
May need to unlock before create a filesystem???

###### File System
Create file system on LUKS device
Navigate to ```Storage -> File Systems```.
Click on ```Create``` button.
Select the ```LUKS device``` from the dropdown.
Enter Volume name ```DataSafe``` or whatever you like.
Then, click on ```Mount``` button.

###### Make Directory
Connect to raspberry via ssh as root
```
ssh root@raspberry
```

Create Directory
```
cd /media/[UUID]
mkdir datasafe
```

###### Shared Folders
Navigate to ```Access Rights Management -> Shared Folders```. Click on ```Add``` button. Select ```DataSafe``` or (whatever you chose) volume.

###### Create User
via WebUI
TODO: add more content here later


###### Create shortcut
```
ssh panda@raspberry
ln -s /media/[UUID]/datasafe backup
```
###### public key
add public key to ```/home/panda/.ssh/authorized_keys```

### Portability
Unplug USB Drive from Pi and plug it in to any Linux PC

###### Install LUKS on Linux PC
```
sudo apt-get install cryptsetup
```

###### Decrypt the volume
```
sudo cryptsetup luksOpen /dev/sdd DataSafe
```

###### Mount
```
sudo mkdir /media/data_safe
sudo mount /dev/mapper/DataSafe /media/data_safe
```

###### Unmount
```
sudo umount /media/data_safe
sudo cryptsetup luksClose DataSafe
```
