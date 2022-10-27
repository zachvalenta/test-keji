# TODO

## 参考

📜 https://docs.djangoproject.com/en/stable
🗣 https://djangochat.com/episodes https://forum.djangoproject.com/
🧪 https://github.com/zachvalenta?tab=repositories&q=django

## current

## queue

courses 🗄 `system.md`
* 📙 Vincent beginners
* 📙 Vincent api
* 📙 Vincent professionals
* 🔗 https://www.mattlayman.com/understand-django/
* 📹 https://www.youtube.com/channel/UCRM1gWNTDx0SHIqUJygD-kQ/videos

clean up
* https://mattsegal.dev/
* https://blog.ovalerio.net/archives/2420
* https://adamj.eu/tech/2021/12/08/pre-order-boost-your-django-dx/
* https://github.com/dabapps/django-zen-queries
* group_by https://stackoverflow.com/a/24767207
```sql
select col, count(*) from tab group by col
```
* get query string https://www.django-rest-framework.org/api-guide/filtering/#filtering-against-query-parameters
```txt
http://app.com/foo/?top=10
request.query_params
```
* QS eval @ `.all()` or repr, len, list, bool
> QuerySets are lazy – the act of creating a QuerySet doesn’t involve any database activity. You can stack filters together all day long, and Django won’t actually run the query until the QuerySet is evaluated. https://docs.djangoproject.com/en/3.1/topics/db/queries/#querysets-are-lazy
* check column present: `Foo.objects.filter(col__isnull=False)`
* https://docs.djangoproject.com/en/3.1/topics/db/
* http://blog.abedmaatalla.me/2020/12/django-orm-optimization-tips.html
* https://docs.djangoproject.com/en/3.1/intro/tutorial02/
> each model has a number of class variables, each of which represents a database field in the model.
> You can use an optional first positional argument to a Field to designate a human-readable name. That’s used in a couple of introspective parts of Django, and it doubles as documentation.
```python
pub_date = models.DateTimeField('date published')
```
* _schema_: `create table` statements https://docs.djangoproject.com/en/3.1/intro/tutorial02/
* https://docs.djangoproject.com/en/3.1/intro/tutorial02/#activating-models
* extensions https://monadical.com/posts/django-packages.html
* DRF refresh https://learndjango.com/tutorials/official-django-rest-framework-tutorial-beginners
* DRF https://www.youtube.com/watch?v=06DJBu1zwoY https://www.laceyhenschel.com/blog/2021/2/22/what-you-should-know-about-drf-part-1-modelviewset-attributes-and-methods
* basics: CRUD (seed) CQ (hooks)
* Vincent beginners: re-read chapters 1-3, finish rest of book

## done

* _2021_: rf, DML
* _2020_: basics - CRUD (ORM, serialization, repl) env (conf, Docker) CQ (testing); DRF (views, nested serializers, testing, read_only) basic middleware to 403 req based on IP addr; tutorials https://wsvincent.com/django-rest-framework-tutorial/ https://learndjango.com/tutorials/django-rest-framework-tutorial-todo-api
* _2019_: Osborn hello web app
* _2018_: skim official tutorial and Ekker course, DRF and ORM at work

# AUTH

* keep track of failed logins https://github.com/jazzband/django-axes

Vincent
* basic https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Authentication https://tech.marksblogg.com/passwords-in-django.html
* login/out https://learndjango.com/tutorials/django-login-and-logout-tutorial
* signup https://learndjango.com/tutorials/django-signup-tutorial
* reset https://learndjango.com/tutorials/django-password-reset-tutorial
* with email https://learndjango.com/tutorials/django-log-in-email-not-username

__approaches__ 搜 'Re: TestDriven.io - new feedback message'

* built-in https://wsvincent.com/django-user-authentication-tutorial-login-and-logout/ 
* registration-redux [Osborn 1.10] 
* all-auth https://wsvincent.com/django-allauth-tutorial/ https://learndjango.com/tutorials/django-allauth-tutorial
* email https://wsvincent.com/django-login-with-email-not-username/
* this https://github.com/aaugustin/django-sesame

❓ where does Django look to resolve calls to url pattern names besides `urls.py`? re: https://github.com/zachvalenta/hello-django1/commit/0cd06134c640fb67df03d8f0a54fcb61925b0faa `password_reset_confirm` calls internal urlpattern named `password_reset_complete`; even if we specify a url pattern named `password_reset_complete` in `urls.py` Django will still route to its own internal url pattern of this name (figured out bc when I was following Osborn on reset complete the url route still changed to `accounts/password/reset/complete` vs. her route `accounts/password/complete`)

## built-in

* _convention > conf_: Django will serve your templates provided they are in `templates/registration` and have the expected name, otherwise will serve its own default https://github.com/zachvalenta/hello-django1/commit/6503b460490fb85f085f3a277fbdd80360291fa0

* `pw_reset_form.html`: prompt email to send reset link [Osborn 72]
* `pw_reset_done.html`: ack of email sent
* `pw_reset_email.txt`: email user link to reset
* `pw_reset_confirm.html`: input new pass; doesn't seem to do any validation re: proximity to previous pw
* `pw_reset_complete.html`: ack new

## registration-redux

* sequence diagram
```
title Django auth flows w/ Registration Redux

group #orange change (logged in)
client->server:req reset
note right of server:validate
note right of server:update db
client<-server:ack
end

group #pink reset (can't login)
client->server:req reset
note right of server:update db
client<-server:email

group #lightgreen registration (new user)
client->server:input credentials
note right of server:validate
note right of server:update db (if not part of reset)
client<-server:ack
end

end
```

---

* _routes_: Registration Redux owns everything under `accounts/` except when overridden by built-in auth [Osborn 1.10.69]

__flow__

💡 this is a mix of Registration Redux and Django's built-in auth

