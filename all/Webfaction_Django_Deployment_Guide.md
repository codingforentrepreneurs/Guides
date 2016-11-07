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

