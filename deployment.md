## Deployment to Heroku and configuration of MySQL Database

Heroku it is popular web hosting service. It is free for small work

## step 1 - Log in to Heroku

First we need a Heroku account and it can be created from the Signup Page.
After having an account, open command prompt, run the command:

```sh
heroku login
```
It will prompt us to enter our Heroku account (email & password) in a browser window. Then we will receive:

```sh
heroku: Press any key to open up the browser to login or q to exit:
Opening browser to https://cli-auth.heroku.com/auth/browser/xxx
Logging in... done
Logged in as xxxxxx@xxxx.com
```
## step 2 - Setup Git and Create a Heroku app

Point the command prompt to our project root directory, then create Git repository:

```sh
cd Web_app
git init
git add .
git commit -m "initial commit"
```
Create Heroku app with command: heroku create [app-name].

```sh
heroku create -a bioinformatics-tools-finder
#Creating ⬢ bioinformatics-tools-finder... done
#https://bioinformatics-tools-finder.herokuapp.com/ | https://git.heroku.com/bioinformatics-tools-finder.git
```
You can check the result of this step with git remote -v:

```sh
git remote -v
#heroku  https://git.heroku.com/bioinformatics-tools-finder.git (fetch)
#heroku  https://git.heroku.com/bioinformatics-tools-finder.git (push)
```
if connection did not establised with git.heroku.com, then you can set it manually using command:
```sh
heroku git:remote -a bioinformatics-tools-finder
```
Also see deploying on heroku with Git on https://devcenter.heroku.com/articles/git

## step 3 - Deploy the app to Heroku

We can easily deploy our web app to Heroku by pushing the code to the remote repository that we created at the previous step. Heroku will automatically detects that this is a Node.js app and builds it accordingly.

```sh
git push heroku master
```

## step 4 - Configure MySQL Database for web app on Heroku app

**create ClearDB**

Heroku provides PostgreSQL as default database engine for our application. In this tutorial, we’re gonna work with MySQL database, so service provider called ClearDB will be used. For more see https://devcenter.heroku.com/articles/cleardb

To get started, install ClearDB add-on to our application with command:

```sh
heroku addons:create cleardb:ignite
#Creating cleardb:ignite on ⬢ bioinformatics-tools-finder... free
#Created cleardb-cubed-xxxx as CLEARDB_DATABASE_URL
#Use heroku addons:docs cleardb to view documentation
```

**Configure MySQL connection**

After installing the Add-ons, we can get our database URL by running the command:

```sh
heroku config | findstr CLEARDB_DATABASE_URL
CLEARDB_DATABASE_URL: mysql://username:password@host/database?reconnect=true
```
Copy the value of the CLEARDB_DATABASE_URL config variable and use it in the following command:

```sh
heroku config:set DATABASE_URL='mysql://username:password@host/database?reconnect=true'
#Setting DATABASE_URL and restarting ⬢ bioinformatics-tools-finder... done, v6
#DATABASE_URL: 'mysql://username:password@host/database?reconnect=true'
```

**Config flask app in app.py file** to connect ClearDB MySQL on Heroku
In the previous step, we get DATABASE_URL that contains:

```py
app = Flask(__name__)
app.config['MYSQL_HOST'] = 'host'
app.config['MYSQL_USER'] = 'username'
app.config['MYSQL_PASSWORD'] = 'password'
app.config['MYSQL_DB'] = 'database'
```
Don’t forget to push the updated code to Heroku remote repository.
```sh
git add .
git commit
git push heroku master
```

**Create MySQL table on ClearDB**

Before testing our app on Heroku, we need to create MySQL table named customers on ClearDB. Using the connect parameters above, open another command prompt, run the command:
```sh
# connect to database on heroku
mysql --host=host --user=username --password=password --reconnect database

## create a table
mysql> CREATE TABLE IF NOT EXISTS `customers` (
  id int(11) NOT NULL PRIMARY KEY AUTO_INCREMENT,
  name varchar(255) NOT NULL,
  description varchar(500) NOT NULL,
  pmid varchar(45) NOT NULL,
) ENGINE=InnoDB DEFAULT CHARSET=utf8;
```