* _registration_: `base.html` links to pattern name `registration_register` which is owned by Registration Redux, so clicking that matches the route to which the pattern name is mapped (`accounts/register`) and invokes that pattern's view, which handles the validation logic
* _login_: `base.html` links to pattern name `auth_login` (route `/accounts/login`) which is owned by Registration Redux, so it calls its own view and renders `registration/login.html` (if we've placed that template in that directory location, that is) --> `login.html` on POST will be handled by the same RR view that renders its GET and if successful will redirect to whatever we've specified in `settings.py/LOGIN_REDIRECT_URL` [Osborn 65]
* _reset_: `login.html` also kicks off our reset flow with a link to pattern name `password_reset`, which sends out an email using `pw_reset_email.txt` and then calls ` password_reset_done`, which just renders a template to ack; when the user follows the link they've been emailed they'll hit the `password_reset_confirm` view and if their guid is still valid that view will render `password_reset_confirm.html` and allow them to input a new pw (idk if same view is used for validation or if separate validation -only view is hit e.g. doesn't care about link validity) and if everything goes well 

__registration-redux__

💡 RR is just view impl validation logic, so templates need to conform to RR names so that their views can render 

* _Osborn chapter 10_: `templates/registration/registration_form.html` and `registration_complete.html` are unnecessary, `/accounts/register` is owned by Registration Redux, we link to it from our `base.html` but after that RR calls its own view and renders its own templates, neither of which are overriden by the aforementioned ones
* _migrations_: let RR know about your user models
* _URLs_: add base domain to `urls.py` and reference subdomain URL pattern names in templates e.g. `base.html/auth_logout`
* _views_: you don't interact with these, but presumably implement password constraint validation 

## users

🗄 `security.md` users

* custom user model https://brntn.me/blog/six-things-i-do-every-time-i-start-a-django-project/
* https://simpleisbetterthancomplex.com/article/2021/07/08/what-you-should-know-about-the-django-user-model.html
* groups https://github.com/bennylope/django-organizations
* automate admin user creation https://stackoverflow.com/a/26091252
* mimic user's account https://www.mattlayman.com/blog/2020/hijack-to-help-customers/
* referencing user model https://learndjango.com/tutorials/django-best-practices-referencing-user-model
* _default_: `AbstactUser` + `PermissionsMixin` https://www.youtube.com/watch?v=458KmAKq0bQ @ 14:10 follows first-last antipattern 🗄 `db.md` 'modeling' https://www.youtube.com/watch?v=458KmAKq0bQ
* `AbstractUser`: everything from default user model except `PermissionsMixin`
* `AbstractBaseUser`: gives you pw and last_login, necessary for pw refresh tokens https://www.youtube.com/watch?v=458KmAKq0bQ @ 14:00 
* _custom model_: use from start, harder to bolt on afterwards https://blog.doismellburning.co.uk/django-an-unofficial-opinionated-faq/ https://learndjango.com/tutorials/django-custom-user-model https://learndjango.com/tutorials/django-custom-user-model
* _permissions_: https://learndjango.com/tutorials/django-best-practices-user-permissions https://wsvincent.com/django-tips-user-permissions/ https://coderbook.com/@marcus/how-to-restrict-access-with-django-permissions https://testdriven.io/blog/drf-permissions/
* _sink_: https://testdriven.io/blog/django-custom-user-model/ https://wsvincent.com/django-referencing-the-user-model/ https://wsvincent.com/django-custom-user-model-tutorial/ https://wsvincent.com/django-tips-custom-user-model https://testdriven.io/blog/django-custom-user-model/ https://www.roguelynn.com/words/django-custom-user-models/

# DB

📜 https://docs.djangoproject.com/en/3.2/#the-model-layer
🔍 https://books.agiliq.com/projects/django-orm-cookbook/en/latest/

how to
* catch dirty model instances https://github.com/romgar/django-dirtyfields
* anonymize data https://github.com/Tesorio/django-anon
* audit table https://github.com/jazzband/django-simple-history
* graph ER model https://github.com/meshy/django-schema-graph/
* generate view from queryset https://schinckel.net/2020/03/03/postgres-view-from-django-queryset

## design

🗄 `db.md` ORM

transactions 🗄 `db.md` consistency
* enter atomic context:	`START TRANSACTION`
* exit atomic context w/out exception: `COMMIT`
* exit atomic context w/ exception: `ROLLBACK`
* default is autocommit mode i.e. "Each query is immediately committed to the database, unless a transaction is active." https://docs.djangoproject.com/en/3.2/topics/db/transactions/#django-s-default-transaction-behavior
* there is much more to learn https://charemza.name/blog/posts/django/postgres/transactions/not-as-atomic-as-you-may-think/

flow http://lucumr.pocoo.org/2011/7/19/sqlachemy-and-you/
* generates SQL
* exec
* deserialize result set into Py obj
* update/save Py obj in mem
* `UPDATE` in SQL

misc
* _F expression_: perform SQL operation without serializing data into Python obj first https://docs.djangoproject.com/en/3.1/ref/models/expressions/#f-expressions
* lazy evaluation https://docs.djangoproject.com/en/3.1/topics/db/queries/#querysets-are-lazy https://davit.tech/django-queryset-examples/#section-contents
```python
qs = Foo.objects.all()  # no eval
qs.filter(foo='foo val')  # no eval
qs.values_list  # eval on queryset access
```
* more focused on application logic than SQLAlchemy http://jmoiron.net/blog/about-sqlalchemy-and-djangos-orm/
```python
# SQLAlchemy - SQL
session.query(Book).join(Book, Author).filter(Author.age==27)
# Django - objects
Book.objects.filter(author__age=27)
```

## admin

* https://news.ycombinator.com/item?id=30321330
* db GUI [Osborn 1.6.37]
* _Django SQL Dashboard_: datasette + visualization
* styling won't work unless `debug=True` https://stackoverflow.com/a/50868962
* register model w/ `admin.py` https://books.agiliq.com/projects/django-admin-cookbook/en/latest/
* for analytics https://github.com/otto-torino/django-baton
* config color https://www.dothedev.com/blog/django-admin-change-color/ https://realpython.com/customize-django-admin-python/ https://github.com/farridav/django-jazzmin https://www.mattlayman.com/understand-django/administer-all-the-things
* config timezone https://til.simonwillison.net/django/show-timezone-in-django-admin

## DDL

* create uuid for record for API https://0of1.com/blog/posts/django-staples/
* phone numbers https://0of1.com/blog/posts/django-staples
* make everything read-only https://github.com/adamchainz/django-read-only
* multi-table inheritance https://monadical.com/posts/django-packages.html
* _custom fields_: https://docs.djangoproject.com/en/dev/howto/custom-model-fields/
* _index_: `db_index=True` https://www.djangorocks.com/snippets/indexing-your-django-models.html without downtime https://realpython.com/create-django-index-without-downtime/ https://adamj.eu/tech/2020/07/27/how-to-modernize-your-django-index-definitions
* _meta_: anything that's not a field
* _PK_: uuid https://docs.djangoproject.com/en/dev/ref/models/fields/#uuidfield https://books.agiliq.com/projects/django-orm-cookbook/en/latest/uuid.html https://books.agiliq.com/projects/django-orm-cookbook/en/latest/slugfield.html

* related_name and 1-M https://books.agiliq.com/projects/django-orm-cookbook/en/latest/one_to_many.html https://docs.djangoproject.com/en/dev/ref/models/fields/#django.db.models.ForeignKey.related_name 🗄 
```python
class Parent(models.Model):

# no change to underlying table
+-----+----------+--------------+---------+------------+----+
| cid | name     | type         | notnull | dflt_value | pk |
+-----+----------+--------------+---------+------------+----+
| 0   | id       | integer      | 1       | <null>     | 1  |
| 1   | name     | varchar(255) | 1       | <null>     | 0  |
+-----+----------+--------------+---------+------------+----+
# gets virtual column from related_name
Parent.objects.get(pk=1).children.all()  # <QuerySet [id: 1, id: 2]>
Parent.objects.get(pk=1).children.get(pk=3).child_field  # nested lookups

class Child(models.Model):
    # unlike SQLAlchemy, both FK and backref go on child
    parent = models.ForeignKey(Parent, on_delete=models.CASCADE, related_name='children')

# FK = adds constraint via column on underlying table
# unlike Flask column name seems autogenerated
+-----+-----------+---------+---------+------------+----+
| cid | name      | type    | notnull | dflt_value | pk |
+-----+-----------+---------+---------+------------+----+
| 0   | id        | integer | 1       | <null>     | 1  |
| 1   | parent_id | integer | 1       | <null>     | 0  |
+-----+-----------+---------+---------+------------+----+
# constraint
Child.objects.create(parent_id=1)
# physical column reflected in ORM obj
Child.objects.get(pk=2).parent_id  # 1
# but also gets virtual column as well
Child.objects.get(pk=2).parent_id  # name is parent_name_one
```

* fields
```python
class Post(models.Model):

    # PRIMARY KEY
    # pk: instance attr, regardless of whether self-defined or auto-defined by Django https://docs.djangoproject.com/en/3.0/ref/models/instances/#the-pk-property
    # id: instance attr if auto-defined by Django

    # JSON / JSONField
    # 3.1 - works for all supported db backends https://docs.djangoproject.com/en/3.1/releases/3.1/#jsonfield-for-all-supported-database-backends but requires installing extesion for sqlite https://docs.djangoproject.com/en/3.1/ref/models/fields/#django.db.models.JSONField 🗄 `linux.md` SQLite extension and DYLD_LIBRARY_PATH; I had to use this 3rd party pkg https://pypi.org/project/jsonfield/
    # ^3.0 - Postgres only https://docs.djangoproject.com/en/3.0/ref/contrib/postgres/fields/#jsonfield
    # alternatives: TextField https://stackoverflow.com/q/48172299/6813490 ArrayField (Postgres-only) https://stackoverflow.com/a/44630696
    # edit from admin https://github.com/jmrivas86/django-json-widget

    # TYPES
    title = models.CharField(max_length=50)  # length limit
    content = models.TextField()  # no length limit

    # VALIDATION 
    # https://www.b-list.org/weblog/2006/jun/28/django-tips-difference-between-blank-and-null/ https://simpleisbetterthancomplex.com/tips/2016/07/25/django-tip-8-blank-or-null.html
    # both default to False
    # use case for blank and not null is value will be created after form validation
    author = models.TextField(null=True)  # nullable
    editor = models.TextField(blank=True)  # form validation

    # TIME
    created_at = models.DateTimeField(auto_now_add=True)  # current time on instance creation
    updated_at = models.DateTimeField(auto_now=True)  # current time on instance save
```

## DML

clean up
* select related, prefetch related https://www.youtube.com/watch?v=TzgZBg7oXNA
* use count instead of len() https://docs.djangoproject.com/en/3.2/ref/models/querysets/#django.db.models.query.QuerySet.count
* https://dev.to/amitness/django-orm-if-you-already-know-sql-k80
* https://davit.tech/django-queryset-examples/#section-comparsion
* prefetch https://www.laac.dev/blog/five-common-django-mistakes
* https://chriswedgwood.com/blog/htmx-with-django-example-2-bulk-update/

lookups
* https://docs.djangoproject.com/en/3.1/topics/db/queries/#lookups-that-span-relationships
* are Django lookups joins or subqueries? https://mattrobenolt.com/the-django-orm-and-subqueries/ https://stackoverflow.com/questions/8556297/how-to-subquery-in-queryset-in-django https://docs.djangoproject.com/en/3.1/ref/models/expressions/#subquery-expressions

```python
###
# LOOKUP = where clause https://docs.djangoproject.com/en/3.1/topics/db/queries/#field-lookups
###

# defaults to __exact
get(id__exact=14)  # explicit form
get(id=14)  # __exact implied
get(id__iexact=14)  # ILIKE https://docs.djangoproject.com/en/3.1/ref/models/querysets/#iexact

filter(name__contains='hello')  # LIKE '%foo%'
filter(id__in=group)  # membership
filter(date_joined__range=[start, end])  # range https://davit.tech/django-queryset-examples/#section-between

all()[:10]  # limit https://davit.tech/django-queryset-examples/#section-limit
order_by('name')  # order by

Entry.objects.filter(blog__name='beatles blog') # https://docs.djangoproject.com/en/3.1/topics/db/queries/#lookups-that-span-relationships
select * from entry where blog_id in 
    (select id from blog where name = 'beatles blog')

# ManyRelatedManager also used for joins? need to call all()
Foo.objects.get(name="bar").m2m.all()

###
# GET/UPDATE
### 

* `first()` isn't appropriate if you're querying for a unique obj, use `get()`

# get
filter(name='foo')  # queryset
get(name='foo')  # single instance but errs if None or n 
filter(name='foo').first()  # return 1 or None https://stackoverflow.com/a/3090342
get(name="foo_key").json_col["bar_key"]  # single instance but errs if None or n 

# update
get_or_create()
create(name="name", desc="desc")  # returns tuple of instance/bool
foo.save()  # update
```

misc
* _queryset_: collection of model instances
* _manager_: default name is `.objects` but can rename by using custom manager https://docs.djangoproject.com/en/3.1/topics/db/managers/#custom-managers
* _flush_: rm data (won't change schema) https://docs.djangoproject.com/en/3.1/ref/django-admin/#flush
* _meta_: https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Testing https://docs.djangoproject.com/en/3.1/ref/models/meta/
* view SQL from query: `all().query()` https://stackoverflow.com/a/1074224 `shell_plus --print-sql` https://davit.tech/django-queryset-examples/#section-bonus-tip
* rm obj: mask it instead https://github.com/makinacorpus/django-safedelete

## migrations

🗄 `db.md` migrations

```sh
migrate <app> <num>  # rollback
migrate <app>        # reapply
```
clean up
* https://docs.djangoproject.com/en/3.0/howto/initial-data/
* https://github.com/Brobin/django-seed https://eli.thegreenplace.net/2014/02/15/programmatically-populating-a-django-database
* https://eli.thegreenplace.net/2014/02/20/clearing-the-database-with-django-commands
* https://www.mattlayman.com/blog/2020/django-testing-toolbox/
* https://jefftriplett.com/2020/how-do-i-test-1000-objects-in-django https://github.com/model-bakers/model_bakery
* https://kite.com/blog/python/django-database-migrations-overview/ https://realpython.com/django-migrations-a-primer https://realpython.com/digging-deeper-into-migrations/
* https://www.mattlayman.com/understand-django/test-your-apps/

schema (DDL) migrations
* downtime https://pankrat.github.io/2015/django-migrations-without-downtimes/
* prevent autonaming https://adamj.eu/tech/2020/02/24/how-to-disallow-auto-named-django-migrations/ 

data (DML) migrations
* https://docs.djangoproject.com/en/dev/topics/migrations/#data-migrations

fixture
* https://realpython.com/django-pytest-fixtures/
* https://docs.djangoproject.com/en/3.1/topics/testing/tools/#django.test.TransactionTestCase.fixtures
* https://docs.djangoproject.com/en/3.0/howto/initial-data/#providing-data-with-fixtures

factory
* 

factory-light
```python
class YourTestClass(TestCase):
    @classmethod
    def setUpTestData(cls):
        print("setUpTestData: Run once to set up non-modified data for all class methods.")
        pass

    def setUp(self):
        print("setUp: Run once for every test method to setup clean data.")
```

misc
* create migration file manually `manage.py makemigrations --empty <app> --name <migration>`
* view migration file as SQL `manage.py sqlmigration <app> <migration>`
* squash migration files for feature branch: rm files and re-run `makemigrations` https://stackoverflow.com/a/40029119
* squash migration files for cleaning up codebase: `squashmigrations` https://docs.djangoproject.com/en/stable/topics/migrations/#squashing-migrations
* internals https://www.youtube.com/watch?v=u6cVvbuUzlk https://speakerdeck.com/andrewgodwin/migrations-under-the-hood

---

rollback
* _revert_: rm latest, wipe db, apply previous migrations, seed db; impl might be `DELETE FROM django_migrations where id=<id>`
* _rollback_: `migrate <app> <num>`; `migrate <app> zero` https://docs.djangoproject.com/en/dev/topics/migrations/#reversing-migrations 
* _non-autogenerated name_: `--name` https://docs.djangoproject.com/en/dev/ref/django-admin/#makemigrations
* not everything can be reversed https://stackoverflow.com/q/63123919
* can use something like RemoveField under the hood https://stackoverflow.com/q/63123919

misc
* _ordering issues_: make db changes on local, generate a new migration script `001-foo`, at some later point pull in `develop` and there's already `001-bar` migration and Django complains about `001-foo`, solve by rm `001-bar` and running `make makemigrations` then `make migrate`

# API

## middleware

📜 https://docs.djangoproject.com/en/3.1/topics/http/middleware/

* hook in req/res cycle
* middleware obj takes req and return res
* can put anywhere in your src
* used in logging?
* called in order of elements in `MIDDLEWARE` in `settings.py` https://docs.djangoproject.com/en/3.1/topics/http/middleware/#middleware-order-and-layering

```python
# api/middleware.py
class Safelist:
    def __init__(self, get_response):
        self.get_response = get_response
    def __call__(self, request):
        print("BEFORE VIEW")
        response = self.get_response(request)
        print("AFTER VIEW")
        return response

# settings.py
MIDDLEWARE = [
    'api.middleware.Safelist',
]
```

restrict requests by IP
* DRF https://www.django-rest-framework.org/api-guide/permissions/ https://www.laurencegellert.com/2019/04/django-rest-framework-how-to-whitelist-safelist-ip-addresses/
* middleware https://riptutorial.com/django/example/6909/middleware-to-filter-by-ip-address https://stackoverflow.com/questions/12383540/authenticate-by-ip-address-in-django
* Nginx https://stackoverflow.com/a/20831562/6813490
```python
class IPSafelist:
    safe = os.getenv("SAFELIST")

    def __init__(self, get_response):
        self.get_response = get_response

    def __call__(self, request):
        print(f"\nreq sent from: {request.META['REMOTE_ADDR']}\n")  # https://stackoverflow.com/a/12384539
        if not request.META["REMOTE_ADDR"] == self.safe:
            return HttpResponseForbidden()
        response = self.get_response(request)
        return response
```

---

https://www.youtube.com/watch?v=3yKuKQ2fuys

* provides thread info (req, user) to app components that otherwise wouldn't have access

* `MIDDLEWARE = []`: everything inside called on each request
```python
from threading import local

_thread_locals = local()

def get_current_request():
    return getattr(_thread_locals, 'request', None)

def get_current_user():
    request = get_current_request()
    if request:
        user = getattr(request, 'user', None)
        if isinstance(user, User):
            return user
```

## serialization

🗄 `system.md` serialization `python.md` serialization
🔗 https://books.agiliq.com/projects/django-api-polls-tutorial/en/latest/

```python
###
# DRF https://www.django-rest-framework.org/api-guide/serializers/ https://testdriven.io/blog/drf-serializers/
###

# basics
class PostSerializer(serializers.ModelSerializer):
    class Meta:
        model = models.Post
        fields = ('id', 'title', 'content')  # defaults to __all__ https://www.django-rest-framework.org/api-guide/serializers/#specifying-which-fields-to-include

class FooView(generics.ListViewAPI):
    queryset = Post.objects.all()
    serializer_class = PostSerializerer

# type flow
from rest_framework.renderers import JSONRenderer
foo = Foo.objects.get(id=1)  # model instance
foo_serial = FooSerializer(foo)  # DRF instance
foo_serial.data  # DRF typed dict
JSONRenderer().render(foo_serial.data)  # byte string

# read_only = shows up in GET but not required for POST https://www.django-rest-framework.org/api-guide/serializers/#specifying-read-only-fields
from rest_framework.serializers import BooleanField
class FooSerializer(ModelSerializer):
    success = BooleanField(read_only=True)
    class Meta:
        fields = ['foo', 'bar', 'success']
        model = FooModel

###
# vanilla https://docs.djangoproject.com/en/3.0/topics/serialization/
###

from django.core import serializers
from django.http import JsonResponse
JsonResponse({"things" : list(Things.objects.all())})  # https://www.youtube.com/watch?v=dfIF7qDDbW8& 14:30
serializers.serialize("things", Thing.objects.all())

# add field to payload before deserialize
class Serializer:
    def to_internal_value(self, data): 
        data['foo'] = 'foo content' 
        return super().to_internal_value(data)
```

DRF
* serialization can be expensive, can drop when you need perf https://hakibenita.com/django-rest-framework-slow
* exclude field https://www.django-rest-framework.org/community/3.4-announcement/#use-fields-or-exclude-on-serializer-classes
* fields defaults to string https://www.django-rest-framework.org/tutorial/1-serialization/#creating-a-serializer-class
* dataclasses https://github.com/oxan/djangorestframework-dataclasses
* similar to Django forms
```python
class Thing(models.Model):
    name = models.CharField(max_length=255)
    description = models.TextField()
    slug = models.SlugField(unique=True)

class ThingForm(ModelForm):
    class Meta:
        model = Thing
        fields = ('name', 'description')

if request.method == 'POST':
    form = ThingForm(data=request.POST, instance=thing)
    if form.is_valid():
        form.save()
        return redirect('thing_detail', slug=thing.slug)
```

nested
* `StringRelatedField` https://www.django-rest-framework.org/api-guide/relations/#stringrelatedfield https://stackoverflow.com/questions/31936401/string-related-field-in-djangorest https://github.com/zachvalenta/django-crud/commit/f0e1b0b4be18289d807e6b012c1ecc11cfa545ef#diff-39f8266a93579ae5dbdb3790c2bfda58R6
* GET nested attr e.g. `parent/1/children` https://www.django-rest-framework.org/api-guide/relations/#custom-hyperlinked-fields https://stackoverflow.com/questions/62156484/drf-create-object-with-nested-serializers-and-foreign-keys
* POST parent and child: impl `create()` https://www.django-rest-framework.org/api-guide/relations/#writable-nested-serializers
```json
{
    "parent_field": "foo val",
    "children": [
        {
            "child_field": "foo val"
        }
    ]
}
```

## URLs

howto
* show all: django-extensions + `manage.py show_urls` https://stackoverflow.com/a/8844834
* split into n modules https://stackoverflow.com/q/26047610
```python
# parent module
urlpatterns = patterns(
    # child module = /src/api.urls.py
    url(r'^api', include('src.api.urls')),
)
```

wiring
* each urlpattern iterated, first match returned
* if call from DTL link, looks for name as opposed to route https://docs.djangoproject.com/en/2.2/topics/http/urls/#how-django-processes-a-request

---

* wiring
```python
from django.urls import path  # create URL obj
from django.urls import include  # point to app-level URLs

urlpatterns = [
    # syntax: route - view - name [Osborn 1 10.64]

    # function-based
    path('', func_views.foo, name='foo_func'),  # use kwarg for name https://stackoverflow.com/a/19670235/6813490 [Osborn 1 4.14]
    # class-based
    path('', ClassView.as_view(), name='bar_class'),
    # template-only https://wsvincent.com/django-about-page-three-ways/
    url(r'^about/', TemplateView.as_view(template_name='about.html'), name='about'),
]

# URL forwarding
return redirect('thing_detail', slug=thing.slug)
path('thing/<slug>', views.thing_detail, name='thing_detail'),
```

---

* public facing IDs https://spikelantern.com/articles/options-for-public-facing-ids-in-django
* _trailing slash_: if URL has trailing slash but user/browser doesn't input Django will 301 to correct URL via `APPEND_SLASH` https://learndjango.com/tutorials/trailing-url-slashes-django
```makefile
# n.b. these URLs don't need trailing slash bc: req via Chrome, Django 301, Chrome redirect
gui:
	open $(api_url)/
```
* `urlpatterns`: ways to map to view; more accurate to think of this way than simply 'URLs' bc actually two ways to map to view (URL, pattern name) and DTL links dont' even need the patterns URL to perform lookups (will still interpolate query string KV pairs but otherwise the FQDN kinda incidental here)
* _why named URL pattern?_ modularity; can change internal naming without update links for external consumers
* `urls.py`: manifest of all routes; project-level
* _slug_: to preserve URLs for external links, auto-generated slugs won't change when attr used for generation update [Osborn 1 9.57, 61] https://learndjango.com/tutorials/django-slug-tutorial
* _methods_: `render()` take files `redirect()` take URL name `url` take URL name
* can override built-in admin templates when using built-in views [Osborn 1.10.73]

## views

🔗 https://spookylukey.github.io/django-views-the-right-way/

status codes
* 200: `HttpResponse` https://docs.djangoproject.com/en/3.1/ref/request-response/#httpresponse-objects
* 500: `HttpResponseServerError` https://docs.djangoproject.com/en/3.1/ref/request-response/#django.http.HttpResponseServerError `Response(content, status=status.HTTP_500_INTERNAL_SERVER_ERROR)` https://www.django-rest-framework.org/api-guide/status-codes/#server-error-5xx

DRF http://www.cdrf.co/ https://www.django-rest-framework.org/api-guide/views/
* setup: register DRF with project, register model with serializer, use serializer in view, urls (map to views, register w/ project)
* _view_: handles impl for HTTP method(s)
* _viewset_: collection of views; designed to be used with routers vs. explicit URLs https://www.django-rest-framework.org/tutorial/6-viewsets-and-routers/
* _ListAPIView_: GET all
* _ListCreateAPIView_: GET all, POST single
* _RetrieveAPIView_: GET single
* _RetrieveUpdateDestroyAPIView_: GET/PUT/PATCH/DELETE single
* _ModelViewSet_: combination of ListCreateAPIView and RetrieveUpdateDestroyAPIView

vanilla https://wsvincent.com/class-function-based-views/
* _function-based_: route on control flow
* _class-based_: route on method sig https://docs.djangoproject.com/en/2.2/topics/class-based-views/
* _generic class-based_: 类似 DRF views http://ccbv.co.uk/
```python
###
# FBV
###

def index(request):
    if request.method == 'GET':
        return HttpResponse("GET")
    elif request.method == 'POST':
        return HttpResponse("POST")

###
# CBV
###

class PollsViews(View):
    def get(self, request):
        return HttpResponse("GET")
    def post(self, request):
        return HttpResponse("POST")

###
# GCBV
###

# single entity
class DetailView(generic.DetailView):
    model = Question
    template_name = 'polls/detail.html'

# all entities
class IndexView(generic.ListView):
    template_name = 'polls/index.html'
    context_object_name = 'latest_question_list'
    def get_queryset(self):
        return Question.objects.order_by('-pub_date')[:5]
```

# ZA

* alternatives https://github.com/vitalik/django-ninja https://news.ycombinator.com/item?id=30221016
* _signals_: send message before/after somethings been done, pass info btw separate Django apps (pre/post-save) https://stackoverflow.com/a/17658156 hooks as replacement https://monadical.com/posts/django-packages.html
* watchman instead of django file watcher https://adamj.eu/tech/2021/01/20/efficient-reloading-in-djangos-runserver-with-watchman/
* more reload https://github.com/adamchainz/django-browser-reload
* example codebasees https://github.com/python/pythondotorg
* support for old versions https://www.codestasis.com/
* GraphQL https://github.com/PaulGilmartin/graph_wrap

shell
* run script: `./manage.py shell < myscript.py` https://stackoverflow.com/a/16853799
* run script w/ env: https://django-extensions.readthedocs.io/en/latest/runscript.html https://www.b-list.org/weblog/2007/sep/22/standalone-django-scripts/
* autload models: `poetry run python manage.py shell_plus --bpython` https://django-extensions.readthedocs.io/en/latest/shell_plus.html
* `dbshell`: passes env var from `settings.py` to default CLI for dbms; https://github.com/dbcli/pgcli.com/blob/2f7a5aac0a9f5fa81670019301a12e9394a416da/content/django-pgcli.md 

dev server on remote
* start cmd: `python manage.py runserver 0.0.0.0:8000`
* `ALLOWED_HOSTS`: if running on server need to add hostname; `localhost` seems to be implicit https://docs.djangoproject.com/en/dev/ref/settings/#allowed-hosts https://stackoverflow.com/a/46443432/6813490
* Docker: set `DEBUG=False` https://stackoverflow.com/a/60832028

static/media files
* `collectstatic`: rifle through `static` of each app and copy assets to project-level `static` https://www.smashingmagazine.com/2020/06/django-highlights-wrangling-static-assets-media-files-part-4/
* default is app-level `static` dir but everyone uses project-level directory `static` dir
* in production: WhiteNoise handles first request and subsequent hit Cloudflare cache https://runninginproduction.com/podcast/4-real-python-is-one-of-the-largest-python-learning-platforms-around#49:30 S3 https://0of1.com/blog/posts/django-staples/ https://testdriven.io/blog/storing-django-static-and-media-files-on-amazon-s3/ https://www.youtube.com/watch?v=E613X3RBegI more cache https://testdriven.io/blog/django-low-level-cache https://news.ycombinator.com/item?id=30324608
```python
# this is where admin static images are located -> django/contrib/admin/static/admin/img/icon-addlink.svg
# idk how it works but maybe something to do with installed_apps
INSTALLED_APPS = [
    "django.contrib.admin",
    "django.contrib.staticfiles",
]
```

security https://snyk.io/blog/django-security-tips
* throttle auth
* don't use raw queries
* cookies over HTTPS
* no user uploads
* mv admin url from `/admin/`; csrf = necessary for stuff w/ `POST` [📙 Osborn 1 9.59] 
* https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/web_application_security
* https://www.mattlayman.com/understand-django/secure-apps
* https://www.ponycheckup.com/ https://www.youtube.com/watch?v=8W4MGggwgfM https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/web_application_security generate secret key https://humberto.io/blog/tldr-generate-django-secret-key https://github.com/jamesturk/django-honeypot https://learndjango.com/tutorials/django-search-tutorial

community
* creators: Simon https://news.ycombinator.com/user?id=simonw Adrian https://www.soundslice.com/ Jacob https://jacobian.org/ Andrew Godwin (did south and migrations)
* _DSF_: admin https://wsvincent.com/how-django-works-behind-the-scenes/ 501 non-profit https://www.b-list.org/weblog/2018/nov/20/core/
* _DEP_: PEP for Django https://github.com/django/deps
* _fellows_: paid devs https://www.b-list.org/weblog/2018/nov/20/core/
* _technical board_: engineering; replaced core teams https://jacobian.org/2020/mar/12/django-governance/

structure
* `django-admin`: CLI for project https://docs.djangoproject.com/en/3.0/ref/django-admin/
* `manage.py`: CLI for app https://docs.djangoproject.com/en/3.0/ref/django-admin/
* _project_: thing w/ settings.py https://stackoverflow.com/q/50090341 create (`django-admin startproject <name> .`)
* _app_: unit of functionality
* check https://docs.djangoproject.com/en/3.0/ref/django-admin/#check https://hakibenita.com/automating-the-boring-stuff-in-django-using-the-check-framework
* different ways to structure https://learndjango.com/tutorials/hello-world-5-different-ways

apps
* create `django-admin startapp <name>` https://hellowebbooks.com/setup/ `python manage.py startapp <name>` https://djangoforbeginners.com/hello-world/
* multiple ways to register app with project https://learndjango.com/tutorials/django-rest-framework-tutorial-todo-api https://wsvincent.com/django-rest-framework-tutorial/
* naming conventions https://stackoverflow.com/a/3101894
* people are too keen to make everything an app https://news.ycombinator.com/item?id=26492043
* API in own app https://learndjango.com/tutorials/django-rest-framework-tutorial-todo-api in main app https://wsvincent.com/django-rest-framework-tutorial/

## config

📜 https://docs.djangoproject.com/en/stable/topics/settings/ https://docs.djangoproject.com/en/stable/ref/settings/ https://www.mattlayman.com/understand-django/settings/

* `settings.py`: just a Python module w/ buncha attributes; fmt installed apps same as imports https://wsvincent.com/django-rest-framework-tutorial/ uses pathlib as of 3.1 https://learndjango.com/tutorials/whats-new-django-31
* use OS https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Deployment
* django-environ https://github.com/joke2k/django-environ
* python-dotenv https://www.untangled.dev/2020/05/31/django-environment-variables/

```conf
# dev
ENV=dev
SQLITE_DB_FILE="local.db"

# prod
ENV=prod
HOST=db
PORT=5432
NAME=postgres
USER=postgres
PASSWORD=postgres
```
```python
# https://learndjango.com/tutorials/django-docker-and-postgresql-tutorial
from dotenv import load_dotenv
load_dotenv()
if os.getenv("APP_ENV") == "dev":
    DEBUG = True
    DATABASES = {
        "default": {
            "ENGINE": "django.db.backends.sqlite3",
            "NAME": os.path.join(BASE_DIR, os.getenv("SQLITE_DB_FILE"))
        }
    }
if os.getenv("APP_ENV") == "prod":
    DEBUG = False
    DATABASES = {
        "default": {
            "ENGINE": 'django.db.backends.postgresql',
            "HOST": os.getenv("HOST"),
            "PORT": os.getenv("PORT"),
            "NAME": os.getenv("NAME"),
            "USER": os.getenv("USER"),
            "PASSWORD": os.getenv("PASSWORD"),
        }
    }
```

## libs

🔍 https://learndjango.com/tutorials/essential-django-3rd-party-packages

* _3rd-party apps_: anything installed by adding to `settings.py/INSTALLED_APPS` https://djangopackages.org https://realpython.com/installable-django-app/
* _analytics_: https://github.com/jazzband/django-analytical
* _backups_: https://github.com/django-dbbackup/django-dbbackup
* _caching_: https://wsvincent.com/django-caching-for-beginners/ https://eralpbayraktar.com/blog/django/2020/caching-with-django
* _channels_: https://www.aeracode.org/2018/06/04/django-async-roadmap/ https://testdriven.io/blog/django-async-views/ https://www.youtube.com/watch?v=j6IOuD5WD8c https://testdriven.io/courses/real-time-app-with-django-channels-and-angular/ https://testdriven.io/courses/real-time-app-with-django-channels-and-angular kinda live Phoenix LiveView? https://github.com/edelvalle/reactor https://runninginproduction.com/podcast/11-logflare-is-a-log-management-and-event-analytics-platform
* _CORS_: https://github.com/adamchainz/django-cors-headers
* _debug_ https://django-debug-toolbar.readthedocs.io/en/latest/installation.html
* _Docker_: https://testdriven.io/blog/dockerizing-django-with-postgres-gunicorn-and-nginx/ https://www.untangled.dev/2020/06/06/docker-django-local-dev https://testdriven.io/courses/tdd-django https://learndjango.com/tutorials/django-docker-and-postgresql-tutorial
* _email_: https://learndjango.com/tutorials/django-email-contact-form
* _favicon_: https://learndjango.com/tutorials/django-favicon-tutorial
* _internals_: https://djangodeconstructed.com/ how do class names (`PasswordChangeView`) resolve to import names (`from django.contrib.auth.views import password_change`)?
* _logging_: https://mattsegal.dev/django-gunicorn-nginx-logging.html https://djangodeconstructed.com/2018/12/18/django-and-python-logging-in-plain-english/ https://www.willmcgugan.com/blog/tech/post/richer-django-logging
* _maps_: https://www.paulox.net/2020/12/08/maps-with-django-part-1-geodjango-spatialite-and-leaflet/
* _Markdown_: https://learndjango.com/tutorials/django-markdown-tutorial
* _payments_: https://testdriven.io/blog/django-stripe-tutorial/ https://github.com/zinmyoswe/Django-Ecommerce https://github.com/dinoperovic/django-salesman
* _perf_: https://openfolder.sh/django-faster-speed-tutorial
* _rate limiting_: https://github.com/jsocol/django-ratelimit
* _search_: https://findwork.dev/blog/optimizing-postgres-full-text-search-django/ https://www.youtube.com/watch?v=is3R8d420D4 https://youtu.be/is3R8d420D4 https://jamesturk.net/posts/websearch-in-django-31 https://www.youtube.com/watch?v=kOKwEDHeBX4 https://github.com/ivelum/djangoql https://pganalyze.com/blog/full-text-search-django-postgres Haystack https://django-q.readthedocs.io/en/latest/examples.html https://github.com/etianen/django-watson https://www.paulox.net/2017/12/22/full-text-search-in-django-with-postgresql
* _secrets_: https://github.com/LeeHanYeong/django-secrets-manager
* _SEO_: https://github.com/kapt-labs/django-check-seo https://github.com/kapt-labs/django-check-seo https://learndjango.com/tutorials/django-sitemap-tutorial
* _sessions_: https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Sessions https://www.youtube.com/watch?v=SMRaHSZiwWE https://eli.thegreenplace.net/2011/06/24/how-django-sessions-work-introduction/
* _Swagger_: https://github.com/axnsan12/drf-yasg
* _taxes_: https://github.com/lowercase-app/django-taxtea
* _tracing_: https://github.com/dabapps/django-log-request-id
* _type checking_ https://sobolevn.me/2019/08/typechecking-django-and-drf

## templates

* https://girlthatlovestocode.com/django-template-tags
* charting https://www.youtube.com/watch?v=B4Vmm3yZPgc
* linting https://github.com/thibaudcolas/curlylint
* _DTL_: default template engine; stick with this over jinja2 https://blog.doismellburning.co.uk/django-an-unofficial-opinionated-faq/
* _syntax_: `{{ }}` insert from context `{% %}` block, inheritance 🙃 percentage signs have to be right against braces
* `context`: dict of template variable to Django obj https://docs.djangoproject.com/en/2.0/intro/tutorial03/#write-views-that-actually-do-something vs. DRF's notion of context, which is the way to get access to entire request (like URL) i.e. more info than the obj you're trying to serialize
* `user`: always in context [Osborn 1.10.68]
* `templates`: inside app (official tutorial, Osborn) inside project (Cookiecutter, Vincent https://wsvincent.com/django-about-page-three-ways/ https://wsvincent.com/django-tips-template-structure/)
* `static`: alongside `templates`; reference from html via `{% load staticfiles %}` and `<link rel="stylesheet" href="{% static 'styles.css' %}" />` [Osborn 1.4.15]
* can provide default values for templates [Osborn 1.5.21]
* `{% load staticfiles %}`: children can inherit for CSS, not for images [Osborn 1.5.22]
* can use Markdown for templates as well https://github.com/rgs258/django-markdown-view

* snippets
```python
# set project-wide templates dir https://learndjango.com/tutorials/template-structure
TEMPLATES = [{ 'DIRS': [os.path.join(BASE_DIR, 'templates')] }]

# render with context
return render(request, 'thing_detail.html', context={'thing':thing})
```

## testing

📜 https://docs.djangoproject.com/en/dev/topics/testing/
🔗 https://www.obeythetestinggoat.com/pages/book.html#toc
🔍 https://www.valentinog.com/blog/testing-django/

impl
```python
###
# GET
###
from django.test import TestCase
class HealthcheckTest(TestCase):
    def test_healthcheck(self):
        res = self.client.get('/healthcheck/')
        self.assertEqual(res.status_code, 200)

###
# POST
###
from rest_framework.test import APIClient  # only worked w/ DRF client and setting fmt as json
res = self.client.post("/api/", data, format="json")
```

misc
* _client_: acts as dummy browser https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Testing#content DRF https://www.django-rest-framework.org/api-guide/testing/#apiclient vanilla https://docs.djangoproject.com/en/3.1/topics/testing/tools/#the-test-client
* _request factory_: add stuff onto req (middleware, user) vs. mimicking browser like client https://docs.djangoproject.com/en/stable/topics/testing/advanced/#the-request-factory
* `TestCase`: creates tmp db for each transaction using same dbms from `setting.py/databases/default` https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Testing#what_does_django_provide_for_testing
* `SimpleTestCase`: for when you don't need db e.g. templates https://learndjango.com/tutorials/django-testing-tutorial inherits from unittest's `unittest.TestCase` https://docs.djangoproject.com/en/2.0/topics/testing/tools/#simpletestcase
* `tearDown()`: TestCase does teardown itself so this isn't typically used https://developer.mozilla.org/en-US/docs/Learn/Server-side/Django/Testing#content
* internals https://adamj.eu/tech/2020/09/05/what-happens-when-you-run-manage.py-test
* DRF: https://www.youtube.com/playlist?list=PLP1DxoSC17LZTTzgfq0Dimkm6eWJQC9ki
* testing admin https://til.simonwillison.net/django/testing-django-admin-with-pytest

execution
* everything prepended w/ `test_` is run
* coverage integration https://docs.djangoproject.com/en/3.1/topics/testing/advanced/#integration-with-coverage-py https://adamj.eu/tech/2019/04/30/getting-a-django-application-to-100-percent-coverage/
```sh
# https://stackoverflow.com/a/18834222
python3 manage.py test app  # app
python3 manage.py test app.tests.mod  # module
python3 manage.py test app.tests.mod.cls  # class
python3 manage.py test app.tests.tests.mod.cls:my_method  # method
```
