## Design frontend and backend of the web app

App structure as the following

```sh
── Web_app/
  │   └── app.py                   <- python, flask, jsonify scripts, MYSQL configs
  │   └── templates/               <- Folder includes webpages
  │       ├── index.html           <- main app page
  │       ├── response.html        <- pages that capture the response from searching MYSQL database table
  │   └── Procfile                 <- for declaring what commands are run by your apps on heroku
  │   └── requirements.txt         <- requriments for python app using pip freeze
  │   └── .git/                    <- git version of app that ready to push
```
