# Install Python & Django on Windows using PIP (Python Package Installer)
The python package installer allows you to install all types of python-related software (and code) include Django, Virtual environments (virtualenv), Python Requests, and more.

## Video: [Installation Video Series](https://codingforentrepreneurs.com/projects/start-with-windows/)

### Download Python 2.7.X
1. Download based on your system. 64-bit likely works for you. 
	1. Get [Latest Python 2 Release - Python 2.7.8](https://www.python.org/downloads/release/python-278/) **Python 2.7 is preferred for Coding for Entrepreneurs tutorials and a large number of Python Packages (including many Django Packages) are still in Pyton 2.7
2. Run Standard Installation
3. Add Environment Variables to your PATH. In `Command Prompt` type the following:
```
set PYTHONPATH=%PYTHONPATH%;C:\Python27;C:\Python27\python.exe;C:Python\27\Lib\site-packages;C;\Python27\Lib\site-packages\django\bin;
```
4. Open `Command Prompt` and type `python` if you see something like:
```
Python 2.7.8 (default, Nov 13 2014, 13:18:45)
>>> 
``` 

You have `Python` successfully installed. You can now exit python:

```
>>> exit()
```

### Install Pip

1. Save the "get_pip.py" file to your Desktop. You can find the file [here](http://pip.readthedocs.org/en/latest/installing.html).
2. Open Command Prompt and do:
```
> cd Desktop
> python get_pip.py
```

3. Now "pip" should work system wide. The following Commands will now work:
```
> pip install virtualenv
> pip freeze
> pip install Django==1.7.1
```


Still having issues? Read on.

### Another Pip Installation Method using setuptools. 
This assumes you installed Python version 2.7 successfully. To test, open command prompt and type:

```
> python	 
>>> exit() 
```
If you can do the above, you have python installed on your computer. 

## Having trouble installing PIP? 
Let's try another method:

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