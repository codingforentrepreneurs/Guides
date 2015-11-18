# Prepare PostgreSQL for Django
This assumes you have `postgresql` installed on your machine. Check out our [database installation guides](https://github.com/codingforentrepreneurs/Guides#database-installation) to install it on your computer.



### Open Terminal/Command prompt

Open `postgresql`:

```
$ psql

```

Resulting in something like:

```
psql (9.4.5)
Type "help" for help.

jmitch=#
```
Where `jmitch` would be your username.


Create database & new database user:

```
jmitch=# CREATE DATABASE newproject;
jmitch=# CREATE USER newprojectadminuser WITH PASSWORD 'adminpassword';
jmitch=# ALTER ROLE newprojectadminuser SET client_encoding TO 'utf8';
jmitch=# ALTER ROLE newprojectadminuser SET default_transaction_isolation TO 'read committed';
jmitch=# ALTER ROLE newprojectadminuser SET timezone TO 'UTC';
jmitch=# GRANT ALL PRIVILEGES ON DATABASE newproject TO newprojectadminuser;
```


Quit:

	jmitch=# \q



### Install & Test with Django
	

Install/upgrade virtualenv

	sudo pip install virtualenv --upgrade
	cd ~/Desktop
	mkdir newenv
	cd newenv
	virtualenv .
	source bin/activate
	pip install django==1.8.6 psycopg2
	django-admin.py startproject newproject
	cd newproject


Update your `Django` `DATABASES` settings (`settings.py`) to:

	DATABASES = {
	    'default': {
	        'ENGINE': 'django.db.backends.postgresql_psycopg2',
	        'NAME': 'newproject',
	        'USER': 'newprojectadminuser',
	        'PASSWORD': 'adminpassword',
	        'HOST': 'localhost',
	        'PORT': '',
	    }
	}



### PostgreSQL Commands (Basics)

Open `postgresql`

	$ psql


Open `postgresql` With User & Database:


	$ psql -U newprojectadminuser newproject



List all Databases:

	jmitch=# \list


Select Database:

	jmitch=# \connect newproject


Delete (drop) Database from `postgresql`:

	jmitch=# DROP DATABASE newproject;



Delete (drop) Database from Command line:

	$ dropdb newproject


Connect & List all tables:

	jmitch=# \connect newproject
	newproject=# \dt


Drop a table

	jmitch=# \connect newproject
	newproject=# \dt
	newproject=# DROP TABLE auth_group CASCADE;
