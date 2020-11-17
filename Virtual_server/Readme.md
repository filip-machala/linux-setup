# Settings of virtual server after isntall

## Install ssh server and net tools
```Bash
echo "Installing tools started."
sudo apt update
sudo apt install openssh-server
sudo apt install net-tools
sudo apt install vim
sudo apt update
sudo apt upgrade
echo "Installing tools finished."
```

To pass public ssh key to server
```
ssh-copy-id username@ip
```

Disable password logon
```Bash
sudo vi /etc/ssh/sshd_config
```

Change PasswordAuthentication option to
```
PasswordAuthentication no
```

Restart service
```
sudo systemctl restart ssh
```

## Install Virtualbox
https://www.virtualbox.org/wiki/Linux_Downloads 
```Bash
echo "Installing Virtualbox started"
sudo echo "deb [arch=amd64] https://download.virtualbox.org/virtualbox/debian eoan contrib" >> /etc/apt/sources.list;
wget -q https://www.virtualbox.org/download/oracle_vbox_2016.asc -O- | sudo apt-key add -;
sudo apt-get update;
sudo apt-get install virtualbox-6.1;
echo "Installing Virtualbox finished"
```



## Setup Virtualbox vm to start after start of the server
Create service and enable it. Please ensure that VM already exists.
``` Bash
echo "Creating service to autostart VM started"
echo "Input full VM name to create service";
read SERVICENAME;
USER=$(whoami)
sudo echo "[Unit]
Description=$SERVICENAME
After=network.target virtualbox.service
Before=runlevel2.target shutdown.target
 
[Service]
User=$USER
Group=vboxusers
Type=forking
Restart=no
TimeoutSec=5min
IgnoreSIGPIPE=no
KillMode=process
GuessMainPID=no
RemainAfterExit=yes
 
ExecStart=/usr/bin/VBoxManage startvm $SERVICENAME --type headless
ExecStop=/usr/bin/VBoxManage controlvm $SERVICENAME acpipowerbutton
 
[Install]
WantedBy=multi-user.target" > /etc/systemd/system/"$SERVICENAME".service;
sudo systemctl daemon-reload
sudo systemctl enable "$SERVICENAME"
echo "Creating service to autostart VM finished"
```
## You are done!

Not actual

//cd /etc/init.d/
//services=(vboxautostart-service vboxweb-service vboxballoonctrl-service)
//base_url="https://www.virtualbox.org/svn/vbox/trunk/src/VBox/Installer/linux"
//for service in "${services[@]}"
    do
      wget "${base_url}/${service}".sh -O "${service}" \
      && chmod +x "$service"  \
      && update-rc.d "$service" defaults 90 10
    done
//

Managing vm
```
vboxmanage startvm "Mint"                                                           
VBoxManage controlvm "Mint" poweroff             
```     

Script based on this article.
https://linux.m2osw.com/autostart-virtualbox-vms