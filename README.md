# noople - the world's worst search engine

(Change `SITE_NAME` to DuckDuckNope for enhanced privacy.)

noople is a search engine that doesn't have any results. It is based on the [Python Flask framework](https://flask.palletsprojects.com/en/1.1.x/) and [SQLite](https://www.sqlite.org/index.html).

noople can be used to demonstrate:

* Reading GET requests in Flask
* Processing SQL requests in Python
* Reflected XSS vulnerabilities
* Stored XSS vulnerabilities
* SQL injection vulnerabilities

## Setting up the database

### Install prerequisite packages:

    sudo apt install libmariadbclient18 libmysqlclient-dev mysql-client \
                     mysql-server python-mysqldb

### Create database, user

    sudo mysql -u root
    CREATE USER 'noople'@'localhost' IDENTIFIED BY '12345678';
    CREATE DATABASE noople;
    GRANT ALL on noople.* TO 'noople'@'localhost';
    exit

### Create table, stored procedures

    cat noople/schema.sql | mysql -u noople -p

## Run the application

Create a Python virtual environment, if you haven't already:

    python3 -m venv venv

Activate your virtual environment:

    source venv/bin/activate

Install the requirements:

    pip3 install -r requirements.txt

Run the application:

    export FLASK_APP=noople/search.py
    flask run

Visit http://localhost:5000 in a web browser.

## (Known) Vulnerabilities

### Reflected XSS

To fix this, use `escape`. See [Flask escape](https://flask.palletsprojects.com/en/1.1.x/api/#flask.escape)

### Stored XSS

To fix this, use `escape`. See [Flask escape](https://flask.palletsprojects.com/en/1.1.x/api/#flask.escape)

### SQL injection

To fix this, use `execute` (instead of `executescript`) with bind variables. See [sqlite3: execute](https://docs.python.org/3/library/sqlite3.html#sqlite3.Cursor.execute)
