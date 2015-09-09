# Reactivate Virtual Environment
Did you close out your terminal or command prompt and forget how to get back into the project? Check out this guide to get you back.



## Assuming you followed our [setup videos](https://codingforentrepreneurs.com/projects/#setup)... 

You will go to the desktop and then to your virtualenv folder

On Mac/Linux Terminal:
```
Last login: Thu Jul  3 17:34:42 on ttys000
$ pwd
/Users/yourusername 
$ cd Desktop
$ ls
$ otherfolders otherfiles.png venv
$ cd venv 
```


On Windows Command Prompt:
```
> dir
\User\yourusername
> cd Desktop
> cd venv
```

*venv denotes a virtual environment*


You would now be in *venv* virtual environment. To reactivate just:

On Mac/Linux Terminal:
```
$ source bin/activate
```

On Windows Command Prompt:
```
> .\Scripts\activate
```


## Assuming you didn't follow our [setup videos](https://codingforentrepreneurs.com/projects/#setup)...
You need to find the direct location to your virtual environment folder. Once you find it, you can change into it's directory like this:

```
$ cd ~/path/to/your/virtualenv/
```
or
```
> cd \path\to\your\virtualenv\
```

Once you are in, you can activate it just like above.


Cheers!


#### Organized by CodingForEntrepreneurs