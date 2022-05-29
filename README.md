# RaspAPServer
About to setup Ubuntu server with RaspAP


## Install Ubuntu server using Raspberry Pi Imager
* Download Raspberry Pi Imager from https://www.raspberrypi.com/software/
* Choose OS "Ubuntu server 20.04.4 LTS (RPI 3/4/400)/", SDCard
* Advanced options
  * Image customization options "to always use"
    - [ ] Disable overscan
    - [ ] Set hostname: raspberrypi.local
    - [x] Enable SSH
      
      ```
      Use password authentication
      ```
    - [x] Set username and password
      
      ```
      Username: daniel
      Password: ********
      ```
    - [x] Configure Wifi
      
      ```
      SSID: Daniel's Mesh
      Password: **********
      ```
    - [x] Wifi country: TW
    - [x] Set locale settings
      
      ```
      Time zone: Asia/Taipei
      Keyboard layout: us
      ```
    
  * Persistent settings
    - [x] Play sound when finished
    - [x] Eject media when finished
    - [x] Enable telemetry
* Start to burn.


## Install RaspAP

Begin with a clean install of the latest release of a supported Linux distribution.
```
ssh daniel@192.168.1.26
sudo apt-get update
sudo apt-get full-upgrade
sudo reboot
```

Install the packages that I need.
```
sudo apt-get install -y emacs
```

Invoke RaspAP's Quick Installer, and install with default settings (y)
```
curl -sL https://install.raspap.com | bash
```

Following a reboot, the wireless AP network will be configured as follows:
```
IP address: 10.3.141.1
Username: admin
Password: secret
DHCP range: 10.3.141.50 — 10.3.141.255
SSID: raspi-webgui
Password: ChangeMe
```
It is strongly recommended that you change these default credentials in RaspAP's Authentication and Hotspot > Security panels.


## Edit ssh configuration
Move ssh port 22 to 2022 
```
sudo cp /etc/ssh/sshd_config /etc/ssh/ssh_config_backup
sudo sh -c 'cat /etc/ssh/sshd_config_backup | sed s/#Port.*/"Port 2022\nAllowUsers daniel"/ > /etc/ssh/_sshd_config'
```

## Install firewall
Install ufw
```
sudo apt-get install -u ufw
```

Edit /etc/default/ufw and set DEFAULT_FORWARD_POLICY to ACCEPT:
```
sudo cp /etc/default/ufw /etc/default/ufw_backup
sudo sh -c 'cat /etc/default/ufw_backup | sed s/DEFAULT_FORWARD_POLICY=.*/DEFAULT_FORWARD_POLICY=\"ACCEPT\"/ > /etc/default/ufw'
```

Configure the rules and enable
```
sudo ufw allow 2022/tcp comment "SSH"
sudo ufw allow 1883/tcp comment "Mosquitto"
sudo ufw allow 53 comment "DNS"
sudo ufw allow 67 comment "BootStrap Service"
#sudo ufw allow 80 comment "http"
#sudo ufw allow 443 comment "https"
sudo ufw enable
sudo ufw status
```


## Reboot and login
``
sudo reboot now
ssh daniel@10.3.141.1 -p 2022
```
