# Settings of virtual server after isntall

## Install ssh server and net tools
```Bash
sudo apt update
sudo apt install openssh-server
sudo apt install net-tools
sudo apt install vim
```

## Install Virtualbox
https://www.virtualbox.org/wiki/Linux_Downloads 


## Setup Virtualbox vm to start after start of the server
Managing vm
```
vboxmanage startvm "Mint"                                                           
VBoxManage controlvm "Mint" poweroff             
```                                                                                                                       
Install Virtualbox extension for usb                                                
```
https://www.tecmint.com/enable-usb-in-virtualbox/
```
Automatic virtualbox start
```
http://lifeofageekadmin.com/how-to-set-your-virtualbox-vm-to-automatically-startup/
https://forums.virtualbox.org/viewtopic.php?f=7&t=60425
vi /etc/default/virtualbox
	VBOXAUTOSTART_DB=/etc/vbox                                                          
	VBOXAUTOSTART_CONFIG=/etc/vbox/autostart.cfg 
```