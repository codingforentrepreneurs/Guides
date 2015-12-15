# Elastic Beanstalk Django

Launching a Django Project on Amazon Web Services (AWS) Elastic Beanstalk.



1. Setup Virtual Environment, GIT, & Django.
	**Create Virtualenv**
	```
	cd ~/Desktop
	virtualenv awsbean && cd awsbean
	```

	**Activate Virtualenv** 

	Mac/ Linux : `source bin/activate`

	Windows: `.\Scripts\activate`

	**Initialize Git (need to [install it](https://git-scm.com/book/en/v2/Getting-Started-Installing-Git)?) inside of your `virtualenv`.**
	```
	git init 
	```

	**Create gitignore (Mac/Linux)**

	```
	touch .gitignore
	open .gitignore
	```

	**Create gitignore (Windows)**
	1. Download and Install  [Sublime Text](http://www.sublimetext.com/) -- Free version works fine. Or any other code text editor.
	2. Open `Sublime Text` (or your code text editor)
	3. `File` > `New File`
	4. `File` > `Save`
	5. Save the file as `.gitignore` (not the `.` prior.) into your newly created virtualenv


	**Add & Save the following to your newly created `.gitignore` file:**

	```
	bin/
	include/
	lib/
	*.py[cod]
	*.sqlite3
	pip-selfcheck.json
	```

	**Install Django & Start Project:**

	```
	pip install django==1.8.7

	django-admin.py startproject awsbean
	```


2. **Install [AWS Command Line Interface](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb-cli3-install.html)**:
	
	**Ensure virtualenv is activated**
	```
	cd /path/to/root/of/your/virtualenv/
	source bin/activate # if Mac/Linux
	.\Scripts\activate * if Windows
	```
	

	**Install AWS CLI**
	```
	pip install awsebcli
	```
		
	__Test installation__
	
	```
	eb --version
	```
	
	**Returns** something like 
	```
	EB CLI 3.6.1 (Python 2.7.9)
	```

3. **Git Commit**
	```
	git add .
	git commit -m "first commit"
	```

4. **Create AWS User Credentials**
	
	1. Navigate to [IAM Users](https://console.aws.amazon.com/iam/home?#users)
	
	2. Select `Create New Users`
	
	3. Enter `awsbean` as a username (or whatever you prefer)
	
	4. Ensure `Generate an access key for each user` is **selected**.
	
	5. Select `Download credentials` and keep them safe. 
	
	6. Open the `credentials.csv` file that was just downloaded/created 

	7. Note the `Access Key Id` and `Secret Access Key` as they are needed for a future step. These will be referred to as `<your_access_key_id>` and `<your_secret_access_key>`




5. **Create Elastic Beanstalk Application via Command Line (aka Terminal/Command Prompt)**
	** Ensure virtualenv is activated **
	```
	cd /path/to/root/of/your/virtualenv/
	source bin/activate # if Mac/Linux
	.\Scripts\activate * if Windows
	```
	Initialize EB:

	```
	eb init 
	```

	This will respond with a few prompts you need to answer. Here's what we did:
	```
		Select a default region
		1) us-east-1 : US East (N. Virginia)
		2) us-west-1 : US West (N. California)
		3) us-west-2 : US West (Oregon)
		4) eu-west-1 : EU (Ireland)
		5) eu-central-1 : EU (Frankfurt)
		6) ap-southeast-1 : Asia Pacific (Singapore)
		7) ap-southeast-2 : Asia Pacific (Sydney)
		8) ap-northeast-1 : Asia Pacific (Tokyo)
		9) sa-east-1 : South America (Sao Paulo)
		10) cn-north-1 : China (Beijing)
		(default is 3): 3                # this is our answer

		You have not yet set up your credentials or your credentials are incorrect
		You must provide your credentials.
		(aws-access-id): <your_access_key_id>
		(aws-secret-key): <your_secret_access_key>

		Select an application to use
		1) [ Create new Application ]
		(default is 1): 1                # We created a new one

		Enter Application Name
		(default is "awsbean"):           # We pressed enter to use the default
		Application awsbean has been created.

		Select a platform.
		1) Node.js
		2) PHP
		3) Python
		4) Ruby
		5) Tomcat
		6) IIS
		7) Docker
		8) Multi-container Docker
		9) GlassFish
		10) Go
		11) Java
		(default is 1): 3                  # Select 3 for Python.

		Select a platform version.
		1) Python 3.4
		2) Python
		3) Python 2.7
		4) Python 3.4 (Preconfigured - Docker)
		(default is 1): 3					# Select 3 for 2.7 if that is what you use locally
		Do you want to set up SSH for your instances?
		(y/n): y                            # Optional, not needed at this point.

		Select a keypair.
		1) aws-eb
		2) aws-eb2
		3) [ Create new KeyPair ]           # If you said yes to SSH, this is required.
	```

	**Create Elastic Beanstalk with Database Option** 
	```
	eb create -db 
	```
	The `-db` option creates a `MySQL` database for us by default which makes setup a lot easier. More create options are [here](http://docs.aws.amazon.com/elasticbeanstalk/latest/dg/eb3-create.html).

	Now, we are prompted with: 

	```
	Enter Environment Name
	(default is awsbean-dev): 
	Enter DNS CNAME prefix
	(default is awsbean-dev): 

	Enter an RDS DB username (default is "ebroot"): 
	Enter an RDS DB master password: 
	Retype password to confirm: 
	```

	Fill out those settings as you'd like. Take note of the master password you set.

	Set default environment in elastic beanstalk.  The environment name is what we entered during the `eb create -db` process.

	```
	eb use awsbean-dev
	```








6. **Django Production `settings.py`:**
	* These credentials are needed for deployment* 
	* In many cases, you will have a `production` version of your `settings.py` instead of the default `Django` install.


	```
	AWS_ACCESS_KEY_ID = "<your_access_key_id>"
	AWS_SECRET_ACCESS_KEY = "<your_secret_access_key>"
	```

	```
	if 'RDS_DB_NAME' in os.environ:
		DATABASES = {
		    'default': {
		        'ENGINE': 'django.db.backends.mysql',
		        'NAME': os.environ['RDS_DB_NAME'],
		        'USER': os.environ['RDS_USERNAME'],
		        'PASSWORD': os.environ['RDS_PASSWORD'],
		        'HOST': os.environ['RDS_HOSTNAME'],
		        'PORT': os.environ['RDS_PORT'],
		    }
		}
	```


7. **Setup EB Extensions:**
	1. Create new folder called `.ebextensions` in the root of your virtualenv where the `.elasticbeanstalk` directory is as well.
	2. Add a new file called `01_awsbean.config` in `.ebextensions` with contents of:
	```
	option_settings:
		  "aws:elasticbeanstalk:application:environment":
		    DJANGO_SETTINGS_MODULE: "awsbean.settings"
		    PYTHONPATH: "/opt/python/current/app/src:$PYTHONPATH"
		  "aws:elasticbeanstalk:container:python":
		    WSGIPath: "src/awsbean/wsgi.py"
	```
	*Note*: `awsbean` above will be replaced with your app name.

	3. Add a new file called `02_packages.config` in `.ebextensions` with contents of:
	```
	packages:
	  yum:
	    git: []
	```

	4. Add a new file called `03_python.config` in `.ebextensions` with contents of:
	```
	container_commands:
  		01_migrate:
    		command: "python src/manage.py migrate --noinput"
    		leader_only: true
	```

	5. Commit in git:
	```
	git add .ebextensions/
	git commit -m "Created EB Extensions"
	```

8. **Add Django Requirements**
	Everytime you add new python packages, such as the `Django Rest Framework` or `Requests`, you need to update and commit your requirements.

	**Install MySQL-python**

	```
	pip install MySQL-python
	```

	**Update (or create) `requirements.txt`**
	```
	pip freeze  #returns what packages are required/installed in your virtualenv.
	pip freeze > requirements.txt
	git add requirements.txt
	git commit -m "Updated requirements.txt"
	```


9. **1st Deploy to Elastic Beanstalk**
	Do Deployment:
	```
	eb deploy
	```
	**Returns** something like:
	```
	Creating application version archive "app-903f-151207_174054".
	Uploading awsbean/app-903f-151207_174054.zip to S3. This may take a while.
	Upload Complete.
	INFO: Environment update is starting.                               
	INFO: Deploying new version to instance(s).                         
	INFO: New application version was deployed to running EC2 instances.
	INFO: Environment update completed successfully.
	```


10. **Create Superuser with Custom Management** 
	Nice! We have deployed Django to elastic beanstalk! Great work. Now how do we create a superuser? Run collect static? This is when we need to add a few more customizations to the `.ebextensions` folder.
	
	1. Create a new Django App
		```
		cd src
		python manage.py startapp accounts
		cd accounts
		mkdir management
		cd management
		touch __init__.py
		mkdir commands
		cd commands
		touch __init__.py
		touch makesuper.py
		open makesuper.py
		```

	2. Create the `makesuper` Command inside the `makesuper.py` file we just created:
		```
		from django.contrib.auth import get_user_model
		from django.core.management.base import BaseCommand

		class Command(BaseCommand):
		    def handle(self, *args, **options):
		        User = get_user_model()
		        if not User.objects.filter(username="superu").exists():
		            User.objects.create_superuser("superu", "superu@teamcfe.com", "superuPASS")
		```
		This code checks if the `superu` exists and creates it if it doesn't. 

	3. Add the new `accounts` app to `INSTALLED_APPS` in `settings.py` 

	4. Now, we can use `python manage.py makesuper` which will automatcially create a Django super user with the username `superu` and password `superuPASS` -- this means we can login to the Django admin.


	5. Add new additions to git:
		```
		git add --all
		git commit -m "Makesuper command & Accounts App"
		```

	6. Create new EB Extension:
		Add `04_python.config` to `.ebextensions` folder with the following:
		```
		container_commands:
		  01_migrate:
		    command: "python src/manage.py makesuper"
		    leader_only: true
		```

	7. Add new eb ebextension to git:
		```
		git add --all
		git commit -m "Updated Eb Extensions"
		```
	
11. **Deploy!** 

	`eb deploy`





Subscribe on our [YouTube Channel](http://joincfe.com/youtube) and join us for more in-depth tutorials on [Django development](http://joincfe.com/enroll).


Cheers!


#### Organized by CodingForEntrepreneurs
