# WebFaction & Django Deployment Guide

A installation guide for getting Django setup on WebFaction

----------

### Setup & Login
1. Sign Up for an account on WebFaction: [Affiliate with 2 months free](http://kirr.co/snbpyg/) | [Non-Affiliate](http://www.kirr.co/a6vcnl/)

2. Login

3. Click `Domains/Websites` > `Applications` > `Add New Application`

4. Create a Django project with the following:
    ```
    Name: "cfehome" # or whatever you call your project below.
    App Category:  Django
    App type: Django 1.X.Y (mod_wsgi 4.5.X/Python 3.5)
    ```
    **NOTE** The `Django` application version we are going to use is `1.10.2`; select your version and replace X & Y with the version you're working with.

    Hit `Save`

5. Create a Static Only folder for STATIC_ROOT
    1. Click `Domains/Websites` > `Applications` > `Add New Application`

    2. Create a `Static` Application with the following:
        ```
        Name: "cfehome_static_root"
        App Category:  Static
        App type: Static only (no .htaccess)
        ```

        Hit `Save`


6. Create a Static Only folder for MEDIA_ROOT
    1. Click `Domains/Websites` > `Applications` > `Add New Application`

    2. Create a `Static` Application with the following:
        ```
        Name: "cfehome_media_root" 
        App Category:  Static
        App type: Static only (no .htaccess)
        ```

        Hit `Save`


7. Create Website:
    1. Click `Domains/Websites` > `Websites` > `Add New Website`

    2. Create a website with the following:

        ```
        Name: cfehome_website
        Security: Normal website (http)
        Status: Enabled
        Domains: <yourusername>.webfactional.com

    3. In Contents, click `Add Application` > `Reuse An Existing Application` select your Django Project `cfehome`. Keep url blank

    4. In Contents, click `Add Application` > `Reuse An Existing Application` select your Static Root `cfehome_static_root`. Add `static` to the url

    5. In Contents, click `Add Application` > `Reuse An Existing Application` select your Media Root `cfehome_media_root`. Add `media` to the url


### SSH into WebFaction

1. Navigate to [https://my.webfaction.com/](https://my.webfaction.com/) & Login (if needed) 

2. In the `Web Server` section, note the `web374.webfaction.com` portion.

3. Open Terminal (or [PuTTY](http://www.putty.org/) on Windows)

4. Run `ssh <username>@<server-id>.webfaction.com` like `ssh cfedeploy@web374.webfaction.com`

5. If first time doing `ssh` into your server, you should see:
    ```
    The authenticity of host 'web374.webfaction.com (2607:f0d0:1104:4:16::2)' can't be established.
    RSA key fingerprint is SHA256:Dc9MghuhqWF1LoCzf6S31KbVSkLphayrrD7KmYHREKw.
    Are you sure you want to continue connecting (yes/no)? 
    ```
    Say Yes

6. Navigate to your Django project:
    Login process returns something like:
    ```
    $ ssh cfedeploy@web374.webfaction.com
    Last login: Wed May  26 02:42:36 2016 from 123.09.64.12
    [cfedeploy@web374 ~]$ ls
    bin  lib  logs  webapps
    ```
    Now navigate to your django project

    ```
    [cfedeploy@web374 ~]$ cd webapps
    [cfedeploy@web374 webapps]$ ls
    cfehome  cfehome_media_root cfehome_static_root htdocs
    [cfedeploy@web374 webapps]$ cd cfehome
    [cfedeploy@web374 cfehome]$ ls
    apache2  bin  lib  myproject
    ```

    Remove pre-installed Django project listed as `myproject`:

    ```
    rm -rf myproject
    ```

### Create a Django Local Project following [this guide](./Create_a_Local_Django_Project.md)

### FTP And Deploy Django Project
1. Open an FTP Client (like Transmit or Cyberduck)

2. SFTP into your Webfaction Account

3. Navigate to your webapp in `/webapps/cfehome`

4. Download `apache2/conf/httpd.conf`, update the settings as:
    ```
    WSGIDaemonProcess cfehome processes=2 threads=12 python-path=/home/cfedeploy/webapps/cfehome:/home/cfedeploy/webapps/cfehome/src:/home/cfedeploy/webapps/cfehome/lib/python3.5
    WSGIProcessGroup cfehome
    WSGIRestrictEmbedded On
    WSGILazyInitialization On
    WSGIScriptAlias / /home/cfedeploy/webapps/cfehome/src/cfehome/wsgi.py
    ```
5. Navigate back to `/webapps/cfehome`

6. Drag Your Local project, we call `cfehome` through CyberDuck/Transmit to `/webapps/cfehome`

7. Update `production.py` with the following settings:
    ```
    ALLOWED_HOSTS = ['cfedeploy.webfaction.com']
    STATIC_URL = '/static/'
    STATICFILES_DIRS = (
            os.path.join(BASE_DIR, "static"),
    )

    STATIC_ROOT = "/webapps/cfehome_static_root/"

    MEDIA_ROOT = "/webapps/cfehome_media_root/"
    ```

8. Setup Domain Name Nameservers to Webfaction and add domain to Webfaction:

    | Nameserver          | 
    | ------------------- |
    | ns1.webfaction.com  |
    | ns2.webfaction.com  | 
    | ns3.webfaction.com  | 
    | ns4.webfaction.com  | 

9. Add Domain to `ALLOWED_HOSTS` in `production.py`:
    ```
    ALLOWED_HOSTS = ['cfedeploy.webfaction.com', 'www.spormicro.com']
    ```

10. Upload changed files (such as `httpd.conf` and `production.py`) and ensure `local.py` is not in the project.

11. SSH via Terminal/PuTTY to Webfaction Project and Restart Apache:
    ```
    cd webapps/cfehome
    ./Apache2/bin/restart
    ```
12. Set `Python Path` inside of your app with `PYTHONPATH=$PYTHONPATH:$PWD/lib/python`

13. Collectstatic:
    ```
    python3.5 manage.py collectstatic
    ```

14. Any Django commands should now work using `python3.5` first:
    ```
    python3.5 manage.py migrate
    python3.5 manage.py createsuperuser
    ```
All set!
