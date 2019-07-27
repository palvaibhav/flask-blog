# flask-blog
https://flask-blog-123.herokuapp.com/          
A simple blogging website where users can create new posts.

# Creating a virtual env
`virtualenv venv` : This creates a virtual env in out project directory.           
`. venv/bin/activate` : This activates the venv.             

# Connecting to PostgresSQL
1. Install PostgresSQL to local machine             
   - `sudo apt-get install postgresql postgresql-contrib`  
   - `sudo -u postgres createuser --superuser <name_of_user>`
2. Create Database          
   - `sudo -u <name_of_user> createdb <name_of_db>`       
   - `psql -U <name_of_user> -d <name_of_db>` : To check the created db.    
3. In config.py add the following line:-
   - `SQLALCHEMY_DATABASE_URI = os.environ.get('DATABASE_URL')`
4. In ~/.bashrc add the following line:-
   - `export DATABASE_URL="postgresql:///<name_of_db>"`    
5. Create file manage.py.
6. Install following extensions:-
   - `pip install flask_script`
   - `pip install flask_migrate`
   - `pip install psycopg2-binary`
7. Start migrating
   - `python manage.py db init`
   - `python manage.py db migrate`
   - `python manage.py db upgrade`
   - `\dt`: To list all tables in the db.
   - `\d <table-name>`: To list details about a table.
8. Run the server
   - `python manage.py runserver`: This runs the app at `localhost:5000`
   
# Deploying app to Heroku
1. Install gunicorn
   - `pip install gunicorn`
2. Make runtime.txt with following line in it
   - `python-3.7.3`
3. Freeze all the app dependencies in requirements.txt file
   - `pip freeze > requirements.txt`
   - Remove line `pkg-resources==0.0.0` from the requirements.txt file.
4. Make Procfile with following line in it
   - `web: gunicorn -w 4 flaskblog.wsgi:app`
5. Commit the repo
   - `git add .`
   - `git commit -m 'Final commit'`
6. Login to heroku account
   - `heroku login`
7. Create new heroku app
   - `heroku create <name_of_your_application>`
8. Set config vars for heroku by
   - `heroku config:set <KEY>=<VALUE>`
9. Add Postgres addon to Heroku server by
   - `heroku addons:create heroku-postgresql:hobby-dev --app <name_of_your_application>`
10. Push the repo to heroku by
    - `git push heroku master`
11. Create all the required tables in db on heroku servers by 
    - `heroku run python manage.py db upgrade --app <name_of_your_application>`
