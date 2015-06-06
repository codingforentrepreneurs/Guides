# Django ImageField & Pillow
A basic reference guide to installing pillow on your local machine as well as a worst-case scenario fallback. 

## Virtual Environment 

Make sure you are working in a virtual environment to ensure software package continuity. 

If you are not working in one, install and make one with:

```
$ pip install virtualenv
$ virtualenv venv && cd venv
```

####Activate the virtual environment.
On Mac/Linux:
```
$ source bin/activate
```
On Windows:
```
> .\Scripts\activate
```

## Install Python Image Library (Pillow)
This provides image validation (as well as many other image-related python activities) for Django's [ImageField()](https://docs.djangoproject.com/en/dev/ref/models/fields/#imagefield)
```
$ pip install pillow
```

## If installation fails...
You might see something like:

```
error: command 'cc' failed with exit status 1

----------------------------------------
Cleaning up...

Command /Users/user/Desktop/venv/bin/python -c "import setuptools, tokenize;__file__='/Users/jmitch/Desktop/venv/build/pillow/setup.py';exec(compile(getattr(tokenize, 'open', open)(__file__).read().replace('\r\n', '\n'), __file__, 'exec'))" install --record /var/folders/pt/3tv_v7lx18xft_fwzsl2l4880000gn/T/pip-F89xZT-record/install-record.txt --single-version-externally-managed --compile --install-headers /Users/user/Desktop/venv/include/site/python2.7 failed with error code 1 in /Users/user/Desktop/venv/build/pillow
Storing debug log for failure in /Users/user/.pip/pip.log
```
That means pillow was not installed correctly. Below are a few suggestions for troubleshooting (aka fixing) this issue.

### Mac Users Troubleshooting guide

##### [Download & Install Xcode](https://developer.apple.com/xcode/downloads/)

##### [Create developer account](https://developer.apple.com/register/index.action) _Free at time of writing_

**Download Command Line Tools for Xcode**. Search "command line tools" **[here](https://developer.apple.com/downloads/index.action)**. 
Download the latest for your operating system (Mavericks or Yosemite)

After XCode and command line tools are installed, open terminal and run:
```
$ pip install pillow
```

_If installation still fails, continue to next section._

### Try HomeBrew

Check Homebrew is installed
```
$which brew
/usr/local/bin/brew #should be returned
```

If Homebrew is not installed, visit [http://brew.sh](http://brew.sh/) to install.


__In Terminal__
```
$ brew update
$ brew tap Homebrew/python
$ brew install pillow
```



_If homebrew installation fails, try:_

```
$ export CFLAGS=-Qunused-arguments
$ export CPPFLAGS=-Qunused-arguments
$ pip install pillow
```

_Lastly try:_
```
$ ARCHFLAGS=-Wno-error=unused-command-line-argument-hard-error-in-future pip install pillow
```

### Linux Users Troubleshooting guide

Linux users if you get any error something like this 
```
error: command 'gcc' failed with exit status 1 
```
Install the following packages in terminal
```
$sudo apt-get update 
$sudo apt-get install python-dev
$sudo apt-get install libevent-dev
```
### Windows Users Troubleshooting guide
if you get error some thing like this 
```
unable to find vcvarsall.bat
```
Check whether you have installed Microsoft Visual C++ 2008 or later

Also you can install pillow using easy_install
```
C:\>easy_install pillow
```



## Worst-Case Fallback: If all else Fails
Use FileField() instead of ImageField() as your model field. Example:
```python
image = models.FileField(upload_to='images/')
```

Instead of 
```python
image = models.ImageField(upload_to='images/')
```

The main advantage of "ImageField" is that checks if the file uploaded is, in fact, an **actual image** while "FileField" does not. Read about "ImageField" in the Django [documentation here](https://docs.djangoproject.com/en/dev/ref/models/fields/#imagefield).

Cheers!

#### Organized by CodingForEntrepreneurs