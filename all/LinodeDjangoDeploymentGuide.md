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


### Setup your Debian System for Django + Apache [here](./Debian_Install_Django_Apache2.md)

