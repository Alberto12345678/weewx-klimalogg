klimalogg - WeeWX driver for TFA KlimaLogg Pro
Copyright 2016 Luc Heijst

Klimalogg is a weewx extension to read data from the KlimaLogg Pro station
and up to 8 thermo/hygro sensors. It saves data to its own database, then
those data can be displayed in weewx reports.  This extension also includes
a sample skin that illustrates how to use the data.


Installation instructions (This is a more detailed Guide for the Installation):

1)  While Installing the WEEWX Software proceed until the point where you chose the Wheater Station and choose "Simulator"
    Note, that there is an easy two-step istallation guide for weewx right here: http://weewx.com/apt/

2)  Use Putty to access your Pi over Network. (If you use an WIFI Dongle, get through the Installation Process of your Device first)

3) Download the latest Version of the Klimalogg Extension directly to your Pi:
    wget -O weewx-kl.zip https://github.com/matthewwall/weewx-klimalogg/archive/master.zip
4) Install the Klimalogg Driver and Skin (notice: IF you run into Permission Issues, use "sudo")
    sudo wee_extension --install weewx-kl.zip

5) Change your previously chosen Simulator with the Klimalogg Driver
    sudo wee_config --reconfigure --driver=user.kl

  5.1) You will get through the general Installation process again.
       Just type your Coordinates in again, if the system haven´t recognised them

6) Notice that the System will ask you for the Driver.
   It should be written there already,  but if not choose the Driver-Numer from the list
   
7) At the end, all is saved in the weewx.conf which you have to edit (easiest way is over a programm like filezilla)

    7.1) Access your Pi over Filezilla (port for the System is 22)
    7.2) You could run into Permission Issues if you try to edit the file. If so, just copy the file to an archive which has the              permissions to edit, like /home/pi 
     to do that type:
     sudo mv "directory of the weewx.conf" /home/pi (this could look like: sudo mv )
     now you can edit the file

8) You have to remove a whole section in the conf (for simple findings use Sublime Text. It has a more Structured View)
   You should find the conf file at /etc/weewx (there are more then one. Just edit the file with the exact name: weewx.conf)
-- notice, that you will permernantly change the configuration

  search for the section [simulator]
  if it´s present, remove it. Otherwise proceed to 9)

9) Go to [StdReport] and remove the [[StandardReport]] section 

10) in the [StdReport] you will find the data_binding. Be sure that it´s equal kl_bilding

11) Move the file back to it´s former location
  sudo mv /home/pi/weewx.conf /etc/weewx

12) reboot your Pi to make all changes excutable
  sudo reboot

13) To Sync the Station and your Pi with the Stick, use the USB Button on the device. 
    Hold it longer until you see USB continiously on your Display of the Klimalogg
   
14) To make sure, that your data is written in the right database. Go to /var/lib/weewx and delete the weewx.sdb or rename it
    You can delete it through putty: sudo rm /var/lib/weewx/weewx.sdb
