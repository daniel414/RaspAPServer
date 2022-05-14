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

