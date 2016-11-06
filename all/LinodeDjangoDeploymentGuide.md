# Linode & Django Deployment Guide

A installation guide for getting Django setup on Linode's VPS service

----------



### Linode Setup
1. Sign up for a Linode account [Affiliate](http://kirr.co/wnlkp6/) | [Non-Affiliate](http://www.incode.com)

2. Select [Linode Plan](https://manager.linode.com/linodes/add) such as Linode 2048

3. Navigate to [Linodes](https://manager.linode.com/linodes/index), select your newly created Linode something like `linode2449295`

4. Select `Deploy an Image`, use `Debian 8`.

5. Set a `<root password>`

6. Select `Boot`; Confirm on pop-up

7. Select `Remote Access`

8. Copy the `SSH Access` which is something like `ssh root@45.79.183.218`; 
   *note: the `45.79.183.218` is your server's IP Address.*

9. In terminal (or [PuTTY](http://www.putty.org/) if on Windows) paste `ssh root@45.79.183.218`

10. You should see an message like:
```
The authenticity of host '45.79.183.218 (45.79.183.218)' can't be established.
ECDSA key fingerprint is SHA256:3Zz7ct9+9Y5tqCTQU2l/1sjLGjyqGUVr4kCgJSvIb0Y.
Are you sure you want to continue connecting (yes/no)?  
```
Type `yes` then hit `enter`

11. It should ask for your `<root password>`, use the one set on Step 5


### Setup your Debian System for Django + Apache [here](./all/DebianInstallDjango&Apache2.md)

### Install Python Tools, Django, Apache2, and Mod_WSGI
1. Install Python Tools, Apache2, and Mod_WSGI

    ```
    sudo apt-get update

    sudo apt-get upgrade

    sudo apt-get install apache2

    sudo apt-get install python-pip python-virtualenv python-setuptools python-dev build-essential

    sudo apt-get install libapache2-mod-wsgi-py3

    sudo apt-get install libapache2-mod-wsgi # if using Python2
    ```

2. Start Virtualenv & Django Project

    ```
    sudo pip install virtualenv 

    cd /var/www

    mkdir venv && cd venv

    virtualenv -p python3 .

    source bin/activate

    python --version #should return Python 3.4

    pip install django==1.10.3

    mkdir src && cd src

    django-admin.py startproject cfehome . 
    ```

3. Setup Static & Media Root directories.
    ```
    cd /var/www
    
    mkdir static-root && mkdir media-root
    ```

4. Open `sudo nano /etc/apache2/sites-available/000-default.conf`


5. Change Apache2 configuration
    ```
    <VirtualHost *:80>
    ServerName localhost
    ServerAdmin webmaster@localhost

    Alias /static /var/www/static-root
    <Directory /var/www/static-root>
       Require all granted
     </Directory>

    Alias /media /var/www/media-root
    <Directory /var/www/media-root>
       Require all granted
    </Directory>

    <Directory /var/www/venv/src/cfehome>
        <Files wsgi.py>
            Require all granted
        </Files>
    </Directory>

    WSGIDaemonProcess cfehome python-path=/var/www/venv/src/:/var/www/venv/lib/python3.4/site-packages
    WSGIProcessGroup cfehome
    WSGIScriptAlias / /var/www/venv/src/cfehome/wsgi.py


    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined

    </VirtualHost>
    ```


6. Add User Permissions (to modify sqlite3 Database)
    ```
    sudo adduser $USER www-data
    sudo chown www-data:www-data /var/www/venv/src    
    sudo chown www-data:www-data /var/www/venv/src/db.sqlite3
    sudo chmod -R 775 /var/www/venv/
    ```

7. Start, Stop, Restart Apache2
    ```
    # Restart in two different ways:
    sudo apachectl restart
    sudo service apache2 restart


    # Start Apache in two different ways:
    sudo apachectl start
    sudo service apache2 start

    # Stop Apache in two different ways:
    sudo apachectl stop
    sudo service apache2 stop
    ```

8. Setup Domain Name DNS records:
    Add your server's ip_address such as `45.79.183.218` as a `A` record for your domain name. Such as:

    | Type          | Host                |  Answer        |  TTL  |
    | ------------- |:-------------------:|:--------------:|:-----:|
    | A             | www.yourdomain.com  | 45.79.183.218  |  300  |
    | A             | blog.yourdomain.com | 45.79.183.218  |  300  |


9. Add Any/All Hosts to Django Settings:
    ```
    ALLOWED_HOSTS = ['45.79.183.218', 'www.yourdomain.com', 'blog.yourdomain.com']
    ```
    
    Add Static + Media Settings
    ```
    STATIC_URL = '/static/'
    STATIC_ROOT = '/var/www/static-root/'
    MEDIA_URL = '/media/'
    MEDIA_ROOT = '/var/www/media-root/'
    ```

10. Restart Apache (see Step 7)

