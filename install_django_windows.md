# Install Python & Django on Windows using PIP (Python Package Installer)
The python package installer allows you to install all types of python-related software (and code) include Django, Virtual environments (virtualenv), Python Requests, and more.

## Video: [Installation Video Series](https://codingforentrepreneurs.com/projects/start-with-windows/)

### Download Python 2.7.X
1. Download based on your system. 64-bit likely works for you. 
	1. Get [Latest Python 2 Release - Python 2.7.8](https://www.python.org/downloads/release/python-278/) **Python 2.7 is preferred for Coding for Entrepreneurs tutorials and a large number of Python Packages (including many Django Packages) are still in Pyton 2.7
2. Run Standard Installation
3. Add Environment Variables to your PATH. In `Command Prompt` type the following:
	```set PYTHONPATH=%PYTHONPATH%;C:\Python27;C:\Python27\python.exe;C:Python\27\Lib\site-packages;C;\Python27\Lib\site-packages\django\bin;```
4. Open `Command Prompt` and type `python` if you see Python-related items and the bottom line being `>>>` then it was successfully installed.

### Install Pip

1. Save the "get_pip.py" file to your Desktop. You can find the file [here](http://pip.readthedocs.org/en/latest/installing.html).
2. Open Command Prompt and do:
	 `> cd Desktop`
	 `> python get_pip.py`

33. Now "pip" should work system wide. Command like `pip install virtualenv` and `pip freeze` will work


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
	1. `> cd Desktop`
	2. `> python ez_setup.py`
	3. `> easy_install pip`

3. Now "pip" should work system wide. Command like `pip install virtualenv` and `pip freeze` will work


You're now ready to start using Python Packages like Django!



Cheers!


#### Organized by CodingForEntrepreneurs