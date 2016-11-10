#Install PostgreSQL on Mac OS X / Linux
A simple guide on how to install PostgreSQL on your local Mac or Linux machine. 

### Using Homebrew 

Install Homebrew: [Linux](http://brew.sh/linuxbrew/) | [Mac](http://brew.sh/)


```
brew update
brew upgrade
brew doctor
brew install postgresql --with-python

```

### Activate PostgreSQL

Quick activation:

```

mkdir -p ~/Library/LaunchAgents 
ln -sfv /usr/local/opt/postgresql/*.plist ~/Library/LaunchAgents
launchctl load ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist
```


The above command comes from a fresh install of `postgresql` via `Homebrew` which will show you:

```
If builds of PostgreSQL 9 are failing and you have version 8.x installed,
you may need to remove the previous version first. See:
  https://github.com/Homebrew/homebrew/issues/2510

To migrate existing data from a previous major version (pre-9.4) of PostgreSQL, see:
  https://www.postgresql.org/docs/9.4/static/upgrading.html

To have launchd start postgresql at login:
  ln -sfv /usr/local/opt/postgresql/*.plist ~/Library/LaunchAgents
Then to load postgresql now:
  launchctl load ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist
Or, if you don't want/need launchctl, you can just run:
  postgres -D /usr/local/var/postgres
```



If you already had previously `postgresql` installed, you would see:

```
To reload postgresql after an upgrade:
  launchctl unload ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist
  launchctl load ~/Library/LaunchAgents/homebrew.mxcl.postgresql.plist
Or, if you don't want/need launchctl, you can just run:
  postgres -D /usr/local/var/postgres
```


Now, test `postgresql` with:
```
createdb
psql
```
You should see something like:
```
psql (9.4.5)
Type "help" for help.

jmitch=#
```
Where `jmitch` would be your username.




