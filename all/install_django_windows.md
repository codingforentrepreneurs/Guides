### Install Python & Django on Windows using PIP (Python Package Installer)
The python package installer allows you to install all types of python-related software (and code) include Django, Virtual environments (virtualenv), Python Requests, and more.

#### Video: [Installation Video Series](https://codingforentrepreneurs.com/projects/start-with-windows/)

#### Download Python 3.6.X
1. Download The [Latest Python 3 Release](https://www.python.org/downloads/release/python-360/). It's currently Python 3.6.0 and the download link is listed under *files* and choose the appropriate one for your system. 64-bit likely works for you. *Note: Python 3.6 is preferred for Coding for Entrepreneurs tutorials. (We have upgraded from version 2.7)*
2. Run Standard Installation Process
3. Add Environment Variables to setup up Command Prompt to work with Python. This is where we'll run the bulk of our commands. (Works on Windows XP, 7, 8, 10 & Up)
 	1. Open `Control Panel`
 	2. Select `System and Security`
 	3. Select `System` 
 	4. Select `Advanced System Settings`
 	5. Select `Advanced` Tab
 	6. Select `Environment Variables`
 	7. Under "User variables for <username>" select the variable `PATH` then hit `edit`
 	8. If `PATH` is not a current user variable, select `new` and set `Variable Name` as `PATH`
 	9. Add the following to the end of whatever is written in the `Variable Value` (if anything):
	```
	C:\Python36;C:\Python36\python.exe;C:\Python\36\Lib\site-packages;C:\Python36\Lib\site-packages\django\bin;C:\Python36\Scripts;
	```
	If something was already in `Variable Value` the end result will look something like:
	```
	C:\Windows\System32;C:\Python36;C:\Python36\python.exe;C:\Python\36\Lib\site-packages;C:\Python36\Lib\site-packages\django\bin\;C:\Python36\Scripts;
	```

4. Open a new `Command Prompt` window and type `python` if you see something like:
	```
	Python 3.6.0 (default, Feb 13 2017, 13:18:45)
	>>> 
	``` 

	You have `Python` successfully installed. You can now exit python:

	```
	>>> exit()
	```

### Install Pip
Pip is the Python Package Installer which allows you to install things like Django, Virtualenv, Requests, and more to your local computer. A must-have for developing with Python.

1. Save the "get-pip.py" file to your Desktop. You can find the file [here](https://bootstrap.pypa.io/get-pip.py) or at the [docs](http://pip.readthedocs.org/).
2. Open Command Prompt and do:
	```
	C:\ > cd Desktop
	C:\ > python get-pip.py
	```

3. Now "pip" should work system wide. The following Commands will now work:
	```
	C:\ > pip install virtualenv
	C:\ > pip freeze
	C:\ > pip install Django==1.10.5
	```



#### Still having issues? Read on.

- If you can't get virtualenv working, just work outside of it. Just remember that different software versions do not always work well. Revisit installing virtualenv once you have a better grasp of Django.

- You may need to open a new command prompt window to work correctly.

- Having trouble installing PIP? Let's try using setuptools. 

This assumes you installed Python version 3.6 successfully. To test, open command prompt and type:

```
C: \ > python	 
>>> exit() 
```

If you can do the above, you have python installed on your computer. 


1. Save the ["ez_setup.py" file](https://bootstrap.pypa.io/ez_setup.py) to your desktop. 

2. Open Command Prompt and do:
```
> cd Desktop
> python ez_setup.py
> easy_install pip
```

3. Now "pip" should work system wide. The following Commands will now work:
```
> pip install virtualenv
> pip freeze
> pip install Django==1.10.5
```


You're now ready to start using Python Packages like Django!



Cheers!


#### Organized by CodingForEntrepreneurs
