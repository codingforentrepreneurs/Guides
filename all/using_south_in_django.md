Using South in Django
======

Simple guide to using South for making changes (migrations/schemamigrations) to your database within any Django Project. In sort, change your models without writing database code.


1. Install south using PIP using Terminal (Mac/Linux) or Command Prompt (Windows): 
```
pip install south
```
2. Add south to Django's settings.py in **INSTALLED_APPS**

```python
#settings.py
INSTALLED_APPS = (
    #django defaults
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    # third part apps, in this case, south
    'south',
    #your apps
    'yourapp',
    'app1',
    'app2',

)
```
2. Ensure Model is in the synced in database using Terminal/Command Prompt (Mac or Linux/Windows):
```
python manage.py syncdb

#should result in something like...

Syncing...
Creating tables ...
Installing custom SQL ...
Installing indexes ...
Installed 0 object(s) from 0 fixture(s)

Synced:
 > django.contrib.admin
 > django.contrib.auth
 > django.contrib.contenttypes
 > django.contrib.sessions
 > django.contrib.messages
 > django.contrib.staticfiles
 > south
 > yourapp
 > app1
 > app2

Not synced (use migrations):
(use ./manage.py migrate to migrate these)
```

3. Convert the model to south in Terminal (Mac/Linux) or Command Prompt (Windows) with: 
```
python manage.py convert_to_south yourapp
```

4. Make changes to model
```python
#App name is yourapp, Model is Join
#before changes
class Join(models.Model):
	email = models.EmailField()
	timestamp = models.DateTimeField(auto_now_add = True, auto_now=False)
	updated = models.DateTimeField(auto_now_add = False, auto_now=True)
	
	def __unicode__(self):
		return "%s" %(self.email)

#after changes
class Join(models.Model):
	email = models.EmailField()
	ip_address = models.CharField(max_length=120, default='ABC')
	timestamp = models.DateTimeField(auto_now_add = True, auto_now=False)
	updated = models.DateTimeField(auto_now_add = False, auto_now=True)

	def __unicode__(self):
		return "%s" %(self.email)

```
5. Run schemamigration in Terminal (Mac/Linux) or Command Prompt (Windows): 
```
python manage.py schemamigration yourapp --auto
```
6. Run migrate in Terminal (Mac/Linux) or Command Prompt (Windows):
```
python manage.py migrate

#or

python manage.py migrate yourapp
```

That's it! If you have trouble, delete the datbase (such as db.sqlite3) and any/all migrations folders for apps (yourapp/migratoins) then run `python manage.py syncdb` again.