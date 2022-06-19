## Design frontend and backend of the web app

App structure as the following

```sh
── Web_app/
  │   └── app.py                   <- python, flask, jsonify scripts, MYSQL configs
  │   └── templates/               <- Folder includes webpages
  │       ├── index.html           <- main app page
  │       ├── response.html        <- pages that capture the response from searching MYSQL database
  │   └── requirements.txt         <- requriments for python app using pip freeze
  │   └── Procfile                 <- for declaring what commands are run by your apps on heroku

```

### Install requirments:
- Python for windows
- Heroku for windows
- Git for windows
- pip install flask
- pip install flask_mysqldb
- pip install gunicorn
- pip install pyscopg2

### step 1 - flask codes in for the app.py file

to communicate with MYSQL data base that will create on the heroku later.

### step 2 - templates in html format

to webpage design and to capture the response from searching table in MYSQL database

### step 3 - create requirements.txt

```sh
pip freeze > requirements.txt
```
### step 4- create Procfile

File to declaring what commands are run by your apps on heroku, which can be create using VS code as new file (without extention). 
Make sure the file encoding is **UTF-8**, the deply will rejected otherwise.

In VS code write and save it

```
web: gunicorn app:app
```

Now the app is ready to deply on heroku [here](https://github.com/AAlhendi1707/bioinformatics-tools-finder/blob/main/deployment.md)



