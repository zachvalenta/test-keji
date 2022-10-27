# TODO

## 参考

📜 https://flask.palletsprojects.com/en/1.1.x/ http://flask.pocoo.org/docs/0.12/
🔍 Pretty Printed, Corey Schafter
🧪 https://github.com/zachvalenta?tab=repositories&q=flask

## current

## next

## done

> prefer Django (community, project structure, docs) https://github.com/gyllstromk/Flask-WhooshAlchemy/issues/66
* _2020_: basics - CRUD (seed, ORM, serialization) UI (styling, search, pagination) CQ (testing, hooks) env (conf, Docker); attempt to separate models/schemas into own modules for `crud` and tests break only when run via pre-commit
* _2019_: Ekker course, API extensions, project structure (Grinberg chapter 7), `python-dotenv`/Flask interplay, Herman https://github.com/mjhea0/flaskr-tdd testing (real-ish test client vs. previous `book-db` implementation) templates w/ water.css, gunicorn in background, different ways to access data (form, JSON, query string), auth landscape
* _2018_: Grinberg chapters 1-4, PS tutorial (Ray)

# STRUCTURE

https://testdriven.io/blog/dynamic-secret-generation-with-vault-and-flask/

🗄 different versions of the docs https://fastapi.tiangolo.com/tutorial/sql-databases/

* _app factory_: func that take conf obj and return app instance; necessary for testing https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-xv-a-better-application-structure 
* _blueprint_: 类似 Django app https://www.youtube.com/watch?v=pjVhrIJFUEs https://www.youtube.com/watch?v=rGQKHpjMn_M
* _taxonomies_: https://exploreflask.com/en/latest/organizing.html 
* organization: by functionality, by feature https://www.openmymind.net/Project-Organisation/
* _sink_: https://www.youtube.com/watch?v=MbXEQZZSvzk setup.py https://flask.palletsprojects.com/en/1.1.x/patterns/packages/ startup.py and servers https://github.com/microsoft/python-sample-vscode-flask-tutorial/blob/master/startup.py

__complaints__

* _premature optimization_: instead of single module to n modules to pkg, single module to pkg
* _over-nesting_: Grinberg chapter 7 https://flask.palletsprojects.com/en/1.1.x/patterns/packages/
* _reasons for mod-2-pkg not articulated_: Grinberg knows what's going on, Schafer summarizing, idk if Flask docs cover this (didn't you complain about this in a Github ticket) https://www.youtube.com/watch?v=44PvX0Yv368 @ 3:15-5:30

## blog

how did this happen?
* Premature optimization https://github.com/pallets/flask/issues/2626 https://lepture.com/en/2018/structure-of-a-flask-project

The core of Flask project structure is:
* routes
* configuration
* database
There can be more (Swagger, error handlers), especially if you're using Flask's templating (static assets, forms), but this tutorial only covers the 3 core aspects.

why project structure in Flask is hard

_You need to know how imports and packages work in Python_
* What's the difference between a namespace package and a regular package?
* When is `__init__.py` necessary? recommended?
* Python core devs write articles called 'Import Traps for the Unwary'

_there is no consensus_
* `app.py` in the project root? Real Python's Flask boilerplate uses this, but `Flask Mega Tutorial` starts with a nested package structure.
* Externalize your application config in a `settings.py` file? 📍 example
* Use bluerprints? From the start of the project, or later when refactoring? 📍 example
* Create an application instance and pass it around? the official Flask tutorial recommended this for the first 8 years of the framework, but now uses application factories

why existing solutions are insufficient

