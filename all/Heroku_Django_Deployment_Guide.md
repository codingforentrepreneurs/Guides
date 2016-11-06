# Heroku & Django Deployment Guide

A installation guide for getting Django setup on Heroku

----------

1. Sign up for Heroku [Non-Affiliate](http://www.kirr.co/9e88gh/)

2. Download & Install [Heroku Command Line Interface](http://cli.heroku.com)

3. Open Terminal or Command Prompt (Windows users)

4. Authenticate with Heroku:
    ```
    $ heroku login
    Enter your Heroku credentials.
    Email: <your-heroku-account-email>
    Password (typing will be hidden): 
    Logged in as <your-heroku-account-email>
    ```

5. Install Python:
    [Python.org](http://www.kirr.co/52lk1y/)
    or
    Mac watch [here](http://www.kirr.co/a9u645/)
    Linux watch [here](http://www.kirr.co/yoywdh/)
    Windows watch [here](http://www.kirr.co/xeaocj/)

### Start Django Project Locally
1. Create Dev Directory for Project Storage
    ```
    cd ~/
    mkdir Dev && cd Dev
    ```

2. Create Virtualenv in Python 3 (use python2 for Python 2)
    ```
    cd ~/Dev
    mkdir cfehome && cd cfehome
    virtualenv -p python3 .

    # activate on Mac/Linux
    source bin/activate

    # activate on Windows
    .\Scripts\activate
    ```

4. Install Django & Start Project
    ```
    pip install django==1.10.3

    mkdir src && cd src 

    django-admin.py startproject cfehome . 

    # Windows (optional)
    .\Scripts\django-admin.py startproject cfehome .
    ```

5. Run Migration & Createsuperuser
    ```
    python manage.py migrate
    python manage.py createsuperuser
    ```

6. Additional Installations
    ```
    pip install gunicorn dj-database-url psycopg2
    ```

7. Create `requirements.txt` file
    ```
    pip freeze > requirements.txt
    ```

8. Static Files:
    We suggest using [Amazon Web Service S3](http://www.kirr.co/exuykp/) for static files in general. However, if you want to use Heroku consider their recommendation in this [section](https://devcenter.heroku.com/articles/django-app-configuration#whitenoise).



### Setup your Django Project on Git
1. Initialize Git in the root of your Django Project (where `manage.py` is)
    ```
    # cd /path/to/your/project
    cd ~/Dev/cfehome/src/
    git init 
    ```

2. Create `.gitignore` file with the exact contents of [this .gitignore file](http://www.kirr.co/mbehan/). Put at the same path as where you did the `git init`

3. Run `git status` result should be:
    ```
    On branch master

    Initial commit

    Untracked files:
      (use "git add <file>..." to include in what will be committed)

        .gitignore
        cfehome/
        db.sqlite3
        manage.py
        requirements.txt

    nothing added to commit but untracked files present (use "git add" to track)
    ```

4. First Commit
    ```
    git add --all
    git commit -m "Intial Commit"
    ```


### Heroku Setup
1. Navigate to the root of your Django Project (where `manage.py` is):
    ```
    cd ~/Dev/cfehome/src/
    ```
2. Create Procfile with the contents:
    ```
    web: gunicorn cfehome.wsgi --log-file -
    ```

3. Call `git status`, result being:
    ```
    (cfehome) $ git status
    On branch master
    Untracked files:
      (use "git add <file>..." to include in what will be committed)

        Procfile

    nothing added to commit but untracked files present (use "git add" to track)
    (cfehome) $ 
    ```

4. Add Procfile to Git
    ```
    git add .
    git commit -m "Added Procfile"
    ```

5. Create Heroku App:
    Use `heroku create <your-app-name>` or just `heroku create`, such as:
    ```
    heroku create cfehome
    ```

    Unsuccessful Result should be:
    ```
    Creating ⬢ cfehome... !
    ▸    Name is already taken
    ```

    Successful Result should be:
    
    ```
    (cfehome) $ heroku create cfehome
    Creating ⬢ cfehome... done
    https://cfehome.herokuapp.com/ | https://git.heroku.com/cfehome.git
    ```

6. Test Heroku Locally
    ```
    heroku local web
    ```
    Open [http://localhost:5000/](http://localhost:5000/)

7. Create `runtime.txt` file for Python Version:
    In Django Project Root (where manage.py is), create a file `runtime.txt` with the contents:
    ```
    python-3.5.2
    ```
    Add to git
    ```
    git add runtime.txt
    git commit -m "Added runtime file"
    ```

### Update Django Settings for Production:
1. Update `settings.py`:
    - Change `DEBUG = TRUE` to `DEBUG = FALSE`

    - Add `cfehome.herokuapp.com` to `ALLOWED_HOSTS`:
        ```
        ALLOWED_HOSTS = ['cfehome.herokuapp.com']
        ```

3. Create `heroku` Live Database:
    ```
    heroku addons:create heroku-postgresql:hobby-dev
    ```

4. Configure Live Database on `settings.py`:
    ```
    # keep this
    DATABASES = {
        'default': {
            'ENGINE': 'django.db.backends.sqlite3',
            'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
        }
    }

    # add this
    import dj_database_url
    db_from_env = dj_database_url.config()
    DATABASES['default'].update(db_from_env)
    ```

5. Disable `python manage.py collectstatic` from running during default push:
    ```
    heroku config:set DEBUG_COLLECTSTATIC=1
    ```
6. (Optional) Enable `python manage.py collectstatic` to run during push:
    ```
    heroku config:set DEBUG_COLLECTSTATIC=0
        ```

### Push to Heroku
1. After all `git` commits, run:
    ``` 
    git push heroku master
    ```

2. Useful Django commands on Heroku:
    
    `heroku bash` opens the shell to do:
    ```
    python manage.py migrate
    python manage.py createsuperuser
    python manage.py shell
    ```
    ** Shortcut commands **:
    `heroku run python manage.py migrate`

    `heroku run python manage.py createsuperuser`

    `heroku run python manage.py shell`

    `heroku restart`

3. When you make changes to Django on your local project:
    1. Ensure `makemigrations` is ran prior to deployment:
        ```
        python manage.py makemigrations
        ```
    2. View local changes: `heroku local web` open [http://localhost:5000/](http://localhost:5000/)
    
    3. Commit all changes:
    ```
    git add --all

    git commit -m "Update something"
    ```
    4. Push & Migrate
    ```
    git push heroku master && heroku run python manage.py migrate
    ```
