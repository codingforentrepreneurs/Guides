# Digital Ocean & Django Deployment Guide

A installation guide for getting Django setup on Digital Ocean

----------



### Digital Ocean Setup
1. Sign up for a Digital Ocean account [Affiliate](https://kirr.co/l8v1n1) | [Non-Affiliate](https://www.digitalocean.com/)

2. Login

3. Create Droplet

4. Under `Distributions` select `Debian` version `8.6x64` or newer.

5. Choose a size in your budget

6. Choose a `datacenter region` likely one close to your target audience

7. Leave out SSH Key unless you know how to create one.

8. Finalize and create: 1 Droplet is fine

9. Let Droplet finish initializing

10. Check email for the following (unless you setup an SSH Key on step #7):

```
Droplet Name: <droplet_name>
IP Address: <ip_address>
Username: <username>
Password: <password>
``` 


#### Digital Ocean & Terminal/PuTTY

1. In terminal([PuTTY](http://www.putty.org/) if on Windows) and enter:
     ```
     # format
     ssh root@<ip_address>

     #example:
     ssh root@104.131.146.34
     ```

2. You should see a message like:
```
The authenticity of host '104.131.146.34 (104.131.146.34)' can't be established.
ECDSA key fingerprint is SHA256:Dg4o2zcwBMMx72IJEgdhJm/iDWtoQzWVmSuRV8B4db4.
Are you sure you want to continue connecting (yes/no)?   
```
Type `yes` then hit `enter`

3. It should ask for your `<password>`, we recevied in our email (unless you setup an SSH Key)

4. It will ask for your `<password>` again so you can reset it. Set a `<new_password>` and then confirm it. From now on, use this `<new_password>` with `ssh root@<ip_address>` to acccess your `Droplet`.
 


### Setup Local Django Project [here](./Create_a_Local_Django_Project.md)

### Setup your Debian System for Django + Apache [here](./Debian_Install_Django_Apache2.md)

### SSH & FTP Local Django Project to Digital Ocean

1. Open an FTP Client (like Transmit or Cyberduck)

2. SFTP into your `<ip_address>` using `root` and your `password`

3. Navigate to `/var/www/venv`

4. Replace `src` with your `src`

5. Navigate to `src/<your-project>/settings/` and remove `local.py`

6. Open Terminal/PuTTY

7. SSH into your `<ip_address>` like `ssh root@<ip_address>` 

8. Update Apache2 to your project's name/settings if needed.

9. Run the following:
     ```
     cd /var/www/venv/
     source bin/activate
     cd src
     python manage.py makemigrations
     python manage.py migrate
     ```
10. Restart apache `sudo service apache2 restart`

11. Navigate to your `<ip_address>` (or domain name) in your browser.
