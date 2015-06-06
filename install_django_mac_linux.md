# Install Django & Virtualenv on Mac OS X / Linux with PIP


*Django* is a popular web development framework written in Python. 
*Virtualenv*, or Virtual Environments, is a tool to keep the dependencies required by different projects in separate places, by creating virtual Python environments for them. Basically, if your project has different software versions (and it will) virtualenv keep them nice and safe.
*PIP*, or Python Package Installer, allows you to install all types of python-related software (and code) include Django, Virtual environments (virtualenv), Python Requests, and more.

## [Setup videos](http://joincfe.com/projects#setup)

			
####  Below is a basic setup guide for installing Django/Virtualenv on a Mac. 

When you see code like the following:

```
ls
```
That means you should type it inside the application we mention below. Watching the free [setup videos](http://joincfe.com/projects#setup) will make this a lot easier as well.


1. Open Terminal (Applications > Utilities > Terminal)
2. Enter the following commands:
NOTE: The command `sudo` will require an admin password. The same password you use to install other programs. Typing will be hidden
	
	1. Install Pip. (Python Package Installer)
		```
		sudo easy_install pip
		```
	2. Install virtualenv:
		```
		sudo pip install virtualenv
		```

	3. Navigate to where you want to store your code. 
		You have two options:
		1. Easy (on Desktop):
			```
			cd ~/Desktop
			``

		2. More Specific (ignoring the ```cd ~/Desktop``` command):
			```
			mkdir Development
			cd Development
			```
		Typical location is in a folder/directory called "Development" and this

	4. Create a new virtualenv:
		```
		virtualenv yourenv
		``` 
		The name "yourenv" above is arbitarry. You can name it as you like.
	5. Activate virtualenv:
		```
		source bin/activate
		```
		The result in Terminal should be something like:
		```
		(yourenv) Justins-iMac-2:~ jmitch$
		``` 

	6. Install Django:
		```
		pip install django==1.8.2
		```
		NOTE: django==1.8.2 is for version 1.8.2. If you need a differnet version, replace those numbers accordingly. Such as django==1.6.8

	7. Happy Coding with Django.


Subscribe on our [YouTube Channel](http://joincfe.com/youtube)
Join us for more in-depth tutorials on [Django development](http://joincfe.com/enroll).


Cheers!


#### Organized by CodingForEntrepreneurs