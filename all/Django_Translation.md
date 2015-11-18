Django Translation Guide
================

A (working) guide to installing and working with Django Translation. More coming soon...


### Mac & Linux Installation 
Install [Homebrew](http://brew.sh/) before install [gettext](https://www.gnu.org/software/gettext/).

1. Install Homebrew

	##### Mac [[Source](http://brew.sh/)]:


	```
	ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
	```  


	##### Linux [[Source](https://github.com/Homebrew/linuxbrew)]: 

	```
	ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/linuxbrew/go/install)"

	export PATH="$HOME/.linuxbrew/bin:$PATH"
	export MANPATH="$HOME/.linuxbrew/share/man:$MANPATH"
	export INFOPATH="$HOME/.linuxbrew/share/info:$INFOPATH"
	```

	Now you have "homebrew" installed on your Mac/Linux. So you can do commands like:

	```
	brew install PACKAGETOINSTALL
	```
	
	Already have brew installed? Do the following
	```
	brew update
	brew upgrade
	```

2. Install the `gettext` package:
	```
	brew install gettext
	brew link gettext --force
	```
> Please note: the command `brew link gettext --force` may be necessary for the command `python manage.py makemessages` to work correctly.




### Windows Installation
Follow the Django documentation [here](https://docs.djangoproject.com/en/1.8/topics/i18n/translation/#gettext-on-windows).






## Setup Translation in Django
1. Make `LOCALE_PATHS` directory and add to `settings.py`

	In your Base Directory of your project, where `manage.py` lives, create a directory called `locale`. Now in `settings.py` add the following tuple:

	```python
	LOCALE_PATHS = (
		os.path.join(BASE_DIR, "locale"),
	)
	```


2. Now you have `gettext` installed and the `LOCALE_PATHS` set, let's make our first translation file. 
	```
	python manage.py makemessages -l es
	```
> `python manage.py` and `django-admin.py` are interchangable if `manage.py` is present.

	In this case, the  `language` (command is `-l`) is `es` which is a [ISO](https://en.wikipedia.org/wiki/International_Organization_for_Standardization) locale name for `Español` (`Spanish`). To see a list of ISO 639 Locale Names, visit [wikipedia](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) and lookup the 639-1 column for the lowercase abreviation in the language of your choice. 

	Some examples:
	`de` = `Deutsch` = `German`
	`da` = `Dansk` = `Danish`
	`pt` = `Português` = `Portuguese`
	`pt_BR` = `Português` = `Brazilian Portuguese`



3. What happens? 
	The command `python manage.py makemessages -l es` creates the following:
		1. A new directory inside of `locale` (which we created above) called `es`
		2. `es` holds a directory called `LC_MESSAGES`
		3. Inside of `LC_MESSAGES` we have a file called `django.po`
	This will be true for every new language you are trying to translate for. 


4. What's in `Django.po`? It starts with `Legal/Attribution` stuff like:
	```
	# SOME DESCRIPTIVE TITLE.
	# Copyright (C) YEAR THE PACKAGE'S COPYRIGHT HOLDER
	# This file is distributed under the same license as the PACKAGE package.
	# FIRST AUTHOR <EMAIL@ADDRESS>, YEAR.
	#
	#, fuzzy
	msgid ""
	msgstr ""
	"Project-Id-Version: PACKAGE VERSION\n"
	"Report-Msgid-Bugs-To: \n"
	"POT-Creation-Date: 2015-09-08 18:50-0700\n"
	"PO-Revision-Date: YEAR-MO-DA HO:MI+ZONE\n"
	"Last-Translator: FULL NAME <EMAIL@ADDRESS>\n"
	"Language-Team: LANGUAGE <LL@li.org>\n"
	"Language: \n"
	"MIME-Version: 1.0\n"
	"Content-Type: text/plain; charset=UTF-8\n"
	"Content-Transfer-Encoding: 8bit\n"
	"Plural-Forms: nplurals=2; plural=(n != 1);\n"
	```

	Then you see stuff like this:
	```

	#: templates/registration/activate.html:6
	msgid "Account activation failed"
	msgstr ""

	#: templates/registration/activation_complete.html:5
	msgid "Your account is now activated."
	msgstr ""

	#: templates/registration/activation_email.txt:2
	msgid "Activate account at"
	msgstr ""

	#: templates/registration/activation_email.txt:11
	#, python-format
	msgid "The above link is valid for %(expiration_days)s days."
	msgstr ""

	#: templates/registration/login.html:14
	#: templates/registration/password_change_form.html:9
	#: templates/registration/password_reset_confirm.html:12
	msgid "Submit"
	msgstr ""

	#: templates/registration/login.html:23
	msgid "Forgot password"
	msgstr ""

	```
> If you do not see anything beyond the `Legal/Attribution`, it's likey becuase you have not implemented anything to be translated just yet. Which is in the next step.

5. Let's do some translation strings. You can put this line in any `view` or `context` you may need. It all comes down to experimenting:. 
	```
	from django.utils.translation import ugettext

	output = ugettext("Welcome to my site.")

	```

	A common shortcut is to use an underscore `_` in place of `ugettext` like so:
	
	```
	from django.utils.translation import ugettext as _
	output = _("Welcome to my site.")
	```
	
	In a **view** ([Source](https://docs.djangoproject.com/en/dev/topics/i18n/translation/#standard-translation)):

	```python
	# someapp/views.py
	
	from django.utils.translation import ugettext as _
	from django.http import HttpResponse

	def my_view(request):
    	sentence = 'Welcome to my site.'
    	output = _(sentence)
    	return HttpResponse(output)

	```

	or in a **template**:

	```html
	<!-- location: templates/some_random/template.html -->
	{% load i18n %}

	<h1>{% trans "This is the title." %}</h1>
	```

6. Run `makemessages` again.
	```
	python manage.py makemessages -l es
	```

7. Open `django.po` in `your_django)project/locale/es/LC_MESSAGES/`. You should now see something like:
	
	```
	#: someapp/views.py:6
	msgid "Welcome to my site."
	msgstr ""

	#: templates/some_random/template.html:11
	#, python-format
	msgid "This is the title."
	msgstr ""

	```
	
	You can now add your translation to it:


	```
	#: someapp/views.py:6
	msgid "Welcome to my site."
	msgstr "Bienvenidos a mi sitio."

	#: templates/some_random/template.html:11
	#, python-format
	msgid "This is the title."
	msgstr "Este es el título."

	```

8. Complie messages: 
   ```
   python manage.py compilemessages
   ```

9. Activate test in a view:
   ```
   from django.utils import translation
   from django.utils.translation import ugettext as _
   
   def home(request):
        title = _("Welcome")
	    if 'lang' in request.GET:
	          translation.activate(request.GET.get('lang'))
	    return render(request, 'home.html', {"title": title})
	
   ```

10. Repeat 5-8 for every string you need to translate. There are more advanced uses for Translation so please refer to the [Django Docs](https://docs.djangoproject.com/en/dev/topics/i18n/translation) for more.


*More Coming Soon (including Testing and Next Steps)*
