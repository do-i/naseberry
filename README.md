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
