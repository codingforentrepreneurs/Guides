# Heroku & Django

Launching a Django Project on Heroku.com.


1. Create Django project.
	A result would include:
	```
	src/
	src/manage.py
	src/myproject/
	src/myproject/settings.py

	```
2. Install [Heroku toolbelt](https://toolbelt.heroku.com/)

3. Migrate `settings.py` into a settings module.
	- Rename `settings.py` to `old_settings.py`; do not delete.
	- create python module (folder) `settings` in project's root configuration folder
	- Add 3 files to new `settings` folder:
		- `__init__.py`
		- `local.py`
		- `production.py`
	- You project should now resemble:

		```
		src/
		src/manage.py
		src/myproject/
		src/myproject/old_settings.py
		src/myproject/settings/__init__.py
		src/myproject/settings/local.py
		src/myproject/settings/production.py
		```

4. Add contents:

	Add following to `__init__.py`:
	```
	try:	
		from .local import *
	except:
		pass

	from .production import *
	```

	`local.py`
	Copy all data from `old_settings.py`

	`production.py`
	Copy all data from `old_settings.py`


5. Initialize a Git repo & add `.gitingore` file:

	In the root of your project do the following:
	- initialize git with: `git init`
	- create `.gitignore` file (notice it's just `.gitignore` you might need to use a code text editor to create this). Put this file where `manage.py` lives. Add the following into it:

	```
	#.gitignore
	yourproject/settings/local.py
	```


6. Add to / create `requirements.txt` file:
	```
	dj-database-url==0.4.0
	Django==1.9.7
	gunicorn==19.4.5
	psycopg2==2.6.1
	whitenoise==2.0.6
	```
	You may need to check the versions above but those are the essential.

7. Create `Procfile`:
	Simply named `Procfile` with no extension (like `.` something). Put this file where `manage.py` lives. Add the following:
	```
	web: gunicorn yourproject.wsgi 
	```

8. `production.py` Changes
	
	*leave local.py unchanged, that is for local testing only*
	```
	DEBUG = FALSE
	import dj_database_url
	DATABASES = {
		'default': dj_database_url.config()
	}

	SECURE_PROXY_SSL_HEADER = ('HTTP_X_FORWARDED_PROTO', 'https')
	```

9. Add/update project in git:
	```
	$ git status -u #local.py should not be in the results here
	$ git add --all
	$ git commit -m "Prepare for production"
	```

10. Create Heroku project & database

	```
	$ heroku create <yourprojectname>
	$ heroku addons:create heroku-postgresql:hobby-dev #add database
	$ heroku config:set DISABLE_COLLECTSTATIC=1 # to prevent needing static files setup now
	```
	**Note** `<yourprojectname>` should be changed. If ommitted, a project name, in heroku only, will be created for you.

11. Deploy to heroku
	```
	git push heroku master
	```

12. Make changes to your project? (Which you should be) make sure you do the following:

	1. Update requirements.txt as needed
	2. Update production.py as needed (don't assume it's works, compare against your local.py)
	3. Commit all changes:
	
		```
		git add --all
		git commit -m "Update changes"
		```
	4. Push to heroku:
		```
		git push heroku master
		```




#### Common Commands

`$ heroku restart`: If, for any reason, you need to restart your application. 

`$ heroku run bash`: runs the Linux bash on Heroku for your app

`$ heroku run python manage.py shell`: runs the Python shell on heroku

`$ heroku run python manage.py`: Allows your to run any django CLI command such as `heroku run python manage.py migate`

`$ heroku logs`: Get the logs for your application; great for if you see `Application Errors` when deploying or accessing your site.

`$ heroku open`: Opens your site/project.

`$ heroku ps:scale web=X worker=Y`:
	- replace `X` with the number of web dynos you need; the higher the number the greater the performance and cost. 
	- replace Y with the number of workers you need; the higher the number the greater the performance and cost.
	- More about scaling [here](https://devcenter.heroku.com/articles/scaling).



Subscribe on our [YouTube Channel](http://joincfe.com/youtube) and join us for more in-depth tutorials on [Django development](http://joincfe.com/enroll).


Cheers!


#### Organized by CodingForEntrepreneurs