* _no explanation_: Grinberg
* _premature optimization_: official tutorial 📝 Flask already violates ['The menu is omakase'](https://rubyonrails.org/doctrine/), so the default should be "here's the hello world way to do it, here's the intermediate way"

my approach
* explain Python packages and imports enough that everything else will make sense
* h/t William Vincent: build 3 different Flask apps, each with a different project structure
* focus just on project structure; we won't concern ourselves with other functionality, any extensions will only be used to illustrate project structure

## 🌱 single module

* good for...tricking people into thinking Flask is easy
```sh
├── proj
│   └── app.py
```

* _examples_: Ray, Real Python https://github.com/realpython/flask-boilerplate
* complicates testing
> The Flask application instance is created as a global variable in `app/__init__.py`, and then imported by a lot of application modules. While this in itself is not a problem, having the application as a global variable can complicate certain scenarios, in particular those related to testing. https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-xv-a-better-application-structure 

## 🌿 n modules

* good for...creating circular imports
```sh
├── proj
│   └── app.py
│   └── models.py
│   └── routes.py
```

* what's worked for me so far
```python
# app.py
app = Flask(__name__)
db = SQLAlchemy(app)
ma = Marshmallow(app)
from models import Foo
from schemas import FooSchema

# models.py
from app import db
class Foo(db.Model):
    pk = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(30))

# schemas.py
from app import ma
from models import Foo
class FooSchema(ma.ModelSchema):
    class Meta:
        model = Foo
```

* and ugly workarounds
```python
app = Flask(__name__)
db = SQLAlchemy(app)
import models
```

* _examples_: Ekker, Herman https://github.com/zachvalenta/herman-flask-tdd Schafer https://www.youtube.com/watch?v=44PvX0Yv368
* _circular imports_: https://lepture.com/en/2018/structure-of-a-flask-project https://www.youtube.com/watch?v=44PvX0Yv368 @ 3:15-5:30 https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-xxiii-application-programming-interfaces-apis
* Herman tutorial https://github.com/mjhea0/flaskr-tdd (has the same circular import issue that n-module structures typically have)

## 🍀 pkg

* good for...doing anything you'd actually want to do in a basic web app
```sh
├── proj/
├──── app/
        └── __init__.py
├──────── models/
        └── users.py
        └── posts.py
├──────── routes/
        └── home.py
        └── account.py
├──────── templates/
        └── base.html
        └── index.html
```

* _examples_: https://pythonbytes.fm/episodes/show/102/structure-of-a-flask-project
* _constraints_: https://flask.palletsprojects.com/en/1.1.x/patterns/packages

## 🗣 Ray

🗄 `ekker`

```sh
├── app.py
├── models.py
├── settings.py
```

The app instance is created in `settings.py`, after which two other modules import it:

* `app.py`: to use for routes
* `models.py`: to use for db interaction --> this instance is also imported back into `app.py`

The end result is that `app.py` imports the same app instance, a vanilla version and a db version built on top of the vanilla version. This smells a bit off but at least is not circular.

## 🗣 Grinberg

📦 https://github.com/miguelgrinberg/flasky-first-edition

⚠️ lost trust in author after chapter 7

* 1a-6b https://github.com/miguelgrinberg/flasky-first-edition/tree/6b
```sh
├── app.py  # routes, SQLAlchemy classes
├── static/
├── templates/
```

* 7a https://github.com/miguelgrinberg/flasky-first-edition/tree/7a too nested [Grinberg 75]
```sh
├── app/
│   └── __init__.py
│   └── main/  # justification for extra nesting is blueprint
        └── __init__.py
        └── forms.py
        └── views.py
│   └── models.py
│   └── static/
│   └── templates/
├── config.py  # ❓ why aren't these stored in `.env`
├── manage.py  # 类似 `Makefile`
├── migrations/
├── requirements.txt
├── tests/
```

## sink

* https://www.youtube.com/watch?v=rGQKHpjMn_M https://www.youtube.com/watch?v=_5OXmXvkU_E https://www.youtube.com/watch?v=rGQKHpjMn_M official, Herman course, Schafer, Grinberg, Smallshire https://flask.palletsprojects.com/en/1.1.x/patterns/packages/ https://flask.palletsprojects.com/en/1.1.x/tutorial/layout/

* Schafer: put tests in `app`? `run.py` necessary? https://www.youtube.com/watch?v=44PvX0Yv368
```sh
├── app/
    └── __init__.py
    └── forms.py
    └── models.py
    └── views.py
    ├── static/
        └── style.css
    ├── templates/
        └── index.html
        └── 404.html
├── dotfiles
├── immediate-files
├── run.py
```

* 📍 have a second look at this, my initial approach might need some work
```sh
├── dotfiles
├── immediate-files
├── src/
│   └── __init__.py
│   └── models.py
├── templates/
│   └── index.html
│   └── 404.html
├── tests/
│   └── test_app.py
│   └── test_models.py
├── utils/
│   └── seed.py
│   └── repl.py
│   └── post.json
```

# ZA

* history: Sinatra (Ruby) Flask (Python) Express (Node) Fiber (Golang)
* new version https://testdriven.io/blog/flask-async/
* _deployment_: manual https://www.youtube.com/playlist?list=PL-osiE80TeTs4UjLw5MM6OjgkjFeUxCYH
* _favicon_: idky but official docs don't work w/ Chrome, use this instead `<link rel="shortcut icon" type="image/x-icon" href="static/favicon.png">` https://stackoverflow.com/a/51542518/6813490
* _microservices_: https://www.youtube.com/watch?v=nrzLdMWTRMM https://testdriven.io/courses/microservices-with-docker-flask-and-react/
* _middleware_: https://flask.palletsprojects.com/en/1.1.x/patterns/deferredcallbacks/
* _msg flashing_: record msg during req and access on next request; stored in `session` http://flask.pocoo.org/docs/1.0/quickstart/#message-flashing http://flask.pocoo.org/docs/1.0/patterns/flashing/ https://github.com/zachvalenta/pacific https://github.com/zachvalenta/flask-ekker
* `rv`: 'return value' https://stackoverflow.com/questions/29499188/why-rv-in-flask-testing-tutorial
* save file https://stackoverflow.com/a/42425388/6813490
* _signal_: send msg from one extension to another (or core framework) https://flask.palletsprojects.com/en/1.1.x/signals/
* _SPA_: https://flask.palletsprojects.com/en/1.1.x/patterns/singlepageapplications/
* _terminology_: instead of MVC, M (data interface) T (render HTML) V (res to req)
* _Vue_: https://testdriven.io/blog/combine-flask-vue/

design https://talkpython.fm/episodes/show/13/flask-web-framework-and-much-much-more Armin @ 33:00
* _components_: templates (Jinja2) HTTP (Werkzeug) https://testdriven.io/blog/what-is-werkzeug/
* _contraints_: no async until support dropped for Python 2.7 and 3.4 https://talkpython.fm/episodes/transcript/177/flask-goes-1.0 https://flask.palletsprojects.com/en/1.1.x/design/#thread-locals
* _Django_: seems like the upper limit of what you should be using Flask for is imperative CRUD; once you're adding a REST framework or an admin panel you've gone too far https://testdriven.io/blog/django-vs-flask/
* _performant_: Pinterest, Twilio, LinkedIn
* _principles_: configuration over convention https://drewdevault.com/2019/01/30/Why-I-built-sr.ht-with-Flask.html API is so good other frameworks use it https://pythonbytes.fm/episodes/show/133/github-sponsors-the-model-open-source-has-been-waiting-for
* _small_: approx 30k LOC

search
* approach: render homepage w/ results and navigate back to the true home page as a hack in lieu of actually clearing the results
* testing: create n records and then assert `perform_search` only returns a subset
```html
<form action="{{ url_for('perform_search') }}" method="post">
    <input type="text" name="lookup">
    <input type="submit">
</form>
```
```python
@app.route("/search", methods=["POST"])
def perform_search():
    query = request.form["lookup"]
    results = exec_sql(query)
    return render_template("homepage.html", items=results)
```

* what is the point of the shell?
```sh
(venv) $ flask shell
Instance: /Users/adcbtb9/Desktop/zv/code/trspoc/instance
>>> import app
>>> dir(app)
['Flask', 'Response', 'SQLAlchemy', 'Thing', '__builtins__', '__cached__', '__doc__', '__file__', '__loader__', '__name__', '__package__', '__spec__', 'app', 'basedir', 'db', 'db_path', 'db_uri', 'find_dotenv', 'get_by_id', 'get_index', 'jsonify', 'load_dotenv', 'make_response', 'os', 'post_by_text', 'request']

(venv) $ bpython
bpython version 0.18 on top of Python 3.7.4 /Users/adcbtb9/Desktop/zv/code/trspoc/venv/bin/python3
>>> import app
>>> dir(app)
['Flask', 'Response', 'SQLAlchemy', 'Thing', '__builtins__', '__cached__', '__doc__', '__file__', '__loader__', '__name__', '__package__', '__spec__', 'app', 'basedir', 'db', 'db_path', 'db_uri', 'find_dotenv', 'get_by_id', 'get_index', 'jsonify', 'load_dotenv', 'make_response', 'os', 'post_by_text', 'request']
```

## auth

* `flask-security`: wraps `flask-mail`, `itsdangerous`, `flask-login` https://www.youtube.com/watch?v=LsHf3JSDBVc project maintenance in doubt https://github.com/mattupstate/flask-security/issues/854 build failing for a month https://travis-ci.org/mattupstate/flask-security
* security headers https://github.com/TypeError/secure
* _JWT_: https://www.youtube.com/watch?v=J5bIPtEbS0Q Ray https://github.com/vimalloc/flask-jwt-extended https://github.com/mattupstate/flask-jwt https://www.youtube.com/watch?v=WubG9iKXZ2g https://www.youtube.com/watch?v=WxGBoY5iNXY https://www.youtube.com/watch?v=WubG9iKXZ2g https://www.youtube.com/watch?v=J5bIPtEbS0Q https://news.ycombinator.com/item?id=33019960
* _login_: https://www.youtube.com/watch?v=vVx1737auSE https://flask.palletsprojects.com/en/0.12.x/tutorial/views/#tutorial-views https://github.com/maxcountryman/flask-login https://www.youtube.com/watch?v=K0vSCCAM2ss https://www.youtube.com/watch?v=2dEM-s3mRLE https://www.youtube.com/watch?v=K0vSCCAM2ss
* _Oauth_: https://docs.authlib.org/en/latest/basic/intro.html https://github.com/singingwolfboy/flask-dance https://flask-oauthlib.readthedocs.io/en/latest/
* _password reset_: Schafer https://www.youtube.com/watch?v=vutyTx7IaAI 

* generate time-sensitive token
```python
s = Serializer(key, time)
token = s.dumps({'user_id' : 1})  # long string
s.loads(token)  # will return user obj or itsdangerous.SignatureExpired
```

* views
```python
def request_reset():
    if request.method == "GET":
        return render_template('req_reset.html')
    if request.method == "POST":
        form.validate_on_submit():  # flask thing?
            user = User.query.filter_by(email=form.email)
            send_reset_email(user)
            return(redirect('login.html'))

def send_reset_email(user):
    pass
```

* user model ❓ flask_login UserMixin necessary here?
```python
class User(db.Model):
    user_id = db.Column(db.Integer, primary_key=True)
    user_name = db.Column(db.String(20), unique=True, nullable=False)
    email = db.Column(db.String(80), unique=True, nullable=False)
    password = db.Column(db.String(80), nullable=False)

    def __repr__(self):
        return f"id {self.user_id} name {self.user_name}"
```

## config

🗄 `python.md` lib/config

python-dotenv, env file
* _dev server_: `load_dotenv(find_dotenv())` is called by `flask run` i.e. you only need to install python-dotenv but not import/call in src https://stackoverflow.com/a/52358706 https://github.com/pallets/flask/pull/2416/files https://github.com/zachvalenta/docker-flask-sqlite-skeleton/commit/fbc3428eb9aa7dbf29c6bede7a7e405f93e53c25
* _production server_: need to call `load_dotenv(find_dotenv())` in src
* _alternatives_: can also set env var from shell or with script (`export $VAR`) [Grinberg 6.70] but still need to run `load_dotenv(find_dotenv())`
```conf
# default https://flask.palletsprojects.com/en/1.1.x/config/#ENV
FLASK_ENV=production
# local
FLASK_ENV=development
```

__approaches__

* classes: https://github.com/miguelgrinberg/flasky/blob/7a/config.py https://github.com/rochacbruno/dynaconf
* settings files: https://github.com/xmonader/create-flask-app/blob/master/settings.py
* obj: https://github.com/mjhea0/flaskr-tdd#second-test https://flask.palletsprojects.com/en/0.12.x/tutorial/setup/

* add conf from env
```conf
FLASK_SECRET_KEY=zjvsecret
```
```python
from os import environ

from flask import Flask
from dotenv import find_dotenv, load_dotenv

app = Flask(__name__)
load_dotenv(find_dotenv())
app.config['SECRET_KEY'] = environ["FLASK_SECRET_KEY"]
```

* use conf elsewhere (in app, from shell)
```python
from app import app  # be sure to import the app obj vs. the module (if it's named `app`) https://stackoverflow.com/a/35467302/6813490
app.config['SECRET_KEY']
```

* default config keys (abbreviated; c.f. 'sessions')
```python
{   
    'APPLICATION_ROOT': '/',
    'DEBUG': False,
    'ENV': 'production',  # default i.e. `flask run` calls `load_dotenv()`
    'EXPLAIN_TEMPLATE_LOADING': False,
    'JSON_SORT_KEYS': True,
    'MAX_COOKIE_SIZE': 4093,
    'PERMANENT_SESSION_LIFETIME': datetime.timedelta(days=31),
    'PREFERRED_URL_SCHEME': 'http',
    'SECRET_KEY': None,  # have to set in application code
    'SERVER_NAME': None,
    'TESTING': False,
}
```

## context

🗄 `system.md` proxies

* _context obj_: used by thread for global var e.g. `session`, `request` https://www.youtube.com/watch?v=Z4X5Oddhcc8 [Grinberg 2]
* _app instance_: obj that receives req from WSGI server [Grinberg 1.7]
* `request`: bound to current incoming req i.e. if n threads each has own `request`; can only access w/ active HTTP request i.e. only inside view function
* `session`: store user data https://flask.palletsprojects.com/en/1.1.x/quickstart/#sessions requires secret key https://stackoverflow.com/a/22463969/6813490 use throwaway key for dev, don't regenerate for prod bc then you'll invalidate all sessions in case of app restart https://stackoverflow.com/a/27287455/6813490 https://testdriven.io/blog/flask-server-side-sessions/

## dev server

🗄 `python.md` 'WSGI' `system.md` 'servers'

* config logs https://stackoverflow.com/a/56407222/6813490
* current: `flask run` https://stackoverflow.com/a/52358706 📍 update this answer
* _hot reload_: hot reload only seems to work reliably with `FLASK_DEBUG=1` and even then if err thrown need to restart app to regain reload https://flask.palletsprojects.com/en/1.1.x/cli/#watch-extra-files-with-the-reloader 
* _legacy_: `python app.py` where `appy.py` holds `if __name__ == main: app.run()`
* _debug_: 400 w/ random char in response solved previously by blowing away virtual env
* _Docker_: `CMD flask run --host 0.0.0.0` https://stackoverflow.com/a/43015007/6813490 https://github.com/zachvalenta/docker-flask-skeleton
* _remote machine_: `flask run --host=0.0.0.0` https://askubuntu.com/a/1059748 legacy uses `app.run()` https://stackoverflow.com/a/7027113/6813490 https://flask.palletsprojects.com/en/1.1.x/api/#flask.Flask.run

## Flask SQLAlchemy

🗄 `db.md` ORM/SQLAlchemy
📜 https://flask-sqlalchemy.palletsprojects.com/en/2.x/ https://flask.palletsprojects.com/en/1.1.x/patterns/sqlalchemy/
📺 https://www.youtube.com/playlist?list=PLXmMXHVSvS-BlLA5beNJojJLlpE0PJgCW

* _debug_: https://www.youtube.com/watch?v=5puPZ3n06EE could split config and adjust `flask_debug`, `flask_env`, `sqla_echo`, `record_queries` https://flask-sqlalchemy.palletsprojects.com/en/2.x/config/ https://flask-sqlalchemy.palletsprojects.com/en/2.x/config/
* _events_: `SQLALCHEMY_TRACK_MODIFICATIONS` part of event system (before and after commit) https://flask-sqlalchemy.palletsprojects.com/en/2.x/signals/ turn off to save memory https://flask-sqlalchemy.palletsprojects.com/en/2.x/config/?highlight=sqlalchemy_track_modifications https://stackoverflow.com/a/33790196/6813490
* _impl_: https://stackoverflow.com/questions/14343740/flask-sqlalchemy-or-sqlalchemy
* _initialization_: either `init_app` or `SQLAlchemy` https://stackoverflow.com/q/49388628/6813490 
* _migrations_: https://flask-migrate.readthedocs.io/en/latest/ https://www.youtube.com/watch?v=BAOfjPuVby0 https://github.com/davidism/flask-alembic https://news.ycombinator.com/item?id=26487959 Flask-DB https://www.youtube.com/watch?v=iDTmyF5HZ0Y
* _raw SQL_: `db.engine.execute('<sql>)` https://www.youtube.com/watch?v=FEtJgtmogSY but you probably don't want to do this https://stackoverflow.com/a/22084672/6813490

DDL
* `create_all()`: won't overwrite existing tables https://flask-sqlalchemy.palletsprojects.com/en/2.x/api/#flask_sqlalchemy.SQLAlchemy.create_all https://docs.sqlalchemy.org/en/13/core/metadata.html#sqlalchemy.schema.MetaData.create_all https://github.com/pallets/flask-sqlalchemy/pull/866
* _constraints_: compound PK 1:40 unique 2:15 non null 2:40 `default` and `server_default` 3:15 check 4:50 https://www.youtube.com/watch?v=lnfrcHdE_HI
* _types_: http://flask-sqlalchemy.palletsprojects.com/en/2.x/models/#simple-example

* pagination https://www.youtube.com/watch?v=hkL9pgCJPNk https://flask-sqlalchemy.palletsprojects.com/en/2.x/api/?highlight=pagination#flask_sqlalchemy.Pagination
```python
# ⚠️ only iterates first 8 pages, last two and anything in between gets None https://www.youtube.com/watch?v=hkL9pgCJPNk 9:00, 14:30

things = Thing.query.paginate()  # all pages
thing = Thing.query.paginate(page=42)  # single page

things.pages  # 5 - all
things.per_page  # el per page (defaults to 20)
things.total  # pages * el/page

things.page  # 1 - number of current page
things.next_num  # 2 - number of next page
things.has_prev  # False
things.has_next  # True

things.items # all el from current page
things.items[0]  # first el
```

* DML
```python
# create
artist = Artist(name="Massive Attack")
db.session.add(artist)
db.session.commit()
artist.id  # some attr unavailable until save https://flask-sqlalchemy.palletsprojects.com/en/2.x/queries/#inserting-records

# read
Artist.query.all()  # all
massive_attack = Artist.query.get(42)  # 1
```

---

* queries
```python
# filter https://docs.sqlalchemy.org/en/13/orm/tutorial.html#common-filter-operators https://stackoverflow.com/questions/21674303/flask-sqlalchemy-filters-and-operators
Foo.query.filter_by(username="alice").first()  # by single attr
Foo.query.filter(Foo.attr_bar == 'this', Foo.attr_baz == 'that').first  # by n attr

# join - https://www.youtube.com/watch?v=_HIY1lZKEw0
db.session.query(Performance).join(Song).filter(Song.song_name == query).all()  # https://www.tutorialspoint.com/sqlalchemy/sqlalchemy_orm_working_with_joins.htm
```

* update https://stackoverflow.com/a/6701188/6813490 https://stackoverflow.com/a/7831094/6813490
```python
this_user = session.query(User).filter_by(name='ed').first().update(dict(nickname='eddie')))

that_user = session.query(User).filter_by(name='ed').first()
that_user.nickname = 'eddie'
db.session.commit()
```

* Django-esque
```python
# https://flask-sqlalchemy.palletsprojects.com/en/2.x/api/?highlight=first#flask_sqlalchemy.BaseQuery
get_or_404()
first_or_404()

# get_or_create https://stackoverflow.com/q/2546207/6813490
def get_or_create(self):
    if Thing.query.filter_by(attr=self.attr).first() is None:
        return self.save()
    else:
        return Thing.query.filter_by(attr=self.attr).first()

# save (avoid add + commit everywhere)
class SaveMixin:
    def save(self):
        db.session.add(self)
        db.session.commit()
        return self

class Thing(SaveMixin, db.Model):
    pass

# validation
try:
    thing.validate_attr()
    thing.save()
except Exception:
    return Response("thing `attr` must be boolean", 400)

def validate_attr():
    if not isinstance(self.attr, bool):
        raise Exception
```

## libs

🔍 https://github.com/humiaozuzu/awesome-flask

📉 community in decline https://github.com/mattupstate/flask-security/issues/854 https://github.com/mattupstate/flask-mail/commits/master https://github.com/mgood/flask-debugtoolbar/issues/140

* _CLI_: out-of-box; used to be `flask_script` [Grinberg 2.17] https://www.youtube.com/watch?v=4gRMV-wZTQs
* _debug_: https://github.com/mgood/flask-debugtoolbar/issues/140
* _documentation_: Sphinx https://stackoverflow.com/q/14295322/6813490 Swagger https://realpython.com/flask-connexion-rest-api/ https://github.com/rochacbruno/flasgger 
* _email_: flask-mail seems most popular still in use despite no project updates for 5 years https://stackoverflow.com/q/37058567/6813490 https://github.com/mattupstate/flask-mail https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-xi-email-support could also use AWS SES https://testdriven.io/blog/sending-confirmation-emails-with-flask-rq-and-ses/#workflow
* _forms_: Ekker http://flask.pocoo.org/docs/1.0/patterns/wtforms/
* _security headers_: https://github.com/GoogleCloudPlatform/flask-talisman https://github.com/TypeError/secure.py
* _Stripe_: Herman Janetakis https://testdriven.io/blog/adding-a-custom-stripe-checkout-to-a-flask-app/ https://testdriven.io/blog/accepting-payments-with-stripe-vuejs-and-flask/
* _WebSockets_: seems like the defaults in 2019 are still Grinberg and Reitz from 2014 https://devcenter.heroku.com/articles/python-websockets https://blog.miguelgrinberg.com/post/easy-websockets-with-flask-and-gevent

## REST

🗄 `4-application` 'data transmission'

* _serialization_: basic (`jsonify()`) complex (Marshmallow)
```python
things = [dict(id=x.pk, name=x.name) for x in Thing.query.all()]
```
* bug in `jsonify` ordering https://github.com/pallets/flask/search?q=JSON_SORT_KEYS&unscoped_q=JSON_SORT_KEYS https://flask.palletsprojects.com/en/1.1.x/config/#JSON_SORT_KEYS https://github.com/pallets/flask/issues/2290#issuecomment-302972719 https://github.com/pallets/flask/issues/974#issuecomment-372702841 https://stackoverflow.com/questions/43263356/prevent-flask-jsonify-from-sorting-the-data https://github.com/marshmallow-code/apispec/issues/193#issuecomment-378882771

extensions
* _vanilla_: don't need extension for API dev https://blog.miguelgrinberg.com/post/the-flask-mega-tutorial-part-xxiii-application-programming-interfaces-apis 
* _Flask-Restful_: class-based views https://testdriven.io/courses/microservices-with-docker-flask-and-react/ 
* _Flask RESTPlus_: seems dead https://github.com/noirbizarre/flask-restplus/issues/612 https://stackoverflow.com/a/55152932/6813490) 
* _others_: Connexion, Flask-Classful, flask-apispec, flask smorest https://github.com/marshmallow-code/apispec/issues/193#issuecomment-378882771

* status codes
```python
# basic
return 'This is a 400', 400

# JSON
return jsonify({"id": new_thing.id}))

# JSON w/ non-200 status code https://stackoverflow.com/a/57667079 https://stackoverflow.com/a/45412576
return make_response(jsonify({"id": new_thing.id}), 201)
```

__form__

* req
```Makefile
form:
    http --form POST http://localhost:5000 my_form="form from httpie"
```
```html
<form method=post>
    <input type=text name=my_form>
    <!-- or a file <input type=file name=my_file> -->
    <input type=submit>
</form>
```

* view
```python
@app.route("/", methods=["GET", "POST"])
def form_view():
    # things you can grab: req.form, req.files, req.filename (to check if empty)
    # for file save, have to use werkzeug secure_filename() https://flask.palletsprojects.com/en/1.1.x/patterns/fileuploads/#a-gentle-introduction 
    # and then save() using an os.path, not Pathlib
    user_input = request.form["my_form"]
    if request.method == "GET":  # initial template render
        return render_template('index.html')
    if request.method == "POST":  # re-render template, probably w/ msg flash
        return redirect(url_for('form_view'))
```

* test https://flask.palletsprojects.com/en/1.1.x/testing/#logging-in-and-out
```python
client.post('/api', data={'my_form': 'form from test client'})
```

__query string__

https://www.youtube.com/watch?v=qYeWemghBxI

* req
```Makefile
poetry run http http://localhost:5000/api/performances/7
```

* view
```python
@app.route("/api/performances/<int:id>")
def get_performance_single(id):
    perf = Performance.query.get(id)
```

---

* req
```Makefile
query:
    http http://localhost:5000/api?id=1
```

* view
```python
@app.route("/api")
def my_func():
    my_foo = request.args.get('id')
```

* test
```python
client.get("/api?id=1")
```

__JSON__

* req
```Makefile
json:
    http POST http://localhost:5000 my_json="json from httpie"
```

* view
```python
@app.route("/", methods=["POST"])
def index():
    # request.is_json -> True
    return request.json["my_json"]
```

* test https://flask.palletsprojects.com/en/1.1.x/testing/#testing-json-apis
```python
client.post('/api', json={'my_json': 'json from test client'})
```

## routing

* _view function_: entry point; 'pluggable view' = class-based (like Django) https://flask-restful.readthedocs.io/en/latest/quickstart.html#resourceful-routing
* _methods_: by default routes only accept `GET` so need to add `methods=[]` arg to `@app.route()` annotation
* `.url_map`: attr of app instance holding all routes
* `static`: dir for which route automatically registered in `.url_map` (meaning, any images inside `static` will automatically be served via `/static/<img>`) [Ekker 2.9]

`url_for(func_identifier)`
```html
<!-- https://github.com/zachvalenta/flask-ekker/blob/42d0a97e398c7c8411cbe15b5734ff5d072d89e6/templates/index.html#L9 -->
<div><a href="{{ url_for('index') }}">homepage</a></div>
```
```python
# https://github.com/zachvalenta/flask-ekker/blob/ed7fae635f27f405bfdcdb1a8bde99d82e80aae3/application.py#L58 
from flask import redirect, url_for

@app.route('/home')
def index():
    return render_template('index.html')

@app.route('/gohome')
def go_home():
    return redirect(url_for('home'))
```

## templates

📜 https://jinja.palletsprojects.com/en/2.11.x/templates/

* pass data into template
```python
@app.route('/')
def get_index():
    things = Thing.query.all()
    return render_template('index.html', things=things)
```

* render data in template https://stackoverflow.com/a/9204987/6813490
```html
<tbody>
    {% for thing in things %}
    <tr>
        <td>{{ thing.id }}</td>
        <td>{{ thing.text }}</td>
    </tr>
    {% endfor %}
</tbody>
```

* _syntax_: `{{ var }}` and `{% expression %}` (need this exact spacing inside element or everything breaks)
* _testing_: no way to test if template used w/out extension https://stackoverflow.com/a/40531281/6813490 https://flask.palletsprojects.com/en/1.1.x/signals/#subscribing-to-signals but pretty easy in Django https://stackoverflow.com/a/10614485/6813490
* _var_: takes strings, no matter how they come (obj attr, list index, func call)
* _locating templates_: default is `templates/` at level of app instance but can override in app instance constructor https://stackoverflow.com/a/48040453/6813490
```python
basedir = os.path.abspath(os.path.dirname(__file__))
app = Flask(__name__, static_folder=basedir, template_folder=basedir)
```

display messages by type
```python
flash("this is an error", 'error')
flash("this is an ack")
```
```html
<div id="flashes">
    {% with messages = get_flashed_messages(with_categories=true) %}
        {% if messages %}
            {% for category, msg in messages %}
                {% if category == 'error' %}
                    <mark>{{ msg }}</mark>
                {% else %}
                    <div>{{ msg }}</div>
                {% endif %}
            {% endfor %}
        {% endif %}
    {% endwith %}
</div>
```

## testing

* using app context https://stackoverflow.com/a/17377101/6813490
* _methods_: `.status_code`, `.get_data()`, `.get_json`
* need byte string when asserting against string or JSON value

* hit endpoint
```python
from app import app
client = app.test_client()

def test_get_index_status_200():
    res = client.get("/")
    assert res.status_code == 200
```

* exceptions https://flask.palletsprojects.com/en/1.1.x/api/?highlight=test_client#flask.Flask.test_client
```python
app.testing = True
client = app.test_client()
```
