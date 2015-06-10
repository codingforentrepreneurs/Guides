# Install Python & Django on Windows using PIP (Python Package Installer)
The python package installer allows you to install all types of python-related software (and code) include Django, Virtual environments (virtualenv), Python Requests, and more.

## Video: [Installation Video Series](https://codingforentrepreneurs.com/projects/start-with-windows/)

### Download Python 2.7.X
1. Download based on your system. 64-bit likely works for you. 
	1. Get [Latest Python 2 Release - Python 2.7.8](https://www.python.org/downloads/release/python-278/) **Python 2.7 is preferred for Coding for Entrepreneurs tutorials and a large number of Python Packages (including many Django Packages) are still in Python 2.7
2. Run Standard Installation
3. Now that Python is installed. We need to make Command Prompt work properly with Python. Add Environment Variables on Windows 8 (will be similiar for Windows 7 and XP)
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

C:\Python27;C:\Python27\python.exe;C:Python\27\Lib\site-packages;C;\Python27\Lib\site-packages\django\bin;c:\Python27\Scripts;


```

If something was already in `variable value` the end result will look something like:

```

C:\Windows\System32;C:\Python27;C:\Python27\python.exe;C:Python\27\Lib\site-packages;C;\Python27\Lib\site-packages\django\bin\;c:\Python27\Scripts;

```



4. Open a new `Command Prompt` window and type `python` if you see something like:
```
Python 2.7.8 (default, Nov 13 2014, 13:18:45)
>>> 
``` 

You have `Python` successfully installed. You can now exit python:

```
>>> exit()
```

### Install Pip

1. Save the "get-pip.py" file to your Desktop. You can find the file [here](http://pip.readthedocs.org/en/latest/installing.html).
2. Open Command Prompt and do:
```
> cd Desktop
> python get-pip.py
```

3. Now "pip" should work system wide. The following Commands will now work:
```
> pip install virtualenv
> pip freeze
> pip install Django==1.8.2
```





### Still having issues? Read on.

- If you can't get virtualenv working, just work outside of it. Just remember that different software versions do not always work well. Revisit installing virtualenv once you have a better grasp of Django.

- You may need to open a new command prompt window to work correctly.

- Having trouble installing PIP? Let's try using setuptools. 

This assumes you installed Python version 2.7 successfully. To test, open command prompt and type:

```
> python	 
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
> pip install Django==1.7.1
```


You're now ready to start using Python Packages like Django!



Cheers!


#### Organized by CodingForEntrepreneurs