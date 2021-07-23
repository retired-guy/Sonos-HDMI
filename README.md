# Sonos-HDMI
Display Sonos zone currently playing track on HDMI monitor 

Build notes:
1. Burn Raspberrypi OS Lite (32-bit version) to a micro-sd card
2. Create an empty file named "ssh" in the /boot directory of the sd card
3. Create a file named "wpa_supplicant.conf" in the /boot directory of the sd card, with your wifi info
4. Edit the file "config.txt" in the /boot directory, adding/changing these lines:
  # uncomment to force a specific HDMI mode (this will force VGA)
  hdmi_group=2
  hdmi_mode=87
  hdmi_cvt=800 480 60 6 0 0 0
  hdmi_drive=1
5. Put the sd card into the Pi Zero W, power it up with HDMI screen plugged in
6. Ssh into the IP address displayed on the HDMI screen, e.g. ssh pi@192.168.68.123 (default pwd is "raspberry")
7. sudo raspi-config
   set Local
   set Timezone
   set hostname (if desired)
   reboot
8. Ssh in again, then:
   sudo apt install python3-pip
   sudo usermod -a -G video pi
   sudo apt install libopen-jp2-7-dev
   sudo apt install libtiff5
   sudo apt install ttf-dejavu
   pip3 install soco
   pip3 install Pillow
9. cd ~
   wget https://github.com/retired-guy/Sonos-HDMI/archive/refs/heads/main.zip
   unzip main.zip
   mv Sonos-HDMI-main sonos
   cd sonos
   sudo cp sonos.service /etc/systemd/system/sonos.service 
   sudo systemctl daemon-reload
   Play something to the Sonos zone to be monitored, and:
   sudo systemctl start sonos
   If everything's working, the playing track should be displayed.  If so:
   sudo systemctl enable sonos
   and reboot.  It should auto-start
   
   References:
   Creating a service: https://www.raspberrypi.org/documentation/linux/usage/systemd.md
   Setting up a headless Pi: https://www.raspberrypi.org/documentation/configuration/wireless/headless.md
   
   [photo](https://1.bp.blogspot.com/-WKMlpBRRxEQ/YPn4OAnMM9I/AAAAAAAAuoU/Odb5FPkRwFYsirDvKZnRG-oSyxkjS2IqgCLcBGAsYHQ/s2048/FAAFCA05-9228-43DB-9009-04EAE065DCC2.jpeg)
   
   
   
   
