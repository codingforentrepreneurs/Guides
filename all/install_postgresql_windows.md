#Install PostgreSQL on Windows
A simple guide on how to install PostgreSQL on your local Windows machine. 

**NOTE**: This guide has not been thoroughly tested. If you find improvements, please submit them to us.

### Download & Install

1. Visit the PostgreSQL Windows download site: [here](http://www.postgresql.org/download/windows/)
2. [Download](http://www.enterprisedb.com/products-services-training/pgdownload#windows) the installer from EnterpriseDB for all supported versions.
3. Select the the most recent Version 9.4.X (it's currently 9.4.5) and your Windows system:
	32-bit systems select "Win x86-32"
	64-bit systems select "Win x86-64"
4. After download completes, run the installer and select all default options.


### Open a Command Prompt Window

Now, test `postgresql` with:

	> createdb
	> psql

You should see something like:

	psql (9.4.5)
	Type "help" for help.

	jmitch=#

Where `jmitch` would be your username.

### Django Docs
As an alternative, you can read [Django Docs](https://docs.djangoproject.com/en/1.8/ref/contrib/gis/install/#postgresql) for information on getting `postgresql` installed.

Now you have PostgreSQL installed.