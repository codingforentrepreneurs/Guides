# **UNDER DEVELOPMENT** 

# Django Pi Network Server Guide
Setting up our Raspberry Pi 3 Model B (and up) to serve a Django project using Apache2.



Adapted from [Offical Docs](https://www.raspberrypi.org/learning/software-guide/quickstart/)

### Software Downloads:

[SDFormatter](https://www.sdcard.org/downloads/formatter_4/) -- to erase/format your microSD card

[Etcher](https://www.etcher.io/) -- to add the operating system to your microSD card

[Raspbian Jessie with Pixel](https://www.raspberrypi.org/downloads/raspbian/) A Raspberry Pi Linux/Debian Operating system. [Docs](https://www.raspbian.org/)

### Setup the Pi

1. Flash microSD card:

    [SDFormatter](https://www.sdcard.org/downloads/formatter_4/)

    1. Download SDFormatter for your System version.

    2. Install

    3. Insert your microSD card.

    4. Open SDFormatter

    5. Select card from list

    6. Select "Quick Format" as option.

    7. Write any name you'd like

    8. Click "Format"


2. Download [Raspbian Jessie with Pixel](https://www.raspberrypi.org/downloads/raspbian/) Zip.

    1. Once downloaded, extract/unzip downloaded contents.

    2. The file is about 1.5 GB so it might take a little while to download.


3. Download and open [Etcher](https://www.etcher.io/)

4. Run Etcher and select the Raspbian image

5. Select the SD card drive (or ensure it's selected)

6. Click **Burn** to transfer Raspbian to microSD card. Once complete, you can safetly pull the card out (it will automatically eject/unmount the card)

7. Insert microSD card into Raspberry Pi (gold pins facing the bottom of the Pi)

8. Power on Raspberry Pi

9. Connect Pi to Network

10. Get IP Address of the Pi




### Apache2 + Django


Update Software:

```
sudo apt-get update
sudo apt-get upgrade
```

Install Apache2:

```
sudo apt-get install apache2 -y
```


Apache2 Settings:

```
sudo nano /etc/apache2/sites-available/000-default.conf

```

```
<VirtualHost *:80>
    ServerName www.example.com

    ServerAdmin webmaster@localhost

    Alias /static /home/pi/Dev/cfehome/static
        <Directory /home/pi/Dev/cfehome/static>
           Require all granted
         </Directory>

    <Directory /home/pi/Dev/cfehome/src/cfehome>
        <Files wsgi.py>
            Require all granted
        </Files>
    </Directory>

    WSGIDaemonProcess cfehome python-path=/home/pi/Dev/cfehome/src:/home/pi/Dev/cfehome/lib/python2.7/site-packages
    WSGIProcessGroup cfehome
    WSGIScriptAlias / /home/pi/Dev/cfehome/src/cfehome/wsgi.py


    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>

```
