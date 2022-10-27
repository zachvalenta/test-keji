# TODO

## 参考

📜 https://docs.python.org/3
⛩ `python -m this`
🔍 semantics https://www.fluentpython.com/lingo/ 📙 Ramalho
🗣 https://chat.stackoverflow.com/rooms/6/python
📚
* Beazley cookbook
* Ramalho fluent https://github.com/fluentpython/example-code-2e
* Van Rossum tutorial

## current

## queue

* prefix operator @ https://treyhunner.com/2018/10/asterisks-in-python-what-they-are-and-how-to-use-them/#Asterisks_in_list_literals https://www.youtube.com/watch?v=R8-oAqCgHag https://bas.codes/posts/python-asterisks
* rf packaging
* rf objects https://www.youtube.com/c/mCodingWithJamesMurphy
* version mgmt
* profiling

## done

* _22_: iteration internals (iterators, generators)
* _21_: rf pdb, doctest basics
* _20_: not much
* _19_: executables, imports, obj assignment, pipx and Poetry, first pass (lambdas, tuple unpacking, iteration, dataclasses, shallow vs. copy, closure, decorator)
* _18_: Hitchhiker's Guide, first pass (imports, unit testing)
* _17_: PSF install, PS beginner course

# CLASSES

🗄 `language.md` object-oriented
📚
* Beazley ch. 7
* Van Rossum ch. 9 https://docs.python.org/dev/tutorial/classes.html

basics
* object model: everything inherits from `object` as of Python 2.2 https://www.youtube.com/watch?v=vvuYPUbwAO0 2:30
* declaration https://www.youtube.com/watch?v=vvuYPUbwAO0
```python
class Foo(object):  # Python 2
class Bar:          # Python 3
```
* construction: `alice = Human("alice")`
* access obj attr w/ dot: `alice.name`

descriptors
> Descriptors provide the underlying magic for most of Python’s class features, including @classmethod, @staticmethod, @property, and even the __slots__ specification. By defining a descriptor, you can capture the core instance operations (get, set, delete) at a very low level and completely customize what they do. This gives you great power, and is one of the most important tools employed by the writers of advanced libraries and frameworks. 📙 Beazley 265
* impl https://docs.python.org/dev/reference/datamodel.html#implementing-descriptors
* https://realpython.com/python-descriptors/#why-use-python-descriptors
* http://nbviewer.jupyter.org/urls/gist.github.com/ChrisBeaumont/5758381/raw/descriptor_writeup.ipynb
* https://sadh.life/post/descriptors/
* even the pros don't knwo much about them https://nedbatchelder.com/blog/201306/explaining_descriptors.html
* class that defines `__get__`, `__set__`?
* `__get__` enables for true encapsulation vs. name mangling
* https://docs.python.org/3/howto/descriptor.html 
* https://stackoverflow.com/questions/22616559/use-cases-for-property-vs-descriptor-vs-getattribute
* https://nedbatchelder.com/blog/201306/explaining_descriptors.html
* _fully persistent data structure_: Git works like this, can branch, can time travel
* _partially persistent data structure_: same as fully persistent except can only modify the most recent copy

## dunder

📜 https://docs.python.org/dev/reference/datamodel.html#specialnames
📙
* Kettler magic https://rszalski.github.io/magicmethods/
* Ramalho ch. 1
* Van Rossum ch. 9

* _dunder_: methods called by the interpreter 📙 Ramalho [3]
* aka magic/special methods 📙 Ramalho [4]
> When an object is passed to the str built-in function, its __str__ method is called. When an object is passed to the len built-in function, its __len__ method is called. https://treyhunner.com/2018/06/how-to-make-an-iterator-in-python/

---

* aka magic methods, name mangling, special methods 📙 Ramalho 3
> why isn't "magic method" or "dunder" in the docs? 📙 Kettler https://docs.python.org/dev/reference/datamodel.html#specialnames https://github.com/python/cpython/blob/main/Doc/reference/datamodel.rst
* _operator overloading_: 
* truer definition of "magic" would language features that user-defined classes cannot used e.g. read-only attr in pre-ES5 JavaScript 📙 Ramalho 16
* used in Django queryset https://books.agiliq.com/projects/Journeyman-Python/en/latest/magic-methods.html

uses
* lifecycle https://eli.thegreenplace.net/2012/04/16/python-object-creation-sequence
```python
class Foo:
    def __init__(self):
        print("init")  # https://realpython.com/python-multiple-constructors/ https://realpython.com/python-class-constructor/
    def __call__(self):
        print("call")

foo = Foo()  # INIT
foo()        # CALL
```
```python
class UrOpener(object):
  # new = precedes init https://betterprogramming.pub/5-pairs-of-magic-methods-in-python-you-should-know-f98f0e5356d6
  pass
  # init = called on obj initialization
  def __init__(self, filename):
    self.file = open(filename)
  # enter = called when enter context (i.e. `with` block starts)
  def __enter__(self):
    return self.file  
  # exit = called when exit context (i.e. `with` block ends)
  # idk what extra 3 args do
  def __exit__(self, a,b,c):
    self.file.close()

with open ('sample-file.txt') as file:
  contents = file.read()
  print(contents)

with UrOpener('sample-file.txt') as file:
  contents = file.read()
  print(contents)
```

## inheritance

hierarchy https://blog.ionelmc.ro/2015/02/09/understanding-python-metaclasses/
* _metaclass_: parent of classes
* used in Django https://news.ycombinator.com/item?id=22346964
* _class_: instance of metaclass
* _instance_: instance of class
```python
class Meta(type):
    pass
class Cls(metaclass=Meta):
    pass
type(Cls)  # <class '__main__.Meta'>
```

---

mixins
* _mixin_: multiple inheritance of abstract class https://stackoverflow.com/a/15605119
* _interface_: https://docs.python.org/3/faq/design.html#how-do-you-specify-and-enforce-an-interface-spec-in-python https://realpython.com/python-interface/ https://glyph.twistedmatrix.com/2021/03/interfaces-and-protocols.html
* _sink_: https://www.ianlewis.org/en/mixins-and-python https://stackoverflow.com/a/52469499/6813490 https://www.residentmar.io/2019/07/07/python-mixins.html https://stackoverflow.com/questions/533631/what-is-a-mixin-and-why-are-they-useful mixins tutorial https://easyaspython.com/mixins-for-fun-and-profit-cb9962760556 https://stackoverflow.com/a/547714/6813490

* _sink_: https://www.youtube.com/watch?v=YXiaWtc0cgE https://realpython.com/inheritance-composition-python/ https://realpython.com/oop-in-python-vs-java/
* _inner class_: encapsulate something only relevant to enclosing class, stem proliferation of small modules https://stackoverflow.com/questions/719705/what-is-the-purpose-of-pythons-inner-classes
* _overloading_: have to implement yourself https://news.ycombinator.com/item?id=22340720

* super: call method from parent
```python
class Mammal():
    def __init__(self, name):
        print('{} is a warm-blooded animal'.format(name))
#############################3
class Dog(Mammal):
    def __init__(self):
        super().__init__('a dog')
```

```python
class Alice():
    def crawl(self):
        print('crawling')

class Bob():
    def walk(self):
        print('walking')

class Candace(Alice, Bob):
    def run(self):
        print('running')

c = Candace()
c.run()
c.walk()
c.crawl()
```

## methods

instance, class, static
```python
class Human:
    planet = "earth"

    def __init__(self, name):
        self.name = name
    
    def im(self):
        """
        * requires instance to call https://softwareengineering.stackexchange.com/a/306095
        * can access class and instance variables
        * take instance obj as arg
        """
        print(f"hi I'm {self.name} and I'm from {self.planet} and my obj is {self}")

    @classmethod
    def cm(cls):
        """
        * doesn't require instance to call
        * can access class variables
        * take class obj as arg
        """
        print(f"hey I'm from {cls.planet} and my obj is {cls}")

    @staticmethod
    def sm():
        """
        * doesn't require instance to call
        * no access to instance/class variables
        """
        return "hi, sm"
```

self/cls 
* impl via descriptor https://www.youtube.com/watch?v=ANLjBsWHshc
* just naming convention https://stackoverflow.com/a/475919
* debate http://neopythonic.blogspot.com/2008/10/why-explicit-self-has-to-stay.html https://stackoverflow.com/q/2709821

@property
* call method same way you used access property/attr i.e. dot notation
* way to refactor field into method https://www.machinelearningplus.com/python/python-property/ https://stackoverflow.com/q/6618002/6813490
```python
# phase 1 - .fullname becomes inconsistent if other attr updated bc only set on init
class Person():
    def __init__(self, firstname, lastname):
        self.first = firstname
        self.last = lastname
        self.fullname = self.first + ' '+ self.last

# phase 2 - works but a breaking change bc .fullname is now .fullname()
class Person():
    def __init__(self, firstname, lastname):
        self.first = firstname
        self.last = lastname

    def fullname(self)
        return self.first + ' ' + self.last

# phase 3 - invoke method with same syntax as accessing property
class Person():

    def __init__(self, firstname, lastname):
        self.first = firstname
        self.last = lastname

    @property
    def fullname(self)
        return self.first + ' ' + self.last
```

# CQ

🗄 REPL

* matchers: https://github.com/hamcrest/PyHamcrest https://github.com/mwilliamson/python-precisely https://changelog.com/gotime/159 https://github.com/corbym/gocrest
* _non-fatal assertions_: continue execution if assertion fails https://github.com/okken/pytest-check unittest https://stackoverflow.com/a/5028110 pytest parameters https://stackoverflow.com/a/36760045

things to check
* autoformat: Black, isort, blacker https://github.com/akaihola/darker black on documentation https://github.com/asottile/blacken-docs
* dead code: https://github.com/jendrikseipp/vulture https://github.com/joshuaclayton/unused https://github.com/sobolevn/flake8-eradicate 
* security: bandit, https://pyup.io/ (uses same vulnerability db as pipenv) pysa https://news.ycombinator.com/item?id=24083432
* src: inspect + ast https://hakibenita.com/automating-the-boring-stuff-in-django-using-the-check-framework

Tox
* test against multiple Python versions
* https://realpython.com/python-testing/#testing-in-multiple-environments https://www.andreagrandi.it/2019/02/21/skipping-tests-depending-python-version/ https://www.b-list.org/weblog/2020/feb/03/how-im-testing-2020/
```sh
# run for n dirs
tox -e py27 -- path/here/ path/there

# run for module
tox -e py27 -- path/here/foo.py

# run for class
tox -- path/to/foo.py::FooClass

# run for func
tox -- path/to/foo.py::FooClass::test_foo

# run test for all versions
tox -- tests/util/dicts_test.py
```

## coverage

📜 https://coverage.readthedocs.io/

* `.coverage`: result files; read by `coverage report` and `coverage html`
* pytest-cov` also has `--cov-fail-under=MIN` arg you could pass as a normal pipeline step https://github.com/pytest-dev/pytest-cov
* pretty slow https://www.drmaciver.com/2017/09/python-coverage-could-be-fast/
* impl https://talkpython.fm/episodes/transcript/178/coverage.py @ 42:00 https://www.pythoninsight.com/2018/03/how-does-coverage-measurement-work-in-python/
```sh
# syntax: `coverage run` replaces whatever was executing tests (`python`, `python manage.py`)
coverage run -m unittest discover -v
# what files to cover is combination of source/include/omit https://stackoverflow.com/q/1628996
poetry run coverage run --source='api' --omit='*/migrations/*.py' manage.py test api
poetry run coverage run --source='api' --omit='*/migrations*'  # all from dir
poetry run coverage run --source='api' --omit='*/migrations*,api/apps.py'  # omit n
# use .coverage for terminal summary
coverage report
# create htmlcov from .coveragerc and open report
coverage html && coverage htmlcov/index.html
```

## documentation

docstring
* _doctring_: triple quote as first line of class/function https://github.com/econchick/interrogate
* use triple quote in lieu of multi-line comment https://stackoverflow.com/a/7696966
* `pydoc`: parse/fmt doctring to create documentation
* how to read: module (`help("doctest")`) function (`help(my_func)` or `my_func.__doc__`)
```python
def foo(my_arg):
    # basic
    """
    basic docstring
    """

    # PyCharm convention https://stackoverflow.com/a/40596167
    """
    This line is for an overview.

    :param req: request from web framework
    :return: what this function is returning
    """
```

doctest
* _doctest_: docstring + test
> [key feature] they look like transcripts of interactive Python console sessions, so you can easily try out the demonstrations yourself 📙 Ramalho xviii
* as TDD-as-design tool bc favors small functions that require minimal setup
* keep docstring aligned to src
* run: `python -m doctest -v my_mod.py`
```python
def foo(a, b):
    """
    >>> foo(2, 3)
    5
    """
    return a + b
```

---

https://talkpython.fm/episodes/show/354/sphinx-myst-and-python-docs-in-2022
❓ where are help files stored for Cpython? 3rd-party pkg are stored around `/Library/Frameworks/Python.framework/Versions/3.6/lib/python3.6/site-packages/<pkg>/__init__.py` asking bc seems like `l.insert()` doesn't have type annotation for return value in help docs (whereas other string methods do)

__tooling__

* _pdoc_: thing that pdoc3 forked from https://github.com/mitmproxy/pdoc
* _pdoc3_: https://pdoc3.github.io/pdoc/ some controversy https://github.com/pdoc3/pdoc/issues/64 https://github.com/pdoc3/pdoc/issues/87 even worse than first blush, apparently he is a fascist https://news.ycombinator.com/item?id=20800157
* _pdocs_: https://github.com/timothycrosley/pdocs/issues/3
* _portray_: built on pdoc3 https://github.com/timothycrosley/portray/
* _pydoc_: https://docs.python.org/3/library/pydoc.html https://stackoverflow.com/a/13043765/6813490 
* _pycco_: pretty but don't see use case https://pycco-docs.github.io/pycco/ https://realpython.com/generating-code-documentation-with-pycco/
* _Sphinx_: `sphinx-apidoc` 缺点 RST, not geared towards APIs https://realpython.com/courses/documenting-python-projects-sphinx-read-the-docs/ can now use Markdown https://www.youtube.com/watch?v=YclYtM56qjo&list=PL2Uw4_HvXqvYk1Y5P8kryoyd83L_0Uk5K&index=38

## exceptions

📚
* Beazley ch. 14
* Van Rossum ch. 8 https://docs.python.org/3/tutorial/errors.html

semantics
* _handler_: `try` block
* _unhandled_: no handler found

common errors
* `Attribute`: attr doesn't exist or cannot be set
* `Index`: trying to access non-existent index; slices handle these in a weak way (i.e. type conversion)
* `Key`: dict doesn't have key you asked for
* `Name`: identifier not defined
* `Syntax`: kw misspelled, bad indentation, missing closing syntax
* `Type`: give wrong type to function, try to do something you can't (mutate string)
* `Value`: func given correct type but still err ex. `int('5')` can convert string to int but not for all strings e.g. `int('five')`

user-defined 
* way to dedupe logging
* boring impl
```python
class EarthquakError(Exception): 
    pass

if not stable_plate:
    raise EarthquakError("earthquake!")
```
* fancier impl
```python
class EarthquakError(Exception): 
    def __init__(self, place):
        self.place = place
    def __str__(self):
        return f"uh oh {self.place} has earthquakes"

def move_to(place):
    raise EarthquakError(place)

def get_better_life():
    try:
        move_to(place="california")
    except EarthquakError as e:
        print(e)
```

---

* control flow: don't go nuts with it https://blog.cerebralab.com/Exceptions_as_control_flow
```python
# CONTROL FLOW
try:
    pass
except SpecificException as e:
    logger.exception(e)
    raise
else: 
    # only for the happy path
finally:
    # no matter what happens

# PASS TO CALLER https://stackoverflow.com/a/34622772
def raiser():
    try:
        do_something()
    except ValueError as err:
        logger.exception(err)
        raise  # https://stackoverflow.com/a/24065533

for el in li:
    raiser()
except Exception as err:
    logger.exception(err)
```

---

* _approach_: EAFP (forgivness > perm i.e. try-catch) better than LBYL (C-style if-else) https://docs.python.org/3/glossary.html#term-eafp
* _sink_: 📙 tutorial ch 8 stdlib ch 5 https://realpython.com/courses/python-exceptions-101/ https://sobolevn.me/2019/02/python-exceptions-considered-an-antipattern https://news.ycombinator.com/item?id=19133948

* _swallow msg_: https://stackoverflow.com/a/52625133/6813490
* _warnings_: https://www.reddit.com/r/learnpython/comments/a14ow5/psa_when_developing_set_pythonwarnings/ https://lerner.co.il/2020/04/27/working-with-warnings-in-python/

## linting

https://flake8.pycqa.org/ https://flake8.pycqa.org/en/latest/user/configuration.html

* lint exceptions https://github.com/guilatrova/tryceratops
* only run on everything outside of repository https://github.com/akaihola/darker
* ignore line: `# NOQA` https://flake8.pycqa.org/en/2.6.0/config.html#per-code-line 
```conf
# multiple
flake8 dir1 dir2
# all __init__
exclude = */__init__.py

# can use from shell, but it might be picking up config file somewhere, so this worked to get back to defaults
flake8 --isolated

# .flake8 (don't use tox.ini) 
# example conf https://ljvmiranda921.github.io/notebook/2018/06/21/precommits-using-black-and-flake8/
[flake8]
max-complexity = 10
max-line-length = 88
ignore =  # http://flake8.pycqa.org/en/latest/user/configuration.html
    # play nice w/ Black https://github.com/psf/black/issues/1029
    E203,  
    # workaround for flattened Flask project structure
    E402
    # flake8 seems dated on line break https://www.flake8rules.com/rules/W503.html https://dev.to/m1yag1/how-to-setup-your-project-with-pre-commit-black-and-flake8-183k
    W503
per-file-ignores =  # https://stackoverflow.com/a/54454433/6813490
    # give user access to all models from REPL
    db_shell.py:F401
```

## perf

* pyperf, timeit https://medium.com/@martin.heinz/python-cli-tricks-that-dont-require-any-code-whatsoever-e7bdb9409aeb
* benchmark: https://github.com/sharkdp/hyperfine https://github.com/egoist/dum
* can use hyperfine under the hood https://github.com/dandavison/magit-delta https://github.com/sharkdp/hyperfine
* https://blog.usejournal.com/how-to-create-your-own-timing-context-manager-in-python-a0e944b48cf8 https://martinheinz.dev/blog/13 https://realpython.com/python-timer/
```python
# The "timeit" module lets you measure the execution
# time of small bits of Python code

# https://www.youtube.com/watch?v=EcGWDNlGTNg

>>> import timeit
>>> timeit.timeit('"-".join(str(n) for n in range(100))',
                  number=10000)

# 0.3412662749997253

>>> timeit.timeit('"-".join([str(n) for n in range(100)])',
                  number=10000)

# 0.2996307989997149

>>> timeit.timeit('"-".join(map(str, range(100)))',
                  number=10000)

# 0.24581470699922647
```

```python
# https://stackoverflow.com/a/7523810/6813490

from timeit import Timer

# doesn't manifest savings in small collections
names_list = ['alice', 'bob', 'candace']
names_set = set(['alice', 'bob', 'candace'])

# setup large collection of numbers and see what happens then

def lookup_list(l):
    return 'alice' in l


def lookup_set(s):
    return 'alice' in s


def cast_to_timer(func, args):
	return Timer(lambda: func(args))


def timeit_ms(func):
	return print(func.timeit(number=1000))


if __name__=='__main__':
    timeit_ms(cast_to_timer(lookup_list, names_list))
    timeit_ms(cast_to_timer(lookup_set, names_set))
```

## profiling

📙 Beazley ch. 14
🗄 `linux.md` tracing
📜 https://docs.python.org/3/library/debug.html
https://github.com/bloomberg/memray https://realpython.com/podcasts/rpp/128/

> It might be a good idea to have an active profiler - to push performance data to the programmer instead of waiting for him to come asking for it. http://paulgraham.com/popular.html

https://pythonspeed.com/articles/measuring-python-performance/

* _profiler_: measure performance i.e. see which lines are executing and how long they take
* `trace`
```python
# src
if True:
    print("hi")
else:
    print("nope")
```
```sh
# trace
py3 -m trace --trace example.py
--- modulename: tracer, funcname: <module>
tracer.py(2):     print("hi")
hi
 --- modulename: trace, funcname: _unsettrace
trace.py(77):         sys.settrace(None)
```

---

* https://codesolid.com/how-do-i-profile-python-code/
* https://tinkering.xyz/fmo-optimization-story/
* https://tech.marksblogg.com/faster-python.html https://www.peterbaumgartner.com/blog/intro-to-just-enough-cython-to-be-useful/ https://github.com/tonybaloney/perflint https://rednafi.github.io/reflections/pre-allocated-lists-in-python.html
* https://github.com/pyroscope-io/pyroscope
* https://flamegraph.com/
* profiling CLI, `time` https://news.ycombinator.com/item?id=30224063
* profiling async https://github.com/aviramha/capara
* https://pythonspeed.com/memory/
* https://github.com/pythonprofilers/memory_profiler https://news.ycombinator.com/item?id=27025829
* https://github.com/csurfer/pyheat
* https://github.com/joerick/pyinstrument
* https://www.youtube.com/watch?v=1EZ8oqjLun0
* https://medium.com/statch/speeding-up-python-code-with-nim-ec205a8a5d9c
* https://github.com/joerick/pyinstrument
* https://hakibenita.com/django-rest-framework-slow
* https://github.com/robusta-dev/WhyProfiler
* `time` https://hacker-tools.github.io/program-introspection/
* https://github.com/joerick/pyinstrument
* https://github.com/P403n1x87/austin https://talkpython.fm/episodes/show/265/why-is-python-slow 54:00
* _flamegraph_: visualization for CPU usage https://heap.io/blog/engineering/basic-performance-analysis-saved-us-millions
* _tools_: PyFlame https://medium.com/zendesk-engineering/hunting-for-memory-leaks-in-python-applications-6824d0518774 PySpy https://github.com/benfred/py-spy/ profile CPython https://instagram-engineering.com/profiling-cpython-at-instagram-89d4cbeeb898 https://pythonspeed.com/articles/memory-profiler-data-scientists/ Fil https://pythonspeed.com/products/filmemoryprofiler/
* sink: https://www.blog.pythonlibrary.org/2020/04/14/an-overview-of-profiling-tools-for-python/ https://www.roguelynn.com/words/tracing-fast-and-slow/ https://pythonspeed.com/articles/blocking-cpu-or-io/ https://pythonspeed.com/articles/custom-python-profiler/ https://pythonspeed.com/articles/live-debugging-python/ https://www.markkeller.dev/2018-07-14-optimize_python/ https://jvns.ca/blog/2017/12/02/taking-a-sabbatical-to-work-on-ruby-profiling-tools/ pyspy https://jvns.ca/blog/2018/12/23/2018--year-in-review/ https://www.youtube.com/watch?v=d5SGUscT2GA https://jvns.ca/blog/2017/12/17/how-do-ruby---python-profilers-work-/ https://github.com/ionelmc/python-hunter https://wsvincent.com/algorithms-binary-search/ https://wsvincent.com/python-optimizations-with-guido/ https://realpython.com/python-f-strings/ https://github.com/airspeed-velocity/asv

## pytest

📜 https://docs.pytest.org/en/latest/contents.html#toc

misc
* does pytest/unittest use `trace` module?
* better than unittest bc easier assertions, parameterization, function-based https://github.com/renzon/pytest-vs-unittest https://www.b-list.org/weblog/2020/feb/03/how-im-testing-2020/
* will pick up modules prepended w/ `test_` otherwise on you to specify
* run in parallel https://github.com/pytest-dev/pytest-xdist https://tech.marksblogg.com/faster-django-testing.html
* xfail https://blog.ganssle.io/articles/2021/11/pytest-xfail.html

cli
* freezes terminal if encounters breakpoint, workaround w/ `pytest -s --pdb`
* `pytest.set_trace()` is deprecated and doesn't work w/ pdbpp https://github.com/pdbpp/pdbpp/issues/392 https://docs.pytest.org/en/latest/historical-notes.html#pytest-set-trace 
```sh
###
# BIN vs. MOD
###
pytest             # bin
python3 -m pytest  # module

###
# SCOPE https://stackoverflow.com/a/54493489
###
test_mod.py             # module
test_mod.py::test_func  # func
-m slow                 # marker
-k <expression>         # regex

###
# ARGS
###
--lf           # only runs tests that failed on last attempt
--testmon      # only runs tests affect by recent code change https://github.com/anapaulagomes/pytest-picked https://github.com/tarpas/pytest-testmon
--durations=n  # show n slowest setups/tests
--setup-show   # show setup of fixtures while executing tests.

###
# DEBUG
###
--pdb    # use w/ pdb.set_trace() https://docs.pytest.org/en/latest/how-to/failures.html#dropping-to-pdb-python-debugger-on-failures 🗄 `sw/algos/algos`
--trace  # use w/ individual func when pdb not working (this happened at work once, idky)
-s       # necessary for pdbpp to work https://stackoverflow.com/a/3418597
-l       # locals https://hackebrot.github.io/pytest-tricks/debug_test_failures/
```

marks
* _mark_: decorator to add metadata
* skip test `pytest.skip('WIP')` https://github.com/box/flaky https://danluu.com/wat/
* params https://docs.pytest.org/en/6.2.x/parametrize.html
> these less readable to me

stdout
* summary reports https://docs.pytest.org/en/latest/usage.html#detailed-summary-report
* info in tracebacks https://docs.pytest.org/en/latest/usage.html#modifying-python-traceback-printing
* `-s` see print statements https://stackoverflow.com/a/55950781/6813490
* `-v` see each test that executed https://github.com/darrenburns/pytest-clarity https://github.com/Teemu/pytest-sugar https://github.com/numirias/pytest-json-report
* group related tests https://pypi.org/project/pytest-testdox/
```python
@pytest.mark.describe("doing stuff")  # can also use mark.it()
def test_doing_this():
    pass
def test_doing_that():
    pass
```
```sh
doing stuff
 [x] doing this
 [x] doing that
```

config
```python
class Test():
    __test__ = False  # tells pytest to not collect this class https://stackoverflow.com/a/42534950/6813490
    foo = 'foo'
```
```conf
# suppress all
pytest --disable-pytest-warnings

# suppress warnings by type https://stackoverflow.com/a/53218641/6813490 https://github.com/zachvalenta/create-python-app/blob/master/pytest.ini
[pytest]
filterwarnings =
    ignore::DeprecationWarning
```

fixtures
* session https://nedbatchelder.com/text/test3/test3.html#39 
* parameterize: https://nedbatchelder.com/text/test3/test3.html#41 cannot use module scoped data https://github.com/pytest-dev/pytest/issues/349
* set module scope for data https://stackoverflow.com/a/47885205 https://docs.pytest.org/en/latest/how-to/fixtures.html#scope-sharing-fixtures-across-classes-modules-packages-or-session
```python
@pytest.fixture(scope="module")
def data():
    return { "my_data": 42 }

def test_use_data(data):
    assert return_it(arg=data["my_data"]) == 42
```
* xunit for fixture/factory https://docs.pytest.org/en/latest/how-to/xunit_setup.html
```python
def setup_module():
    print('before entire mod')

def teardown_module():
    print('after entire mod')

def setup_function():
    print('before each func')
    
def teardown_function():
    print('after each func')

def test_foo():
    pass
```

Django
* things we used at work: pytest-django, pytest-env, pytest-python
* specify settings https://pypi.org/project/pytest-env/
```ini
# pytest.ini
[pytest]
env =
  DJANGO_SETTINGS_MODULE=proj.settings
```

## typing

🗄 `language.md` typing

* _type annotation_: Python 3, PEP 484 https://blog.zulip.org/2016/10/13/static-types-in-python-oh-mypy/
```python
def greeting(name: str) -> str:
    return f"hello, {}"
```
* mypy can check both annotation and comments
* _type comments_: alternative to annotations for Python 2 https://realpython.com/lessons/type-comments/
```python
def my_func(arg):
    # type:(str) -> str
    return arg

my_variable = 42  # type: int

# not available in `__annotations__`
func.__annotations__
# {}
```

---

* https://realpython.com/python311-new-features/#improved-type-variables
* boxing https://www.moderndescartes.com/essays/data_oriented_python/ https://en.wikipedia.org/wiki/Object_type_(object-oriented_programming)#Boxing https://stackoverflow.com/questions/13055/what-is-boxing-and-unboxing-and-what-are-the-trade-offs
* _dummy version_: `isinstance`
* type hints introduced in PEP 484 https://www.python.org/dev/peps/pep-0484/
* _libs_: mpypy (PSF) PyRight (Microsoft) https://github.com/Microsoft/pyright pyre (Facebook) https://pyre-check.org/ pyannotate (Dropbox i.e. Python 2) https://github.com/dropbox/pyannotate MonkeyType (Instagram i.e. Python 3 https://github.com/Instagram/MonkeyType https://www.pythonpodcast.com/monkeytype-with-carl-meyer-and-matt-page-episode-146/
* _sink_: https://talkpython.fm/episodes/show/151/gradual-typing-of-production-applications https://www.youtube.com/watch?v=mh9jQSxzv0c https://inventwithpython.com/blog/2019/11/24/type-hints-for-busy-python-programmers/ https://veekaybee.github.io/2019/07/08/python-type-hints/ https://blog.petrzemek.net/2019/02/22/even-feature-that-you-do-not-use-can-bite-you/


mypy https://mypy.readthedocs.io/en/stable/getting_started.html#installing-mypy
* _impl_: looks at AST, doesn't run src
* changes versions too frequently https://news.ycombinator.com/item?id=26814919
* trade-offs: write a bit more code but read a lot less; more code but simpler (vs. Java tower of abstractions in type graph); prevents drift btw method sig and impl (esp. after refactor); seems easier/better to use at the start of a project (although, gradual typing given as a main use case; tbh, idk)
* debugging, best practices https://calpaterson.com/mypy-hints.html
* _Any_: mypy catch-all type for anything it can't do type inference on https://calpaterson.com/mypy-hints.html
* _Optional_: can return None (or another value)
* `typing.cast`: tell mypy that you know better than it does https://calpaterson.com/mypy-hints.html
```python
def get_config_value(key: str): Optional[str]:
    # Either return the config value, or None if it's not present
```
## unittest

📙 Beazley ch. 14
📜 stdlib chapter 26

* _advantages_: `unittest` assertions > Python OOB `assert` keyword bc useful logging https://stackoverflow.com/a/2958183/6813490
* _config_: tests prepended with `test_`; `discover` requires `__init__.py` in sub-directory https://stackoverflow.com/a/6672873/6813490
* _disadvantages_: seems to be fading in popularity, projects based on it are going away https://github.com/jarus/flask-testing too many assertions https://docs.python.org/3/library/unittest.html#classes-and-functions
* `error` vs. `failure`: exception vs. test case
* _fixtures_: `setUp` (run before each test case) `tearDown` (typically don't need to fuss with this)
* _history_: during Python 2.7 used to be called `unittest2` https://realpython.com/python-testing/
* _parameterize_: https://stackoverflow.com/a/34094/6813490
* run
```sh
py3 -m unittest discover -v  # all tests recursively
py3 -m unittest tests.test_sut  # all tests in module
py3 -m unittest tests.test_sut.TestSUT.test_sanity  # single test in module
```
* snippet
```python
# skip test
@unittest.skip("skip this test")

# class-based syntax
import unittest
class TestSUT(unittest.TestCase):
  def test_foo(self):
    self.assertEqual(True, True)

# test error thrown
def test_miss_entry_raises_KeyError(self):
  phonebook = Phonebook()
  with self.assertRaises(KeyError):
    phonebook.lookup('missing')

# test exit code https://stackoverflow.com/a/15672165
with self.assertRaises(SystemExit) as x:
  ur_method()
self.assertEqual(x.exception.code, 1)
```

# COLLECTIONS

📜 https://docs.python.org/3/library/stdtypes.html
📚
* Beazley ch. 1
* Van Rossum ch. 5

* _byte array_: used for HTTP response, passing files around

## taxonomy

| class   | type    | mutable | subscriptable |  notes              |
|---------|---------|---------|---------------|---------------------|
| list    | seq     | yes     | yes           | for iteration       |
| tuple   | seq     | no      | yes           | list + immutable    |
| string  | seq     | no      | yes           | tuple + for text    |
| dict    | mapping | yes     | yes           | place for ur stuff  |
| set     | set     | yes     | no            | for set operations  |

properties
* _subscriptable_: read by index or key
* aka indexing
* impl via `__getitem__` https://stackoverflow.com/a/216980
```python

```
* _mutable_: update by index or key
```python
# TypeError: 'tuple' object does not support item assignment
t = (42, 7, 13)
t[1] = "bob"
# TypeError: 'str' object does not support item assignment
b = "bob"
b[1] = "r"
```

## operations

utils
* lodash https://github.com/dgilland/pydash https://github.com/dgilland/fnc
* diff https://github.com/seperman/deepdiff

copy
* _idiom_: use factory function i.e. `list()` `dict()` instead of specific impl (`l[:]`, `l.copy()`) https://realpython.com/copying-python-objects/
* _shallow copy_: copied collection refers to obj from original i.e. cannot modify independently if obj are mutable [Smalleshire 1 6.5 @ 3:00]
```python
l = [42, 'abc', [1,2,3]]
n = list(l) 

n == l  # True bc holds same val
n is l  # False bc diff obj 

# shallow = mutable el will update for all collections that reference them
n[2][0] = 100
l  # [42, 'abc', [100, 2, 3]]
n  # [42, 'abc', [100, 2, 3]]

# immutable el are just replaced w/ new obj
n[0] = 0
l  # [42, 'abc', [100, 2, 3]]
n  # [0, 'abc', [100, 2, 3]]
```
* _deep copy_: copy actual values i.e. can modify independently
```python
from copy import deepcopy
l = [42, 'abc', [1,2,3]]
n = deepcopy(l) 
n[2][0] = 100
l  # [42, 'abc', [100, 2, 3]]
n  # [42, 'abc', [1, 2, 3]]
```

sort 📜 https://docs.python.org/3/howto/sorting.html https://realpython.com/python-sort
```python
# out-of-place
# works for any iterable https://realpython.com/python-sort/#sorting-numbers
sorted(tup)

# in-place
# method on lists
# uses Timsort sorts by first el e.g. `[(5, 1100), (6, 200)]`
qd.sort()
```

---

* `__lt__`: defines sort order for obj https://docs.python.org/3/howto/sorting.html#odd-and-ends
* `key`: func to apply to each el https://docs.python.org/3/howto/sorting.html#key-functions
```python
"""
basic
"""

sorted('This test string'.split(''))  # ['This', 'string', 'test']
sorted('This test string'.split(), key=str.lower)  # ['string', 'test', 'This'] -> ❓ unclear about syntax re: str.lower vs. str.lower() 

"""
1 attr
"""

from collections import namedtuple
Musician = namedtuple('Musician', 'name instrument genre')
mick = Musician(name='mick', instrument='vocals', genre='rock')
nas = Musician(name='nas', instrument='vocals', genre='rap')
stevie = Musician(name='stevie', instrument='piano', genre='r-n-b')
timbo = Musician(name='timbo', instrument='production', genre='rap')
musicians = [mick, nas, stevie, timbo]

sorted(musicians, key=lambda muz: muz.instrument)  # stevie and timbo to front

"""
n attr
"""

from operator import attrgetter
sorted(musicians, key=attrgetter('instrument', 'genre'))  # nas in front of mick
```

## list

```python
###
# READ
###

qd[0]  # read at index from start
qd[-2]  # read at index from end; n.b. not slice syntax
if qd:  # check if empty
qd.count(item)  # number of occurences

###
# UPDATE
###

qd.insert(ind, el)      # add at index
qd.extend(listToAdd)    # spread iterable
qd1 + qd2
qd2 = [42, *qd]
qd.insert(0, el)        # unshift
qd.append(el)           # push

del qd[2]  # rm at index
qd.remove('foo_el')  # rm by content
qd.pop(0)  # shift
qd.pop()  # pop

qd.reverse()  # in place
qd[index] = newItem  # overwrite at index
qd + qd  # concatenate

###
# INIT
###

l = [2]  # constructor - int, iterable as single el
list({1,2,3})  # constructor - spread over iterable
l = list ()  # empty (`list[]` is invalid)

###
# FMT
###

" ".join(str(x) for x in L)  # to string
print(*ur_list, sep="\n")  # https://stackoverflow.com/a/22695369
print(json.dumps(item, indent=4, sort_keys=True))  # https://stackoverflow.com/a/55179673/6813490
"""
{
    "first": 123,
    "second": 456,
    "third": {
        "1": 1,
        "2": 2
    }
}
"""

```

---

* 📍 https://docs.python.org/3/tutorial/stdlib2.html#tools-for-working-with-lists
* specialized array storage: array (typed) bytes (immutable, single byte i.e. 0-256) bytearray (byte but mutable) https://dbader.org/blog/python-arrays
* impl as dynamic array https://docs.python.org/3/faq/design.html#how-are-lists-implemented-in-cpython
* finding stuff
```python
# membership = "is it there?"
1 in [1, 2, 3]
'a' in 'abc'

# location = "where is it?"
qd.index(el)  # only returns first match
if my_str.find(query) >= 0:  # # https://docs.python.org/3/library/stdtypes.html#str.find
    return my_str.find(query)
else:
    return QueryNotFoundException()
```

## tuple

🔗 https://docs.python.org/3/tutorial/datastructures.html#tuples-and-sequences
🗄 'sorting'

```python
###
# INIT
###
tup = ()  # zero el
tup = ('a',)  # single el (sans trailing comma Python understands parens to be those of mathematical precedence control) https://docs.python.org/3/tutorial/datastructures.html#tuples-and-sequences
tup = 'a', 42, [1, 2, 3] # n el - parens recommended but not strictly necessary

###
# NAMED TUPLE
###
from collections import namedtuple
Musician = namedtuple('Musician', 'name instrument')  # first arg is type, second is attrs
stevie = Musician(name='stevie', instrument='piano')
stevie.instrument = "guitar"  # AttributeError

###
# SimpleNameSpace
# set attr on init, repr for free, comparison by attr instead of id() https://stackoverflow.com/a/37161391
# ❓ given that SimpleNameSpace is writable, why do docs recommend using named tuple instead? if you need a more complete container, why not tell people to use a class (like the comments on Stack Overflow)? https://docs.python.org/3/library/types.html?highlight=simplenamespace#types.SimpleNamespace
###
from types import SimpleNameSpace
stevie = SimpleNamespace(name="stevie", instrument="piano")
stevie.instrument  # 'piano'
stevie.instrument = "guitar"
stevie.instrument  # 'guitar'
```

## string

📙 Beazley ch. 1
🗄 `security.md` sanitization

* munge
```python
"NYC:London".split(":")         # into chunks; default delimiter is space
"NYC:London".partition(":")     # into halves; requires delimiter
list("this test string")        # split by char
"".join(l)                      # join by delimiter
"foo ".strip()                  # rm newline, trailing/leading whitespace
"1-2-3".replace("-", " ")       # swap
```

---

* contains `"hey" in "heya"`
formatting 📙 Van Rossum ch. 7
* _f-string_: only works on 3.6 and up https://old.reddit.com/r/learnpython/comments/hjegkc/why_do_people_use_format_method_when_f_string/ there's also Template strings, apparently safer that f-strings https://realpython.com/python-string-formatting/ convert to f-string https://github.com/ikamensh/flynt
```python

# HISTORY https://pyformat.info/
f"hey, {'zjv'.upper()}"  # newest
'{} {}'.format('one', 'two')  # newer
'%s %s' % ('one', 'two')  # old

###
# MULTILINE / CONCATENATION
###

# adjacent literals and f-strings concatenate automatically https://stackoverflow.com/a/54950733
me = 'z' 'j' 'v'

# combine w/ multiline (no commas else it's a tuple)
return (
    f"foo: {foo} bar: {bar}"
    f"baz: {baz} qux: {quz}"
)
my_var = (
    "long string oooooooooooooooooooooooone"
    "lone string twoooooooooooooooooooooooo"
)

# use join() bc other approaches create tmp obj (addition +, augmented assignment +=)
"".join(["alice", "and", "bob"])  # bobandalice
" ".join(["alice", "and", "bob"])  # bob and alice
```

misc
* parsing quotes https://pymotw.com/2/shlex/
* char values: `import string; string.string.ascii_letters` https://realpython.com/python-coding-interview-tips/#access-common-string-groups-with-string-constants
* _raw string_: treats backslash as literal, which is why they're seen in Django URLs, `re` https://docs.python.org/3/reference/lexical_analysis.html?highlight=string%20literal#string-and-bytes-literals
* _StringIO_: access string as if it were a file (for modules that are used to working with files) https://stackoverflow.com/a/7996541

encoding 🗄 `math.md` encoding
* _impl_: `PyBytesObject` (Python 3) `PyStringOjbect` (Python 2) https://www.laurentluce.com/posts/python-string-objects-implementation/ https://docs.python.org/3/whatsnew/2.6.html?highlight=pystringobject#pep-3112-byte-literals https://github.com/python/cpython/blob/45876a90e2663f12b90c2090ec3e48bd97841aae/Objects/bytesobject.c
* _unicode_: UTF8 seems like it was an unmitigated disaster https://news.ycombinator.com/item?id=21536468 https://pymongo.readthedocs.io/en/stable/tutorial.html file names stored as byte strings on OS, as Unicode in Python, PP 20:00 https://www.pythonpodcast.com/beets-with-adrian-sampson-episode-152/ @ 20:00 https://realpython.com/python-encodings-guide/ https://stackoverflow.com/a/2081655/6813490 https://www.b-list.org/weblog/2018/nov/26/case/ http://esr.ibiblio.org/?p=8161 http://python-notes.curiousefficiency.org/en/latest/python3/text_file_processing.html https://news.ycombinator.com/item?id=22931240 https://realpython.com/courses/python-unicode/

## dict

* map of immutable K to mutable V
* K can be int https://stackoverflow.com/questions/44814719/can-both-the-values-and-keys-of-a-dictionary-be-integers
* impl w/ hash table hash table https://akshayr.me/blog/articles/python-dictionaries https://www.pythoninsight.com/2018/08/python-basics-dict-lookup/ https://habr.com/en/post/458518/ https://docs.python.org/3/faq/design.html#how-are-dictionaries-implemented-in-cpython

OrderedDict
* ordered by insertion since 3.6 https://stackoverflow.com/a/39980744 https://just-taking-a-ride.com/inside_python_dict/chapter1.html
* doesn't work w/ keyword arguments https://stackoverflow.com/a/41866972
* need to add keys one at a time vs. constructor

```python
###
# INIT
###

literal = {'username': 'a-xia', 'followers': 987}
constructor = dict(username='a-xia', followers=987)

# can feed (unpack?) pairs into constructor
c = Counter(['alice', 'bob', 'candace', 'candace'])
c.most_common()  # [('candace', 2), ('alice', 1), ('bob', 1)]
dict(c.most_common())  # {'candace': 2, 'alice': 1, 'bob': 1}

###
# READ
###

# view obj  https://docs.python.org/3/library/stdtypes.html#dictionary-view-objects
.keys()   # K
.values() # V
.items()  # list of KV

```

---

recipes
* _check if empty_: cast to bool https://stackoverflow.com/a/54179636/6813490
* _check in key present_: `<key> in <dict>`
* _get all keys_: cast to list `list({'name': 'alice'})` https://docs.python.org/3/tutorial/datastructures.html#dictionaries
* _merge_: `{**dict1, **dict2}` https://realpython.com/iterate-through-dictionary-python/#using-the-dictionary-unpacking-operator https://treyhunner.com/2016/02/how-to-merge-dictionaries-in-python/
* _pretty print_: `print(json.dumps(item, indent=4, sort_keys=True))` only works when keys are primitives https://stackoverflow.com/a/47007417
* _sort_: `sorted(ur_dict.items(), key=lambda x: x[1])` (sorts by V) https://jeffknupp.com/blog/2018/12/13/how-to-do-just-about-anything-with-python-lists/

* read
```python
cidian['username']
cidian.get('username', 'could not find user name')  # fallback if attr not found
```

* default https://realpython.com/python-defaultdict/
* mutate
```python

# add key
my_dict['new_key'] = 'associated value'

# return existing key or set new (default)
my_dict = {'alice': 1234, 'bob': 5678}
my_dict.setdefault('alice', 'this val would be used if alice was not already a key')
my_dict  # {'alice': 1234, 'bob': 5678}
c = my_dict.setdefault('candace', 42)  # returns 42

# set default for all
my_dict = default_dict(list)
my_dict['alice'] = 1234
my_dict['bob'] = 5678
my_dict['candace']
# defaultdict(<class 'list'>, {'alice': 1234, 'bob': 5678, 'candace': []})

# overwrite key
user['name'] = 'alice'
user.update({'tweets': 42})

# rm key https://stackoverflow.com/a/11277439/6813490
del my_dict['key']  # KeyError if nonexistant
my_dict.pop('key')  # KeyError if nonexistant
k = my_dict.pop('key', None)  # no KeyError if nonexistant
k, v = cidian.popitem()  # pop off kv of last el
```

## set

* CRUD
```python
# create
ur_set = set()  # have to use parens for empty bc braces creates empty dictionary https://docs.python.org/3/tutorial/datastructures.html#sets
ur_set = {1, 1, 2, 3}  # literal
ur_set = set(['foo', 'foo', 'baz', 'foo'])  # constructor

# reads - no way to do non-mutatively bc sets are 1) unordered 2) don't support indexing https://stackoverflow.com/q/59825
# update 
my_set.add(el)  # push - single
my_set.pop()  # shift
my_set.update(iterable)  # push - n

# delete
ur_set.remove('foo_el')
```

* set operations 📍 pick SSoT between here and `math.md`
```python
fruit =  {"avocado", "banana", "tomato"}
veg = {"beet", "carrot", "tomato"}

# DIFFERENCE: el unique to first set 📙 Bhargava [150]
fruit - veg  # avocado, banana

# INTERSECTION: el shared 📙 Beaulieu [1000]
fruit & veg  # tomato

# SYMMETRIC DIFFERENCE: el not shared https://www.idiotinside.com/2017/08/19/set-theory-and-python-tips-tricks/
fruit ^ veg  # avocado, banana, beet, carrot

# UNION: el across sets sans dupes 📙 Beaulieu [99]
fruit | veg   # avocado, banana, tomato, beet, carrot
```

# FUNCTIONS

📙 Beazley ch. 7
🗄 obj/assignment

* _pass_: implicit return of `None`
* _return_: implicit return of `None` if no other return defined
> A Python function will always have a return value. There is no notion of procedure or routine in Python. https://realpython.com/python-return-statement/#implicit-return-statements

## args

* functions maintain order of args passed sinced Python 3.6 https://treyhunner.com/2018/04/keyword-arguments-in-python/#Order_matters

fixed
* _positional_: arg matched to param by sequence
* positinal-only `def bar(/, x)` https://www.youtube.com/watch?v=R8-oAqCgHag
* _keyword_: arg matched to param by name
* must follow positional
```python
foo("hey", "there")      # positional
foo(y="there", x="hey")  # keyword
```

variadic
* _*args_: variable number of positional args
* kw-only after
```python
def foo(*args, kw):
def bar(x, *, kw):  # alternate syntax https://www.youtube.com/watch?v=R8-oAqCgHag https://treyhunner.com/2018/10/asterisks-in-python-what-they-are-and-how-to-use-them/#Keyword-only_arguments_without_positional_arguments
```
* _**kwargs_: variable number of keyword args
* used in: OO https://stackoverflow.com/a/1415882 stdlib https://treyhunner.com/2018/04/keyword-arguments-in-python/#Where_you_see_keyword_arguments

prefix operator
* _prefix operator_: used for packing/unpacking https://treyhunner.com/2018/10/asterisks-in-python-what-they-are-and-how-to-use-them/
* _packing_: caputure all positional/keyword args and put into list/dict
* _unpacking_: iterate over list/dict
```python
# packing on function declaration
def bar(**kwargs):
# unpacking on function invocation
myd = dict(magic=32, larry=33)
"{magic} {larry}".format(**myd)
```

default
* must follow positional/keyword
* _early-bound_: evaluated at function definition https://rednafi.github.io/reflections/gotchas-of-early-bound-function-argument-defaults-in-python.html
* evaluated only once so use `None` over empty list https://news.ycombinator.com/item?id=29682785

## functools

* _partial_: create callable by wrapping another callable w/ default args http://pymotw.com/2/functools/
* closure for a function vs. just a value
> we created a new callable that will always pass the `file=sys.stderr` keyword argument to print, allowing us to simplify our code by not having to specify the keyword argument every time. https://towardsdatascience.com/functools-the-power-of-higher-order-functions-in-python-8e6e61c6e4e4 
```python
from functools import partial
import sys
print_stderr = partial(print, file=sys.stderr)
print_stderr("This goes to standard error output")
```

* _reduce_: sum over list comprehension https://stackoverflow.com/a/16632125
```python
from functools import reduce
from operator import mul
nums = [1, 2, 3]
reduce(mul, nums)  # 6
```

## inner / closures

🗄
* `language.md` functional
* functools/partial

* _closure_: closes around value on stack to preserve in mem after stack finishes 
```python
def generate_power(number):
    def nth_power(power):
        return number ** power
    return nth_power

# use this example
# https://stackoverflow.com/a/141426/6813490
def counter():
    count = 0
    def count()
```

* _inner_: sans closure doesn't seem particularly useful re: encapsulation https://stackoverflow.com/a/4020443/6813490 https://realpython.com/inner-functions-what-are-they-good-for/#encapsulation
```python
def outer(num):
    def inner_increment(num):
        return num + 1
    return inner_increment(num)
```

## lambdas

* _anonymous_: don't assign a name https://treyhunner.com/2018/09/stop-writing-lambda-expressions/
* _constraints_: only for expression i.e. no iteration, conditions https://wsvincent.com/python-lambda-expressions/
* _sink_: https://zenhack.net/2016/12/25/why-python-is-not-my-favorite-language.html https://realpython.com/python-lambda/ https://philip-trauner.me/blog/post/python-quirks-lambdas

__use cases__

* avoid a throwaway function definition

```python
colors = ["Goldenrod", "Purple", "Salmon", "Turquoise", "Cyan"]

# bad
def normalize_case(string):
    return string.lower()

normalized_colors = map(normalize_case, colors)

# better --> keep in mind, use list comprehensions instead of either map or filter
list(map(lambda x:x.upper(), colors))
```

* `key` function

```python
"""
MAX
-> https://www.youtube.com/watch?v=EnSu9hHGq5o&__s=kznp9q3qiibqzd9qjf12 @ 12:15
"""
tall_buildings = {'Empire State': 381, 'Sears Towers': 442, 'Burj Khalifa': 828}
max(tall_buildings.keys())  # 'Sears Towers'
max(tall_buildings.values())  # 828
max(tall_buildings.items(), key=lambda b: b[1])  # ('Burj Khalifa', 828)

"""
SORTED
-> https://treyhunner.com/2018/09/stop-writing-lambda-expressions/
"""

colors = ["Goldenrod", "Salmon", "purple", "turquoise", "cyan"]
sorted(colors, key=lambda s: s.lower())  # ['cyan', 'Goldenrod', 'purple', 'Salmon', 'turquoise']
sorted(colors, key=lambda c: (len(c), c.lower()))  # can also use tuple for combinatorial i.e. sort by length and then, if tie in length, use lexicographical (lowercased)
```

## scope

🔗 https://blog.araj.me/til-nonlocal-statement-in-python/ https://realpython.com/python-namespaces-scope/

* _scope_: namespace; doesn't correspond to code blocks e.g. `if` doesn't introduce nested scope
* _local_: current function https://realpython.com/python-pass-by-reference/#passing-arguments-in-python
```python
def loc():
    foo = 'foo val'
    print(locals())  # {'foo': 'foo val'}
```
* _global_: module (func/class, imports, var); can cast name to global but not recommended (not thread safe) https://realpython.com/python-pass-by-reference/#replicating-pass-by-reference-with-python
* _variable shadowing_: prevent access to same name in higher scope [Smalleshire 5.5 @ 2:30]; use `global` to refer to globally scoped name in event of shadowing
```python
foo = 'foo val'  # global foo
def fail_to_set_foo():
    foo = 'new val'  # local foo

fail_to_set_foo()
foo  # global foo untouched
```

# IMPORTS

📙 Beazley ch. 10
📜 https://docs.python.org/3/reference/import.html https://docs.python.org/3/library/imp.html
`py-repetitive-paths.md`

* types https://realpython.com/absolute-vs-relative-python-imports
```python
# relative = dot notation to specify location
from ..pkg import func

# absolute = 
# circular = 
```

* _absolute_: import from `sys.path`
* _relative_: specify location of module being imported relative to module doing the importing https://realpython.com/absolute-vs-relative-python-imports/ https://stackoverflow.com/q/1918539/6813490 https://stackoverflow.com/questions/14132789/relative-imports-for-the-billionth-time
* explicit vs. implicit https://realpython.com/absolute-vs-relative-python-imports/#relative-imports
❓ when do we need `.` for modules in same dir? https://www.youtube.com/watch?v=rGQKHpjMn_M @ 7:30
* _circular_: https://www.pythoninsight.com/2018/04/how-import-works-differently-in-python-3-5/ https://realpython.com/courses/python-imports-101/ https://seddonym.me/2019/05/20/meet-import-linter/

---

* https://rednafi.github.io/reflections/how-not-to-run-a-script-in-python.html
* people know they suck https://lucumr.pocoo.org/2018/7/13/python/
* speed up imports https://rednafi.github.io/reflections/caching-connection-objects-in-python.html
* _tldr_: most advice about import and project structure are for libraries (vs. apps or executables) https://www.youtube.com/watch?v=QX_Nhu1zhlg @ 16:30
* _multiline_: use parens
* import from module in same dir: `from .module import SomeClass`
* get names defined in module: `dir(sys.modules[__name__])` https://stackoverflow.com/a/991158 🗄 `algos`

symbol table
* _private_: all obj in module 
* _public_: obj in mod avaiable when import mod https://realpython.com/python-modules-packages/#the-import-statement https://docs.python.org/3/library/functions.html#locals
* `locals()`: local symbol table https://docs.python.org/3/library/functions.html#locals
* `globals()`: global symbol table
* `dir()`: locals() w/ out values https://stackoverflow.com/a/21961813 https://realpython.com/python-modules-packages/#the-dir-function

---

https://tenthousandmeters.com/blog/python-behind-the-scenes-11-how-the-python-import-system-works/
* _sink_: https://realpython.com/python-modules-packages https://docs.python.org/3/tutorial/modules.html#packages

__people know that the import system sucks__

http://lucumr.pocoo.org/2018/7/13/python/

> The fact that most methods of invoking Python code from the command line break when that code is inside a package, and the two that do work are highly sensitive to the current working directory is all thoroughly confusing for a beginner. I personally believe it is one of the key factors leading to the perception that Python packages are complicated and hard to get right. http://python-notes.curiousefficiency.org/en/latest/python_concepts/import_traps.html Nick Coghlan (CPython dev)

> The problem is that where on your system you need to put a Python library module in order so that a Python main program (or other library) can see it and load it varies in only semi-predictable ways. By version, yes, but there’s also an obscure distinction between site-packages, dist-packages, and what for want of any better term I’ll call root-level modules (no subdirectory under the version directory) that different distributions and even different application packages seem to interpret in different and incompatible ways. The root of the problem seems to be that good practice is under-specified by the Python dev team. - http://esr.ibiblio.org/?p=8161 Eric Raymond

__namespaces__

* `import foo` binds module obj `foo` to name `foo` in current namespace [Smallshire 1 @ 5.7 0:20]
* `import f` binds module obj `foo` to name `f` in current namespace
* `import mod`: place module itself into caller's symbol table; doesn't place `mod` private symbol table into the caller i.e. need to use dot notation to drill down to symbol table `mod.obj1` https://realpython.com/python-modules-packages/#the-import-statement
* `from <mod> import <obj>`: place obj from module into caller's symbol table https://realpython.com/python-modules-packages/#the-import-statement

https://realpython.com/python-namespaces-scope/
https://learndjango.com/tutorials/django-best-practices-imports
https://realpython.com/python-import/
https://github.com/dabeaz-course/practical-python/blob/master/Notes/Contents.md
* _import module from same directory_: `from .views import TemplateView` https://djangoforbeginners.com/pages-app/
* _import obj from module in sibling directory_: pkg.mod.Obj https://djangoforbeginners.com/hello-world/

* https://www.youtube.com/watch?v=rGYbrIf-y58
cool project https://github.com/dandavison/optimistic-reload
https://github.com/benawad/destiny
* https://github.com/ankur-gupta/rain
* https://github.com/Mckinsey666/bullet/blob/master/bullet/client.py
🔗 https://github.com/zachvalenta/python-imports
* FastAPI: imports, app structure, ASGI, Stack Overflow https://stackoverflow.com/questions/tagged/fastapi?tab=votes&pagesize=50 https://developer.mongodb.com/how-to/FARM-Stack-FastAPI-React-MongoDB
* Python imports
```sh
├── dir
│   └── __init__.py
│   └── foo.py
│   └── bar.py
```
```python
# __init__.py https://github.com/Mckinsey666/bullet/blob/master/bullet/__init__.py
from .foo import obj_bar
from .bar import obj_bar

# application code https://github.com/Mckinsey666/bullet/blob/master/DOCUMENTATION.md#using-bullet-objects-
from dir import Bullet, Check, YesNo, Input
```

* https://nedbatchelder.com/text/test3/test3.html#21
* https://fastapi.tiangolo.com/tutorial/sql-databases/ https://testdriven.io/courses/tdd-fastapi/ https://testdriven.io/blog/moving-from-flask-to-fastapi/
* https://github.com/dinsaw/kines/blob/master/tests/test_metrics.py
* https://www.b-list.org/weblog/2020/feb/03/how-im-testing-2020/
* https://chrisyeh96.github.io/2017/08/08/definitive-guide-python-imports.html
* clean up create-python-app https://testandcode.com/80 https://testandcode.com/81
* the origin of digging into imports again --> works for pytest...
```sh
drwxr-xr-x     - adcbtb9 17 Dec 14:03 .
.rw-r--r--@   28 adcbtb9 17 Dec 14:03 ├── .gitignore
.rw-r--r--@   30 adcbtb9 17 Dec 13:55 ├── array.py
.rw-r--r--  1.3k adcbtb9 17 Dec 14:03 ├── Makefile
.rw-r--r--   187 adcbtb9 17 Dec 13:55 ├── requirements.txt
.rw-r--r--@   74 adcbtb9 17 Dec 13:55 └── test_array.py
```
```python
# array.py
def say_hi():
    return "hi"

# test_array.py
from array import say_hi

def test_say_hi():
    assert say_hi() == "hi"
```
```Makefile
test:
	pytest -v test_array.py
```

* ...not for coverage https://coverage.readthedocs.io/en/coverage-5.0/ coverage changes `sys.path` https://github.com/pytest-dev/pytest-cov
```Makefile
test:
	coverage run -m pytest -v test_array.py
```
```sh
ImportError while importing test module '/Users/adcbtb9/Desktop/death-by-imports/test_array.py'.
Hint: make sure your test modules/packages have valid Python names.

Traceback:
test_array.py:1: in <module>
    from array import say_hi
    ImportError: cannot import name 'say_hi' from 'array' (Python.framework/Versions/3.7/lib/python3.7/lib-dynload/array.cpython-37m-darwin.so)
```

* write an article on this and ask Brian Okken https://testandcode.com/52
* modules are only executed once, at import @ 2.11 0:25
* `__init__.py` executed when pkg imported 📍 useful to put module attr into higher namespace @ 2.12 1:15
* seems like there's only direction for pkg structure for distro (lib, exec) and not app (web, daemon) and not the-as-of-yet unnamed third category (scripts with tests?)
* execute module `python3 -m <mod>`@ 2.12 1:20
* _relative imports_: import mod from pkg w/out specifying the full module path, have to use syntax `from .mod import name`, not supposed to use @ 2.12 1:30
* `__all__`: list of attr to export when `from mod import *` is used @ 2.12 2:10
* _regular pkg_: pkg as defined before introduction of namespace pkg https://www.python.org/dev/peps/pep-0420/#terminology
* _namespace pkg_: don't use `__init__.py`, exist when dir on `PYTHONPATH` matches import and no normal pkg does, "across multiple directories" seems to mean "filepath to pkg" https://www.python.org/dev/peps/pep-0420/#abstract @ 2.12 2:20
* _executable directory_: has `__main__.py`
* `.__path__`
```sh
(venv) /U/a/D/py-imports $ t
drwxr-xr-x     - adcbtb9 16 Dec 15:58 .
.rw-r--r--@   28 adcbtb9 16 Dec 15:25 ├── .gitignore
.rw-r--r--@   30 adcbtb9 16 Dec 15:26 ├── array.py
.rw-r--r--@   68 adcbtb9 16 Dec 15:38 ├── array_test.py
drwxr-xr-x     - adcbtb9 16 Dec 16:00 ├── bar
.rw-r--r--     0 adcbtb9 16 Dec 15:59 │  ├── __init__.py
.rw-r--r--@   32 adcbtb9 16 Dec 15:59 │  └── bar.py
drwxr-xr-x     - adcbtb9 16 Dec 15:57 ├── foo
.rw-r--r--@   31 adcbtb9 16 Dec 15:58 │  └── foo.py
.rw-r--r--  1.8k adcbtb9 16 Dec 15:39 ├── Makefile
.rw-r--r--   371 adcbtb9 16 Dec 15:11 └── requirements.txt
(venv) /U/a/D/py-imports $ bpython
bpython version 0.18 on top of Python 3.7.4 /Users/adcbtb9/.local/pipx/venvs/bpython/bin/python
>>> import foo
>>> import bar
>>> foo.__path__
_NamespacePath(['/Users/adcbtb9/Desktop/py-imports/foo'])
>>> bar.__path__
['/Users/adcbtb9/Desktop/py-imports/bar']
```

## modules

📙 Van Rossum ch. 6

* _module_: file containing Python [tutorial 6.0]
* _attributes_: obj (variables, functions, classes)
* _impl_: can be written in Python or C (`re`, mathematical libs) https://realpython.com/python-modules-packages/#python-modules-overview
* _types_: user-defined, third-party, stdlib (`itertools`) https://realpython.com/python-modules-packages/#python-modules-overview
* _script_: module meant to be directly executed https://realpython.com/run-python-scripts/#scripts-vs-modules
* _import time_: when the interpreter loads module [Fluent Python 7.185] once per interpreter session https://realpython.com/python-modules-packages/#reloading-a-module on module load the entire module is executed, not only the object imported https://www.youtube.com/watch?v=44PvX0Yv368 @ 3:15

__attributes__

* `__file__`: location from which file is imported https://realpython.com/python-modules-packages/#the-module-search-path
* `__name__`: evaluates at runtime to either module name (if imported) or `__main__` (if run as script)
* `__main__.py`: module required to make pkg callable (think `pytest`) https://alex.dzyoba.com/blog/python-import/
* `__path__`: shows where pkg looks for submodules [Smallshire structure 2.2 @ 1:45]
* `__all__`: kinda like `exports` in Node; Cookbook 10.2 https://realpython.com/python-modules-packages/#importing-from-a-package
```python
def foo(): pass
def bar(): pass
__all__ = ['bar']  # only export 'bar'
```

## pkg

packages
* _package_: collection of modules https://docs.python.org/3/tutorial/modules.html#packages
* module that can contain other modules https://docs.python.org/3/reference/import.html#packages
* project w/ `setup.py` (PEP 517) https://github.com/pipxproject/pipx/issues/279#issuecomment-555254281
* project w/ `pyproject.toml` (PEP 518) https://github.com/pipxproject/pipx/issues/279#issuecomment-555254281

module search path https://docs.python.org/3/tutorial/modules.html#the-module-search-path
* 1 - stdlib: `sys.path`, PYTHONHOME https://docs.python.org/3/using/cmdline.html#envvar-PYTHONHOME
* 2 - CWD
* 3 - PYTHONPATH: exact dir vary per installation
* 4 - site-packages

---

__types__

* _regular pkg_: pkg w/ `__init__.py`
* _namespace pkg_: pkg w/out `__init__.py`; since Python 3.3
* `__init__.py`: still recommended bc more explicit; useful for initialization logic

> When a package is imported, Python runs all of the code in the package’s `__init__.py` file, if such a file exists. All of the objects defined in the module or the package’s `__init__.py` file are made available to the importer.

> You can set up this `__init__.py` file in a way that enables you to import classes and methods from the package as a whole, instead of knowing the internal module structure and importing from `helloworld.helloworld` or `helloworld.helpers` https://realpython.com/python-application-layouts/#one-off-script

__get Python to find your pkg (here be dragons)__

* put your pkg in dir contained in `sys.path` [https://realpython.com/python-modules-packages/#the-module-search-path, Smallshire structure 3.1 @ 1:30] 
* ⚠️ edit `sys.path` at runtime https://realpython.com/python-modules-packages/#the-module-search-path 
* ⚠️ edit env var https://orbifold.xyz/pythonpath.html
* `context.py` file inside test suite https://docs.python-guide.org/writing/structure/#test-suite
* um, avoid it? https://alex.dzyoba.com/blog/python-import/ https://chrisyeh96.github.io/2017/08/08/definitive-guide-python-imports.html#case-4-importing-from-parent-directory 

# ITERATION

## internals

📙 Beazley ch. 4
🔗
* https://stackoverflow.com/questions/2776829/difference-between-pythons-generators-and-iterators
* https://stackoverflow.com/questions/231767/what-does-the-yield-keyword-do/231855
* Batchelder https://www.youtube.com/watch?v=EnSu9hHGq5o
* Hunner 2016 https://treyhunner.com/2016/12/python-iterator-protocol-how-for-loops-work/
* Hunner 2017 https://www.youtube.com/watch?v=V2PkkMS2Ack
* Hunner 2018 https://treyhunner.com/2018/06/how-to-make-an-iterator-in-python/
* Hunner 2019 https://treyhunner.com/2019/06/loop-better-a-deeper-look-at-iteration-in-python/

iterables
* _iterable_: 1) impl `__iter__` 2) where `__iter__` returns iterator https://www.youtube.com/watch?v=EnSu9hHGq5o 23:45
* anything you can for loop i.e. obj that can return members sequentially e.g. collections, files https://treyhunner.com/2019/06/loop-better-a-deeper-look-at-iteration-in-python/
```python
# ❌ TypeError: 'TodoList' object is not iterable
class TodoList():
    def __init__(self, items):
        self.items = items

todos = TodoList(["buy groceries", "pickup kids"])
for todo in todos:
    print(todo)

# ❌ TypeError: iter() returned non-iterator of type 'list'
class TodoList():
    def __init__(self, items):
        self.items = items
    def __iter__(self):
        return self.items

# ✅ iterable
class TodoList():
    def __init__(self, items):
        self.items = items
    def __iter__(self):
        return iter(self.items)  # ✅ iterator
```

iterators
* _iterator_: obj that does the iterating
```python
# iterable
myl = [3, 42, 7]
# get iterator
myi = iter(myl)
# get next item (calls __next__)
next(myi)  # 3
```
* itself an iterable (impl `__iter__`) and its iterator is itself (`__next__`) https://treyhunner.com/2018/06/how-to-make-an-iterator-in-python
```python
class Count:
    def __init__(self, start=0):
        self.num = start
    def __iter__(self):
        return self
    def __next__(self):
        num = self.num
        self.num += 1
        return num

# for loop impl: 1) call __iter__ 2) call __next__ until handle StopIteration https://github.com/python/cpython/blob/ac0c6e128cb6553585af096c851c488b53a6c952/Lib/test/test_enumerate.py#L109
for n in Count():
    print(n)  # 0 1 2...
```

generators
* _generator_: https://realpython.com/introduction-to-python-generators/ 🗄 `language.md` functions
* iterator using `yield` https://jeffknupp.com/blog/2013/04/07/improve-your-python-yield-and-generators-explained/
* _generator expression_: syntactic sugar for generator function https://www.youtube.com/watch?v=EnSu9hHGq5o 24:45
* can only iterate once bc values not stored in memory https://stackoverflow.com/a/231855
```python
gen = (x for x in range(3))
for el in gen:
    print(el)  # 0 1 2
for el in gen:
    print(el)  # nothing
```
* holds single value in memory at a time (vs. lists, which hold all el in memory at once)
* useful when you just want to iterate https://realpython.com/python-coding-interview-tips/#save-memory-with-generators
* lazy iterable https://treyhunner.com/2016/11/check-whether-all-items-match-a-condition-in-python/
* type of continuation https://www.hhyu.org/posts/generator_and_continuation/
* with multiprocessing http://www.antoncohen.com/2016/10/python-generators-with-multiple-threads.html
* 📍 https://medium.com/canopy-tax/sammys-generators-in-python-57e43386b89e https://jeffknupp.com/blog/2013/04/07/improve-your-python-yield-and-generators-explained/ 

## itertools

* module for doing stuff with iterables
* https://github.com/erikrose/more-itertools/ https://www.pythoncheatsheet.org/#itertools-Module https://realpython.com/python-itertools/ https://jeffknupp.com/blog/2018/12/13/how-to-do-just-about-anything-with-python-lists/ https://towardsdatascience.com/tour-of-python-itertools-2af84db18a5e https://florian-dahlitz.de/blog/introduction-to-itertools https://www.blog.pythonlibrary.org/2021/12/07/a-tour-of-pythons-itertools-library/ https://martinheinz.dev/blog/52
```python
# COMBINATIONS AND PERMUTATIONS https://www.youtube.com/watch?v=jUM_Dpt6yu0
list(itertools.combinations(['alice', 'bob', 'candace'], r=2))  # [('alice', 'bob'), ('alice', 'candace'), ('bob', 'candace')]
list(itertools.permutations(['alice', 'bob', 'candace'], r=2))  # [('alice', 'bob'), ('bob', 'alice')...]

# ITERATE COLLECTIONS CONSECUTIVELY HTTPS://SOURCERY.AI/BLOG/EFFECTIVE-COLLECTION-HANDLING/
for foo in itertools.chain(this_one_first, then_this_one):
    do_something(foo)
```

* sum list of numbers
```python
from functools import reduce
from operator import add

round(reduce(add, [5.15, 4.2, 10.7]), 2)
```

## comp/index/slice

comprehensions
* for-loop replacement https://sourcery.ai/blog/effective-collection-handling/
* takes iterable, performs operation on each el and adds to collection (list, dict, set)
```python
# syntax
x * 42             # 3 operate
for x in iterable  # 1 iterate
if x % 2 == 0      # 2 condition

# list
my_list = [
    x * 2
    for x in my_iterable
    if x % 2 == 0
]

# set (dedupe)
my_set = { i for i in [42, 13, 7, 7, 7] }

# dictionary
my_dict = {
    i : string.ascii_letters[i]
    for i in range(3)
}

list_of_dict = [
    dict(id=i, letter=zimu[i])
    for i in range(3)]
```

indexes
* https://docs.python.org/3/tutorial/datastructures.html#looping-techniques
* https://treyhunner.com/2016/04/how-to-loop-with-indexes-in-python/
```python
# sequence
for val in seq:
for ind, val in enumerate(seq):  # aka elementwise operation
for artist, album in zip(artists, album):

# mapping https://realpython.com/iterate-through-dictionary-python
for k, v in cidian.items():
```

* `range()`
```python
# start inclusive, end exlusive
range(<start>, <stop>, <step>)

# single arg refers to 'stop'
range(1)  # iterates for zeroeth el
for _ in range(1):
    print('hey')
# hey

# two args refer to 'start' and 'stop'
for _ in range(2, 7):
    print('hey')
# hey
# hey
# hey
# hey
# hey

# three args refer to 'start', 'stop', 'step'
for _ in range(2, 7, 2):
    print('hey')
# hey
# hey
# hey

# if start is higher than stop, simple returns range obj that will iterate 0 times
for i in range(5,1):
    print(i)  # nothing happens
>>>
```

slicing
* syntactic sugar for grabbing subset of iterable
* out-of-place https://stackoverflow.com/a/5131563
```python
# syntax https://stackoverflow.com/a/509295
[start : stop : step/direction]

# start/stop
'alice'[1:]  # 'lice' -> start is inclusive
'alice'[:3]  # 'ali' -> stop is exclusive
'alice'[:-2]  # 'ali' -> stop by negative index

# step
'alice'[::1]  # 'alice' 
'alice'[::2]  # 'aie'  -> inclusive

# direction
'alice'[::-1]  # 'ecila' 
'alice'[::-2]  # 'eia'  -> can combine w/ step

# slice obj https://stackoverflow.com/a/24713353 https://stackoverflow.com/a/10573523
my_s = slice(1,3)
'alice'[my_s]  # 'li'

# doesn't throw IndexError https://wsvincent.com/python-wat-slice-out-of-range/
[42, 13, 7][:100]  # returns entire collection
[42, 13, 7][100:]  # returns empty string
```

# LIBS

📜 https://docs.python.org/dev/library/index.html
📙 Van Rossum ch. 10-11
📈 https://pythonwheels.com/
🔍 https://github.com/vinta/awesome-python

* _six_: convert from Python 2 and Python 3
* control mouse/keyboard https://github.com/asweigart/pyautogui

---

* _auth_: https://authlib.org/
* browser: `webbrowser` https://dev.to/dmahely/one-bash-command-to-start-the-day-2fni

* _config/env var_: https://github.com/theskumar/python-dotenv https://github.com/sloria/environs https://github.com/facebookresearch/hydra https://rednafi.github.io/digressions/python/2020/06/03/python-configs.html less popular cousin https://github.com/sloria/environs
```python
import os
from dotenv import load_dotenv, find_dotenv
load_dotenv(find_dotenv())  # if `.env` present in project
os.getenv("FOO_VAR")
```

* _cron_: https://github.com/zachvalenta/pypub https://github.com/maxhumber/hickory 🗄 `shell.md`
* _daemon_: https://github.com/dbader/schedule https://schedule.readthedocs.io/en/stable/faq.html#how-to-continuously-run-the-scheduler-without-blocking-the-main-thread https://towardsdatascience.com/scheduling-all-kinds-of-recurring-jobs-with-python-b8784c74d5dc
* _desktop/native_: Kivy, pyqt https://build-system.fman.io/pyqt5-tutorial PySimpleGUI https://github.com/PySimpleGUI/PySimpleGUI tkinter https://www.youtube.com/watch?v=xqDonHEYPgA
* _ETL_: bonobo https://www.bonobo-project.org/ https://www.pythonpodcast.com/bonobo-with-romain-dorgueil-episode-143/
* _hashing_: passlib https://passlib.readthedocs.io/en/stable/ https://pythonbytes.fm/episodes/show/21/python-has-a-new-star-framework-for-restful-apis
```python
# https://pythonbytes.fm/episodes/show/21/python-has-a-new-star-framework-for-restful-apis
import hashlib as hl
sha = hl.sha256()
sha.update(b'hey')
sha.hexdigest()  # 'fa690b82061edfd2852629aeba8a8977b57e40fcb77d1a7a28b26cba62591204'
```

* _markdown_: https://pypi.org/project/markdown2/ used this one for `m2h` https://github.com/Python-Markdown/markdown had issues with ampersands in URLs, see repo commit `43e` https://stackoverflow.com/a/20593644/6813490 https://stackoverflow.com/questions/39086/search-and-replace-a-line-in-a-file-in-python
* _networking_: Scapy https://www.youtube.com/watch?v=EnuF9ZR6MVc psutil https://matt.sh/netmatt#_what-if-we-replaced-90s-c-netstat-with-python
* _notifications_: https://github.com/notifiers/notifiers
* _photos_: https://github.com/sedthh/pyxelate 
* _PDF_: https://realpython.com/pdf-python/ https://github.com/Halolegend94/pdf4py

* _random_: https://realpython.com/courses/generating-random-data-python/ https://eli.thegreenplace.net/2010/01/22/weighted-random-generation-in-python
```python
choice([True, False])  # pick one
randomint(1, 10)  # pick one from range
sample(["hey", "hi", "hello", "hiya"], 2)  # pick n
''.join([choice(string.ascii_letters + string.digits) for n in range(32)])  # random string
```
```python
import string
from random import choices, choice

char = string.ascii_letters + string.digits  # 'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789'

# choices - return subset https://www.youtube.com/watch?v=rGQKHpjMn_M @ 13:15
choices(char, k=3)  # ['F', 'g', 'z']
''.join(choices(char, k=3))  # '1d3'

# choice - return single el
choice(char)  # 'z'
choice(char, k=3)
Traceback (most recent call last):
  File "<input>", line 1, in <module>
    choice(char, k=3)
TypeError: choice() got an unexpected keyword argument 'k'
```

* _scheduling_: https://docs.python.org/3/library/sched.html https://github.com/dbader/schedule
* _unit conversion_: https://pint.readthedocs.io/en/0.10.1/
* _zip/tar_: https://github.com/BuzonIO/zipfly

## built-in

📜 https://docs.python.org/3/library/functions.html

* _dir()_: list obj attr
* _next()_: call `__next__`

## CLI

🗄 `shell.md`

frameworks
* CLI from obj: https://github.com/google/python-fire https://github.com/chriskiehl/Gooey https://github.com/BstLabs/py-dynacli
* interpreter / shebang
```sh
# https://realpython.com/run-python-scripts/#using-the-script-filename
#!/usr/bin/python --> explicit path
#!/usr/bin/env python --> use whatever python on $PATH
```

input 🗄 `security.md` sanitization
* basic: `ur_in = input()`
* filter: https://github.com/amjith/fuzzyfinder https://github.com/j-bennet/wharfee/blob/master/setup.py https://github.com/davidhalter/jedi https://www.pythonpodcast.com/episode-113-jedi-code-completion-with-david-halter/ https://github.com/seperman/fast-autocomplete 🗄 `shell.md` filter
* interactive prompt https://github.com/Mckinsey666/bullet https://github.com/tmbo/questionary
* frameworks: Click, prompt-toolkit (used by pgcli, http-prompt, https://github.com/j-bennet/wharfee/blob/master/setup.py)

output
* format https://github.com/Textualize/textual https://github.com/Textualize/rich https://talkpython.fm/episodes/show/336/terminal-magic-with-rich-and-textual
* markdown rendering https://github.com/charmbracelet/glamour https://github.com/charmbracelet/glow
* progress bar https://dev.to/rsalmei/a-cool-new-progress-bar-for-python-1c0g https://github.com/tqdm/tqdm https://github.com/rsalmei/alive-progress https://pypi.org/project/enlighten/
* colors (really matter cf. pastel) https://github.com/timofurrer/colorful https://github.com/erikrose/blessings
* fmt https://github.com/willmcgugan/rich
* tables https://github.com/astanin/python-tabulate
* styling https://github.com/pterm/pterm/ https://github.com/charmbracelet/lipgloss
* progress bar
```python
if i % 100 == 0:
    progress = ((i + 1) / float(len(qd))) * 100.0
    print('%.2f%%' % progress)
```

TUI https://github.com/rothgar/awesome-tuis
* curses (UNIX) ncurses (Linux) https://docs.python.org/3/howto/curses.html https://github.com/cmus/cmus https://github.com/jesseduffield/lazydocker https://github.com/NerdyPepper/dijo
* https://github.com/willmcgugan/textual
* https://github.com/bczsalba/pytermgui
* https://github.com/peterbrittain/asciimatics
* http://urwid.org/ used for pudb
* https://github.com/mum4k/termdash https://github.com/jroimartin/gocui
* frameworks from other languages https://github.com/fdehau/tui-rs https://github.com/gyscos/Cursive https://github.com/gizak/termui https://github.com/Phantas0s/devdash
* Bloomberg terminal https://whoo.ps/2021/03/21/you-merely-adopted-dark-mode

Click https://click.palletsprojects.com/en/8.1.x
* basic
```python
# run: python script.py
#!/usr/bin/env python
import click

@click.command()
def main():
    print("hey zach")

if __name__ == "__main__":
    main()
```
* multiple commands
```python
# run: python script.py hello alice

@click.group()
def cli():
    pass

@cli.command()
@click.argument("person")
def hello(person):
    """say hello"""
    print(f"hi, {person}")

@cli.command()
@click.argument("person")
def goodbye(person):
    """say goodbye"""
    print(f"goodbye, {person}")

if __name__ == "__main__":
    cli()
```
* args vs. options https://click.palletsprojects.com/en/8.1.x/parameters/
* types: str, int https://click.palletsprojects.com/en/8.1.x/parameters/#parameter-types
> I'm not using these semantically, using options in lieu of args bc options have better syntax on command invocation
```python
# ARGS: python path/to/script.py path/to/file
@click.command()
@click.argument("in-file", type=click.Path(exists=True))
def main(in_file):
    """input file"""  # https://click.palletsprojects.com/en/8.1.x/documentation/

# OPTIONS: python path/to/script.py -in-file path/to/file
@click.command()
@click.option("-in-file", required=True, type=str, help="input file")
def main(in_file):
```
* read from anywhere, write to local dir
```python
# run: python script.py -in_path path/to/file.txt -out_file new_file.txt
@click.command()
@click.option("-in_path", required=True, type=str, help="path to input file")
@click.option("-out_file", required=True, type=str, help="output filename")
def main(in_path, out_file):
    path_input = os.path.normpath(in_path)
    path_output = os.path.join(os.getcwd(), out_file)
    with open(path_output, mode="w") as csv_out:
        with open(path_input, mode="r") as csv_in:
```

argparse
* alternatives: https://github.com/tiangolo/typer old (`sys.argv`, optparse, docopt)
* testing: https://github.com/dbader/photosorter/blob/master/test_sorter.py https://www.youtube.com/watch?v=ApTZib0L2X8 4:00
* `description`: one-liner on purpose of CLI http://dustinrcollins.com/testing-python-command-line-apps
* `action=store_true`: boolean https://stackoverflow.com/a/15008806/6813490 https://stackoverflow.com/a/36710639/6813490
* `metavar=''`: avoid weird upppercasing https://docs.python.org/3/library/argparse.html#metavar
* scaffold
```python
def parse():
    parser = ArgumentParser()
    parser.add_argument("-f", "--file", help="file")
    parser.add_argument("-s", "--start", help="start trim")
    parser.add_argument("-e", "--end", help="end trim")
    if len(argv) == 1:
        parser.print_help()
        exit()
    return parser.parse_args()

args = parse()
main(file=args.file, start=args.start, end=args.end)
```

## datetime

📙 Beazley ch. 3
https://pypi.org/project/pytz/ https://github.com/crsmithdev/arrow https://github.com/timofurrer/maya https://github.com/sdispater/pendulum https://github.com/dateutil/dateutil

```python
# iterate months in range https://stackoverflow.com/a/35651063
import datetime as dt
from dateutil.relativedelta import relativedelta as delta
def iter_months(year, month, day):
    month_start = dt.date(year, month, day)
    month_previous_dt = dt.datetime.utcnow().replace(day=1) - delta(days=1)
    month_previous = month_previous_dt.date()
    while month_start <= month_previous:
        do_something()
        month_start += delta(months=1)

# string to date
nov_2019 = dt.strptime("2019 Nov", "%Y %b")  # datetime.datetime(2019, 11, 1, 0, 0)
nov_2019.strftime("%Y %m")  # "22 03"

datetime.date(2021, 12, 1).strftime("%b %Y").upper()

month_start = "2019 11"
month_end = dt.now().strftime("%Y %m")  # "22 03"

start = dt.date(2019,11,1)
end = dt.now()

# create timestamp
from datetime import datetime as dt
dt.now().isoformat()
ts = int(dt.timestamp(dt.today()))
import time
ts = int(time.time())

# timestamp to Python https://docs.python.org/3/library/datetime.html#datetime.date.fromtimestamp
dt.date.fromtimestamp(ts)
date.fromisoformat('2019-12-04')  # not in 2.7

# formatting https://strftime.org/ https://stackoverflow.com/a/48947064
this_month = dt.now().strftime('%m')

# pad string https://stackoverflow.com/a/339024
last_month = str(int(this_month) - 1).rjust(2, '0')
two_months_ago = str(int(this_month) - 2).rjust(2, '0')

# compare timestamp to current time
from datetime import datetime, timezone
now = datetime.now(timezone.utc)  # https://stackoverflow.com/a/25662061

from dateutil import parser
task = parser.isoparse("2021-06-04T18:10:19.885484Z")
# datetime.datetime(2021, 6, 4, 18, 10, 19, 885484, tzinfo=tzutc())

diff = now - task
diff.seconds
```

## files

📙 Beazley ch. 5

* basics
```python
# read
with open("input.csv", mode="r") as f:
    reader = csv.reader(f)
    for row in reader:
        pass

# write
with open("output.csv", mode="w") as f:
    writer = csv.writer(f)
    writer.writerow(["foo", "bar"])  # headers
    writer.writerows(myl)
```

* DictWriter expects a list of dictionaries
```python
# ❌
artists_1371 = artists_1025 - artists_1124
with open("03-artists-1371.csv", "w") as csv_1371:
    writer = csv.DictWriter(csv_1371, fieldnames=["artist"])
    writer.writeheader()
    for el in foo:
        writer.writerow(el)
    
# ✅
artists_1371 = artists_1025 - artists_1124
artists = [dict(artist=x) for x in artists_1371]
with open("03-artists-1371.csv", "w") as csv_1371:
    writer = csv.DictWriter(csv_1371, fieldnames=["artist"])
    writer.writeheader()
    for el in artists:
        writer.writerow(el)

# ❌ how to write string to single header vs. iterate string across n headers?
with open("03-artists-1371.csv", "w") as csv_1371:
    writer = csv.writer(csv_1371)
    writer.writerow(["artist"])
    for el in artists_1371:
        print(type(el))
        writer.writerow(el)
        
# ✅ write list of strings
with open("um_only.csv", mode="w") as f:
    writer = csv.writer(f)
    writer.writerow(["isrc"])  # takes iterable
    for dl in um_only:
        writer.writerow([dl])  # takes iterable
```
* parse Click file
```python
def parse_click_file(f):
    return [
        {"foo": row["FOO"], "bar": row["BAR"], "baz": row["BAZ"]}
        for row in csv.DictReader(f)
    ]
```
* CSV
```python
# read
with open(file_path, mode="r", encoding="utf-8-sig") as f:
    reader = csv.DictReader(f)
    headers = reader.fieldnames
    for row in reader:
        do_something(row[header])

# write
with open(file_path, "w") as f: 
    headers = ["SKU", "name", "earnings"]
    writer = csv.DictWriter(f, fieldnames=headers) 
    writer.writeheader()
    for dl in data_lines:
        writer.writerow(dl)

# read from + write to
with open(file_path, "w") as csv_out: 
    with open(file_path, mode="r") as csv_in:
        reader = csv.DictReader(csv_in)
        writer = csv.DictWriter(csv_out, fieldnames=reader.headers + ["header_for_out"]) 
        writer.writeheader()
        for row in reader:
            data_line = OrderedDict(do_something(row))
            writer.writerow(data_line)

# write list of dict to file
with open(file_path, "w") as f: 
    headers = ["SKU", "name", "earnings"]
    writer = csv.DictWriter(f, fieldnames=headers) 
    writer.writeheader()
    for dl in data_lines:
        writer.writerow(dl)

# create output headers and link to input headers
def generate_headers(headers):
    headers_IO = od()
    for header in headers:
        if "TOTAL AMOUNT" in header:
            mmyy = "ta_{}".format("_".join(header.split(" ")[2:]).lower())
            headers_IO[mmyy] = header
    return headers_IO

# create output headers based on date range and link to input headers
def generate_headers(year, month, day):
    headers = od()
    month_start = dt.date(year, month, day)
    month_previous_dt = dt.datetime.utcnow().replace(day=1) - delta(days=1)
    month_previous = month_previous_dt.date()
    while month_start <= month_previous:
        k = "out_{}".format(month_start.strftime("%Y%m")[2:])
        v = "in {}".format(month_start.strftime("%b %Y").upper())
        headers[k] = v
        month_start += delta(months=1)
    return headers

# add generated headers to hard-coded
generated = generate_headers(reader.fieldnames)
writer = csv.DictWriter(csv_out, fieldnames=get_headers(generated=generated.keys()))
def get_headers(generated):
    return [
        "foo",
        "bar",
    ] + generated

# sum across generated headers
gen_rows, total = sum_gen(gen=generated, row=row)
def sum_gen(gen, row):
    total = 0
    rows = od()
    # k = output header, v = input header
    # e.g. "out_nov_21" : "IN NOV 21"
    for k, v in gen.items():
        # row = "id":"id", "IN NOV 21": "42", "IN DEC 21": "7"
        rows[k] = row[v]  # out_nov_21: 42
        if row[v] != "":
            total += float(row[v])
    return rows, round(total, 2)
```

* HTTP
```python
# write response
res = requests.get(url)
with open(file_name, mode="wb") as f:
    f.write(res.content)

# read IO https://stackoverflow.com/a/21843713
byte = io.BytesIO(res.content).read()
text = byte.decode("utf-8-sig")
string_obj = io.StringIO(text)
reader = csv.DictReader(string_obj)
for row in reader:
```

## Git

📜 https://gitpython.readthedocs.io/en/stable/tutorial.html https://github.com/gitpython-developers/GitPython

```python
# clone https://stackoverflow.com/a/41252521 https://stackoverflow.com/a/34424094
# clone_from https://github.com/search?q=clone_from+gitpython&type=Code https://gitpython.readthedocs.io/en/stable/reference.html#git.repo.base.Repo.clone_from
from pathlib import Path
from git import Git, Repo

# download repo as tarball
res = requests.get(
    'https://gitlab.com/zachvalenta/pre-commit-test/repository/archive.tar.gz?ref=master',
    headers={'PRIVATE-TOKEN': access_token}
)
if res.url == "https://gitlab.com/users/sign_in":
    print("set token")
    os._exit(0)
with open(r'zjv_test.tar.gz', 'wb') as f:
    f.write(res.content)

# ssh
path = Path.cwd().joinpath('cloned-repo')
path.mkdir(exist_ok=True)
pk = Path.home().joinpath('.ssh/id_rsa')
with Git().custom_environment(GIT_SSH_COMMAND=f"ssh -i {pk}"):
    Repo.clone_from(
        url='git@github.com:zachvalenta/flask-CRUD.git', 
        branch='master',
        to_path=path, 
    )

# access token
path = Path.cwd().joinpath('cloned-repo')
path.mkdir(exist_ok=True)
Repo.clone_from(
    url='https://username:access_token@gitlab.com/gnachman/iterm2.git',
    branch='master',
    to_path=path, 
)

# commit hash https://stackoverflow.com/a/31957784/6813490
repo = Repo(path_to_cloned_repo)
repo.git.rev_parse(repo.head.object.hexsha, short=1)

# diff commits
# clients need `.git` on file system https://www.christianengvall.se/check-for-changes-on-remote-origin-git-repository/ https://stackoverflow.com/a/16315536/6813490 https://gitpython.readthedocs.io/en/stable/reference.html#git.remote.Remote https://github.com/gitpython-developers/GitPython/issues/373
# Gitlab needs access token, not deploy key
res = subprocess.Popen('git ls-remote origin -h refs/heads/master', shell=True, stdout=subprocess.PIPE, stderr=subprocess.STDOUT)
res.stdout

# get branch from remote https://stackoverflow.com/a/60735120
from pathlib import Path
from git import Repo

p = Path.cwd()
repo = Repo(p)
repo.git.ls_remote("--heads", "origin", "master")
```

## HTML

🗄 `html-css.md`

BeautifulSoup 📜 https://www.crummy.com/software/BeautifulSoup/bs4/doc/
* parse HTML
* can also do scraping
* way to simulate an API for a site that doesn't have one
* install: `pip install beautifulsoup4`
* ampersand issue https://stackoverflow.com/a/7188419/6813490
```python
# insert: add element inside of another element https://www.crummy.com/software/BeautifulSoup/bs4/doc/#insert
div.insert(1, ul)

# https://www.crummy.com/software/BeautifulSoup/bs4/doc/#append
# https://www.crummy.com/software/BeautifulSoup/bs4/doc/#extend
# CSS https://stackoverflow.com/a/53635461
# add at end https://stackoverflow.com/a/4320313/6813490
```

scrape
* _scrape_: 
* Scrapy
* table data https://www.visidata.org/blog/2020/ten/#4-scrape-html-table-data-from-a-webpage
* _Git scraping_: version control your scrapes https://simonwillison.net/2020/Nov/14/personal-data-warehouses/ 16:15

parse
* BeautifulSoup
* filter on selector like jq https://github.com/mgdm/htmlq
* summary data https://github.com/buriy/python-readability

---

* _shot-scraper_: automated screenshots https://github.com/simonw/shot-scraper
🔗 https://realpython.com/python-web-scraping-practical-introduction/

* _scale_: Scraping Hub https://blog.scrapinghub.com/web-scraping-at-scale-lessons-learned-scraping-100-billion-products-pages
* _legal_: anti-bot counter measures to actual legal hot water ('crawling' is the preferre nomenclature, 'scraping' has a bad rep)  https://benbernardblog.com/web-scraping-and-crawling-are-perfectly-legal-right/

alternatives
* https://github.com/jamesturk/spatula
* https://github.com/codelucas/newspaper/ https://www.pythonpodcast.com/newspaper-data-extraction-episode-280/ https://github.com/maxhumber/gazpacho https://github.com/howie6879/aspider https://github.com/MontFerret/ferret
* pup https://github.com/ericchiang/pup

Scrapy
* _Scrapy_: framework, not lib 🗄 `language.md` req are async
* _scraper_: portion of data (for some other use); small data sets
* _crawler_: all the data (to index as is); big data sets
* _spider_: impl; how your want to scrape site; different types https://blog.scrapinghub.com/web-scraping-at-scale-lessons-learned-scraping-100-billion-products-pages

* help: `scrapy`
* init project: `scrapy startproject foo` -> has same gotcha as Flask!
* run - REPL: `scrapy shell`
* run - script: `scrapy crawl <spider_name>` (from dir holding `scrapy.cfg)
* make request: `fetch(<URL>)`
* select DOM element from response: `response.css('<selector>')`
* extract text from DOM element: `response.css('<selector>').extract()`
* rm tags: `from w3lib.html import remove_tags` 🔗 https://stackoverflow.com/a/33309310/6813490
* rm newline: `.replace('\n', '')` 🔗 https://stackoverflow.com/a/1249740
* to break through lifecyle https://stackoverflow.com/a/35871117/6813490 https://stackoverflow.com/a/7969243/6813490

Selenium
* other browser automation tool https://github.com/checkly/headless-recorder
* why? dynamic content https://stackoverflow.com/questions/6682503/click-a-button-in-scrapy https://stackoverflow.com/questions/17975471/selenium-with-scrapy-for-dynamic-page https://stackoverflow.com/questions/30345623/scraping-dynamic-content-using-python-scrapy
* Firefox driver https://github.com/mozilla/geckodriver/releases
* find binary https://stackoverflow.com/a/40208762/6813490 https://stackoverflow.com/a/22130211/6813490
* docs https://selenium-python.readthedocs.io/waits.html https://www.seleniumhq.org/docs/
* inspect autocomplete https://stackoverflow.com/q/34911553/6813490
* cannot select el by text https://stackoverflow.com/q/1520429
* `By.CSS_SELECTOR` https://stackoverflow.com/a/40708217
* dropdown not inspectable in dev tools https://stackoverflow.com/questions/34911553/not-able-to-inspect-debug-autocomplete-option-elements
* finding binary https://stackoverflow.com/a/22130211/6813490
* tutorial https://intoli.com/blog/running-selenium-with-headless-chrome/

## logging

* https://monadical.com/posts/ins-and-outs-of-logging-in-python-part-one.html
* logs sent by default to `sys.stdout` i.e. they're buffered https://stackoverflow.com/a/51362214/6813490
* pretty stdout https://github.com/onelivesleft/PrettyErrors
* can unbuffer w/ `PYTHONUNBUFFERED=1` https://docs.python.org/3/using/cmdline.html?highlight=pythonunbuffered#envvar-PYTHONUNBUFFERED
* this shows up in Docker, Docker won't show logs from Flask dev server in real-time unless logs set to unbuffered although I don't know why https://github.com/sclorg/s2i-python-container/issues/157 https://learndjango.com/tutorials/django-docker-and-postgresql-tutorial
* add logs without updating source https://github.com/yiblet/inquest
* _libraries_: https://stackoverflow.com/a/51362214 https://github.com/Delgan/loguru https://github.com/BNMetrics/logme https://github.com/hynek/structlog https://github.com/itamarst/eliot stdlib https://docs.python.org/3/howto/logging.html https://docs.python.org/3/howto/logging-cookbook.html GUI https://github.com/busimus/cutelog

## operating system

📙 Beazley ch. 13
🔗 https://docs.python.org/3/library/pathlib.html#correspondence-to-tools-in-the-os-module

```python
# mkdir in cwd
os.mkdir(os.path.join(os.getcwd(), dir_name))
```

----

* _check Python version from script_: `sys.version` https://stackoverflow.com/a/1093331/6813490
* _sink_: https://realpython.com/python-pathlib/ https://treyhunner.com/2018/12/why-you-should-be-using-pathlib/ https://treyhunner.com/2019/01/no-really-pathlib-is-great/
* _why path libs are useful_: avoid dealing with different directory delimiters per OS [Sweigart automate 8.174]
* _how to represent paths_: Python can represent paths as strings (like os) https://realpython.com/python-pathlib/#the-problem-with-python-file-path-handling but Pathlib doesn't https://snarky.ca/why-pathlib-path-doesn-t-inherit-from-str/ in Python 2 binary and textual data were implicitly compatible and that caused problems https://snarky.ca/why-pathlib-path-doesn-t-inherit-from-str/
* _Pathlib_: most functionality in `path`

* recipes
```python
from pathlib import Path

cwd = Path.cwd()  # get cwd
file_names = [x.name for x in cwd.glob("**/*.csv")]  # get CSV filenames https://docs.python.org/3/library/pathlib.html#basic-use

# get filenames https://stackoverflow.com/a/50876889/6813490

#########

# env
os.environ  # get all
os.environ[]  # get 1 - throws err
os.environ.get()  # get 1 - no err
os.getenv("target", "default")  # get 1 - defaults if target not found

# dir
Path.cwd()  # $CWD
Path.home()  # ~
os.listdir()  # ls

basepath = path.dirname(__file__)
austen = path.abspath(path.join(basepath, "..", "austen.json"))  # file from parent dir https://stackoverflow.com/a/4381638

austen = os.path.join(os.path.dirname(__file__), "austen.json")  # file from CWD - can occlude but flaky if open w/ just `open(file)`, although doesn't seem like it should be, maybe not a problem w/ pathlib https://stackoverflow.com/a/1315401 
with open(austen) as f:
    return json.load(f)

Path.cwd().joinpath('foo').mkdir()  # mkdir named 'foo'
Path.cwd().joinpath('foo').mkdir(exist_ok=True)  # mkdir - don't err out if already exists (won't overwrite, just won't do anything)
Path.cwd().joinpath('foo').mkdir(parents=True)  # mkdir - make all necessary subdirectories

Path.home().joinpath("Desktop").exists()  # check if dir exists
Path.home().joinpath("Desktop").joinpath("foo.txt").is_dir()  # check if file is dir
path_to_file.rename(path_to_new_location.joinpath('file-name-at-new-location.txt'))  # mv

Path.unlink(path_to_file)  # rm file
Path.rmdir(path_to_dir)  # rmdir - empty https://docs.python.org/3/library/pathlib.html#pathlib.Path.rmdir 
shutil.rmtree(path)  # rmdir - not empty https://stackoverflow.com/a/303225/6813490 https://stackoverflow.com/a/25172642/6813490

# files
os.path.isfile(f)  # check if file
os.path.exists(f)  # check if file exists
os.listdir()  # list files in dir

open(path, mode).read()  # read - modes include w (write) r (read)
open('ur-file.txt', 'w').close()  # create empty
print(open(path, mode).read())  # print
open(path, mode).read().split(" ")  # tokenize https://stackoverflow.com/a/55723307/6813490
f.readline()   # first line https://stackoverflow.com/a/19044550

###
# CONTEXT MANAGER
# clean up unmanaged resources (like file streams)
# r (read; default) b (binary) w (create new) w+ (create new if doesn't exist https://stackoverflow.com/a/2967249
# BYO https://rednafi.github.io/digressions/python/2020/03/26/python-contextmanager.html
###
with open('data.txt', 'w') as f:
    data = 'some data to be written to the file'
    f.write(data)

# misc
shutil.make_archive(root_dir=dir_to_tar, base_name=tarball_name, format='zip')  # make zip
os.system  # run script; subprocess, Sultan also work https://stackoverflow.com/a/56842257/6813490
tarballs = [os.base.pathname(x) for x in glob(f"{Path.cwd().joinpath('foo')}/*.tar.gz")] # grab file names sans full path https://stackoverflow.com/a/55439309/6813490 https://stackoverflow.com/a/20384686/6813490
```

* _exit code_: `sys.exit(0)` or `os._exit(0)` https://stackoverflow.com/a/49950466/6813490
* _create temp dir/file_: dir (`dir` here specifies location, not sure how to name) `tempfile.mkdtemp(dir='.')` put file in temp dir `tempfile.mkstemp(dir='mytempdir')`
* iterate
```python
with open('foo.txt') as f:
    for line in f.readlines():
        print(line)
```
* iterate and update https://stackoverflow.com/a/20593644/6813490
```python
import fileinput

with fileinput.FileInput(filename, inplace=True, backup='.bak') as file:
    for line in file:
        print(line.replace(text_to_search, replacement_text), end='')
```

## regex

🗄 `algos`, `algos.md` regex

---

* methods
```python
import re

regex = re.compile(r"zach")  # ❓ why compile?
regex.search("zach another thing zach 1234").group()  # first match
regex.findall("zach another thing zach 1234")  # all matches
```
* https://github.com/tfeldmann/simplematch
* _alternatives_: https://github.com/kootenpv/textsearch https://github.com/r1chardj0n3s/parse
* _best practices_: use raw strings (c.f. 'strings') verbose mode https://docs.python.org/2/library/re.html#re.VERBOSE
* _match_: what your regex matched
* _group_: portion of match available if you've used groups in your regex https://stackoverflow.com/a/29108/6813490
* `sub`: https://stackoverflow.com/a/16720752/6813490
* `.match()`: apparently good for searching telephone numbers, anything that's not a sentence https://howchoo.com/g/zdvmogrlngz/python-regexes-findall-search-and-match but otherwise no one uses https://stackoverflow.com/questions/180986/what-is-the-difference-between-re-search-and-re-match inconsistent w/ how regex work in Perl, sed, grep https://stackoverflow.com/a/37363575/6813490 allegedly faster than `search()` but not so! https://stackoverflow.com/a/49710946/6813490
* _sink_: https://regexone.com/references/python 🗄 `python-regex.pdf` https://docs.python.org/3/howto/regex.html http://xahlee.info/python/python_regex_flags.html

## serialization

📙 Beazley ch. 6
🗄 `system.md` serialization
📜 https://docs.python.org/3/library/json.html https://docs.python.org/3/library/persistence.html

* fmt https://orbifold.xyz/check-in-json.html
```sh
python -m json.tool myfile.json > myfile.json.formatted
```
```python
def test_formatting():
    with open("myfile.json") as fp:
        raw = fp.read()
    content = json.loads(raw)
    redumped = json.dumps(content, indent=4) + "\n"
    assert raw == redumped
```

---

* https://www.mistql.com/
* https://github.com/ijl/orjson
* https://hakibenita.com/django-rest-framework-slow

general
* _serialization_: convert btw obj and interchange format 🗄 `system.md`
* _types_: to json, to token `s.dumps({'user_id': 1})` 📺 Schafer video
* `dumps()`: serialize
* `loads()`: deserialize JSON
* `load()`: deserialize file
* pickle https://nedbatchelder.com/blog/202006/pickles_nine_flaws.html

* _1-M_: https://stackoverflow.com/a/37802227/6813490 https://stackoverflow.com/a/44511616/6813490 https://marshmallow.readthedocs.io/en/latest/nesting.html 
* _filter nested_: https://stackoverflow.com/q/57851811/6813490
* _sink_: https://www.kimsereylam.com/python/2019/10/25/serialization-with-marshmallow.html https://www.pythonpodcast.com/marshmallow-data-validation-episode-200/

__Marshmallow__

* docs: https://marshmallow.readthedocs.io/en/stable
* _alternatives_: https://news.ycombinator.com/item?id=14477434 stdlib https://news.ycombinator.com/item?id=14477434

libs for Flask
* _1 - Marshmallow_: base library https://github.com/marshmallow-code/marshmallow
* _2 - Marshmallow-SQLAlchemy_: lib for SQLAlchemy https://github.com/marshmallow-code/marshmallow-sqlalchemy
* _3 - Flask-Marshmallow_: lib for Flask-SQLAlchemy https://github.com/marshmallow-code/flask-marshmallow
> ❓ need both 2 and 3 to work w/ Flask https://www.youtube.com/watch?v=kRNXKzfYrPU 7:00 or just base lib? https://marshmallow.readthedocs.io/en/2.x-line/examples.html#quotes-api-flask-sqlalchemy

* Flask how to
```python
# CONNECT TO MODELS
# declaration must come after model https://stackoverflow.com/questions/59455520/flask-sqlalchemy-marshmallow-error-on-relationship-one-to-many
class Artist(db.Model):
    artist_id = db.Column(db.Integer, primary_key=True)
    name = db.Column(db.String(30))
    songs = db.relationship("Song", backref="artist")

    def __repr__(self):
        return f"id {self.artist_id} name {self.name}"

class ArtistSchema(ma.ModelSchema):
    class Meta:
        model = Artist

# nested
class SongSchema(ma.ModelSchema):
    class Meta:
        model = Song

    artist = ma.Nested(ArtistSchema)

# INIT
# Flask-SQLAlchemy before Flask-Marshmallow https://flask-marshmallow.readthedocs.io/en/latest/
db = SQLAlchemy(app)
ma = Marshmallow(app)

# SERIALIZE
# initialization must be <model>_schema
artist_schema = ArtistSchema()  # 1
artist_schema = ArtistSchema(many=True)  # n
artist_schema = ArtistSchema(only=("name", "songs"))  # subset

# DESERIALIZE https://marshmallow.readthedocs.io/en/3.0/quickstart.html#deserializing-objects-loading
# validate https://www.cameronmacleod.com/blog/better-validation-flask-marshmallow https://medium.com/bitproject/recently-i-created-a-restful-api-with-flask-where-my-models-had-many-parameters-75da1db870b7
```

## visualization

🔍 https://pyviz.org/
🗄
* `computers.md` information theory
* `math.md` cartesian plane
* `shell.md` CLI design

types https://python-graph-gallery.com https://pbpython.com/python-vis-flowchart.html
* bar: count 
* scatterplot: correlation btw 2 var 
* histogram
* radar https://matplotlib.org/matplotblog/posts/stellar-chart-alternative-radar-chart/
* stock and flow https://www.youtube.com/watch?v=ng6jML-Rklk 25:30

GUI
* _Matplotlib_: more complex, powerful
* _Seaborn_: built on Matplotlib but easier
* _Bokeh_: not built on Matplotlib but also easier https://www.youtube.com/watch?v=2TR_6VaVSOs https://realpython.com/courses/interactive-data-visualization-python-bokeh/ https://pbpython.com/bokeh-bullet-waterfall.html
* _Altair_: requires Jupypter http://fernandoi.cl/blog/posts/altair/ --> ggplot2 https://github.com/has2k1/plotnine
* _Streamlit_: can use full stack or frontend https://testdriven.io/blog/fastapi-streamlit/#streamlit-frontend https://github.com/streamlit/streamlit
* online: https://www.datawrapper.de/ https://quickchart.io/
* web app https://streamlit.io/
* Jupyter for viz https://observablehq.com/ https://github.com/lux-org/lux https://observablehq.com/@simonw/datasette-downloads-per-day-with-observable-plot
* https://github.com/apache/superset
* data completeness https://github.com/ResidentMario/missingno
* https://github.com/chriskiehl/Gooey

CLI
* _plotnine_: ggplot clone https://github.com/has2k1/plotnine
* sparkline https://blog.jonudell.net/2021/08/05/the-tao-of-unicode-sparklines/
* _termgraph_: unit tests https://github.com/mkaz/termgraph/pull/44 histogram https://github.com/mkaz/termgraph/pull/51 use csv https://github.com/pfries/quantiles bar charts https://github.com/mkaz/termgraph Ruby alternative https://github.com/Martin-Nyaga/termplot
* _bashplotlib_: only bar graphs https://github.com/glamp/bashplotlib https://robertheaton.com/2019/04/14/open-source-for-advanced-beginners-1-bashplotlib/ 
* looks promising https://github.com/piccolomo/plotext
* _gnuplot_: https://lwn.net/Articles/826456/ https://missing.csail.mit.edu/2020/data-wrangling/
* https://github.com/mcastorina/graph-cli https://github.com/mcastorina/graph-cli/issues/24 create asset using Altair and pop in browser (like coverage)?
* https://github.com/guptarohit/asciigraph
* check this one out for tracking https://github.com/irevenko/tsukae

# OBJECTS

📜 https://docs.python.org/3/tutorial/classes.html

attributes
* _property_: you can control `__get__`/`__set__`/`__delete` (whereas you cannot on attributes) https://stackoverflow.com/q/7374748
* kinds of attr: value, type, refcount (reference count) https://realpython.com/pointers-in-python/#objects-in-python https://pythonspeed.com/articles/python-object-memory/ https://realpython.com/python-pass-by-reference/#passing-arguments-in-python https://realpython.com/python-pass-by-reference/#understanding-assignment-in-python
* read: single (dot notation) all (`dir()`, `vars()`)
* check if attr present with try/catch, don't use hasattr() https://hynek.me/articles/hasattr/

* comparison operators 🗄 `language.md` semantics
```python
# isinstance -> type
isinstance(False, bool)  # True

# `is` -> identity (same obj) 🗄 'assignment'
a = "hey"
b = a
a is b  # True
b is a  # True

# `==` -> equality (same val); SimpleNameSpace does this as well https://treyhunner.com/2019/03/python-deep-comparisons-and-code-readability/
x = [1,2,3]
y = [1,2,3]
id(x)  # 4567741704
id(y)  # 4567723016
x == y  # True
x is y  # False
```

---

* _sink_: https://www.youtube.com/playlist?list=PL-osiE80TeTsqhIuOqKhwlXsIBIdSeYtc 📙 tutorial chapter 9, Hitchhiker's Guide 3.1.7, https://zenhack.net/2016/12/25/why-python-is-not-my-favorite-language.html https://realpython.com/python3-object-oriented-programming/ https://www.youtube.com/watch?v=epKegvx_Jws https://realpython.com/python38-new-features/#more-precise-types https://robertheaton.com/2014/02/09/pythons-pass-by-object-reference-as-explained-by-philip-k-dick/ + https://www.hackerfactor.com/blog/index.php?/archives/825-8-Reasons-Python-Sucks.html https://www.youtube.com/watch?v=mUu_4k6a5-I object types https://medium.com/@meghamohan/mutable-and-immutable-side-of-python-c2145cf72747 https://apirobot.me/posts/lets-talk-about-data-structures-in-python https://kite.com/blog/python/python-dictionaries

obj
* PyObject is base obj class for CPython, impl as C struct https://realpython.com/pointers-in-python/#names-in-python
* _representation_: tldr always impl `__repr__` bc it will be used by both `str()` and `repr()`; longer answer is that if you do impl both `__repr__` is expected to be more detailed and (logging) `__str__` more readable (debugging) https://realpython.com/courses/pythonic-oop-string-conversion-__repr__-vs-__str__/ https://stackoverflow.com/a/2626364
* _temporary_: holds another name's value https://docs.python.org/2.4/lib/weakref-extension.html https://www.quora.com/What-is-temp-in-c-programming
```python
# everything is an obj (var, fun, class, modules)
isinstance(1, object)

# components: 
sys.getrefcount('abc')  # 43 (idky so many; bpython cache? vanilla Python interpreter displays different, lower number)
hey = 'abc'
sys.getrefcount('abc')  # 44
```

* _get class_: `type()` or `obj.__class__`
* _hashable_: can be compared to other objects, has hash value which never changes https://stackoverflow.com/a/14535739/6813490 are immutable https://inventwithpython.com/blog/2019/02/01/hashable-objects-must-be-immutable/
* _single underscore_: hint (not enforcement) of private method [tutorial 9.6] i.e. no access modifiers

* OOP
```python
# eh
class SomeView(BaseView):
  _foo_service = None
  @property
  def foo_service(self):
    if not self._foo_service:
      self._foo_service = factory.get_foo_service()
    return self._foo_service

# better
class SomeView(BaseView):
  @functools.cached_property
  def foo_service(self):
    return self._foo_service = factory.get_foo_service()
```

dataclass
> the most useful purpose is adding a certain degree of formalization to a group of values that need to be passed around. https://www.revsys.com/tidbits/dataclasses-and-attrs-when-and-why/
* `__repr__` and `__eq__` for free https://realpython.com/python-data-classes/
* faster access than `namedtuple` but worse mem usage https://stackoverflow.com/a/51673969
* convert dict to dataclass https://github.com/konradhalas/dacite

## garbage collection

* _garbage_: memory occupied by obj no longer in use
* _garbage collection_: scheduled memory management
* _why?_ other wise you'd run out of memory; easier than manual, but can be slower
* can turn off for performance improvements https://talkpython.fm/episodes/show/265/why-is-python-slow 42:00
* how to fit a lot of data in memory https://pythonspeed.com/articles/data-doesnt-fit-in-memory/
* _sink_: https://docs.python.org/3/faq/design.html#how-does-python-manage-memory https://docs.python.org/3/faq/design.html#why-doesn-t-cpython-use-a-more-traditional-garbage-collection-scheme https://docs.python.org/3/faq/design.html#why-isn-t-all-memory-freed-when-cpython-exits https://docs.python.org/3/faq/design.html#why-isn-t-all-memory-freed-when-cpython-exits https://pythonspeed.com/articles/function-calls-prevent-garbage-collection/

* _when?_
```python
# unbind name from obj

x = 1000  # int obj created w/ value of 1000
x = 500  # creates new int obj, re-points `x` at new obj

# delete variable, class instance

y  = [2,3,5]
del y

# local var goes out of scope

def foo(param):
    bar = [1,2,3]  # will be gc'd
    return param
```

* `__del__()`: aka finalizer; method called when `del` called against obj/var; meant for cleaning up memory, not doing other code cleanup (use `with` instead) [4:00]

## memory

🗄
* `architecture.md` memory
* `language.md` memory

basics
* _object_: underlying value
* get size `sys.getsizeof(obj)`
* _name_: way to refer to obj
* aka object reference https://nedbatchelder.com/text/names.html
* _aliasing_: multiple names bind to same obj https://docs.python.org/dev/tutorial/classes.html#a-word-about-names-and-objects
```python
def view_obj(obj):
    print(id(obj))

myo = 1
id(myo)        # 4300357872
view_obj(myo)  # 4300357872
```

---

* https://pythonspeed.com/articles/json-memory-streaming/
* https://martinheinz.dev/blog/68
* https://realpython.com/python-memory-management/
* https://pythonspeed.com/memory/
* https://www.moderndescartes.com/essays/data_oriented_python/

* _assignment_: bind name to obj https://realpython.com/copying-python-objects/ https://eloquentjavascript.net/03_functions.html
```python
###
# WALRUS
# combine assignment w/ another operatation
##

foo = 'foo val'  # w/out walrus, have to do next operation (print, whatever) in another statement
print(foo := 'foo val')  # can combine assignment w/ another statement

# makes for easier control flow https://realpython.com/python-pass-by-reference/#creating-conditional-multiple-return-functions
if (temp_var := foo_func()) is not None:
    another_func(temp_var)

###
# PACKING
# *return* n obj in single statement
###

def multiple_return():
    return 1, 2  # tuple

###
# UNPACKING
# *assign* n obj in single statement 📙 Beazley 1
###

t = multiple_return()  # tuple
for k, v in  # type depends on iterable

# can unpack iterable to single name
l_in_l = [1, [42, 13, 99]]
a, b = l_in_l
a  # 1
b  # [42, 13, 99]

# cannot unpack n el to single name
my_l = [42, 13, 99]
a, b = my_l
Traceback (most recent call last):
  File "<input>", line 1, in <module>
    a, b = my_l
ValueError: too many values to unpack (expected 2)

# used to replace hard-coded indices w/ asterisk/star operator https://mathspp.com/blog/pydonts/unpacking-with-starred-assignments https://mathspp.com/blog/pydonts/deep-unpacking
# splat operator https://stackoverflow.com/a/48451275
sys.argv[0], sys.argv[1:]
program_name, *arguments = sys.argv

# used to replace hard-coded indices
date = timestamp.split('/')
print(f'{date[2]}-{date[0]}-{date[1]}')
month, day, year = timestamp.split('/')
print(f'{year}-{month}-{day}')
```

* _reassigment_: rebind name to new obj https://realpython.com/python-pass-by-reference/#understanding-assignment-in-python
```python
# assignment evaluated right to left i.e. can swap (just another form of packing) https://docs.python.org/3/reference/expressions.html#evaluation-order
a, b = b, a
# can do for multiple https://stackoverflow.com/a/31111801
l = list('cat')
l[0:1], l[1:3] = l[1:3], l[0:1]

bl = 42
bl = 13  # new int obj created for 42 (as opposed to updating value of int obj already created for 13)
id(bl)  # 4304845696

bar = [0]
bar = [0, 1]  # diff obj

# versus performing operation on existing obj
foo = [0]
foo.append(1)  # same obj
```

* _interning_: 🗄 `language.md` https://realpython.com/pointers-in-python/#a-note-on-intern-objects-in-python -> don't understand his first example in this section
```python
# ✅ pre-created immutable obj are interned (ints 0-256)
hey = 13
hi = 13
hi is hey  # True

# ❌ non-pre-created immutable obj are not interned 
hey = 257
hi = 257
hi is hey  # False

# ✅ strings under 20 char and only containing char/int/underscores are interned
x = "hey"
y = "hey"
x is y  # True

# ❌ strings over 20 char or not containing char/int/underscores are not interned
x = "hey!"
y = "hey!"
x is y  # False

# 🎗 can force interning with sys.intern() https://docs.python.org/3/library/sys.html#sys.intern useful for speeding dict lookup bc interned obj will be compared using memory address, not value https://realpython.com/pointers-in-python/#a-note-on-intern-objects-in-python
import sys
x = sys.intern(x)
y = sys.intern(y)
x is y  # True

# ✅ mutable obj can be interned if names are transitively bound
hey = [1, 2, 3]
hi = [1, 2, 3]
hi is hey  # False
hello = hey
hello is hey  # True

# ⚠️ mutable obj updated for all bound names https://robertheaton.com/2014/02/09/pythons-pass-by-object-reference-as-explained-by-philip-k-dick/
foo = [1, 2, 3]
bar = foo
bar[0] = 42
foo  # [42, 2, 3]
```

# PACKAGING

🗄 `linux.md` packaging

stdlib
* rise of 3rd-party packages, dead batteries http://pyfound.blogspot.com/2019/05/amber-brown-batteries-included-but.html https://www.python.org/dev/peps/pep-0594/
* how to get in https://github.com/hukkin/tomli/issues/141

---

https://news.ycombinator.com/item?id=32258783
https://venthur.de/2021-06-26-python-packaging.html
https://pythonspeed.com/articles/distributing-software/

🗄 `list-of-python-pkg-terminology.md`

* _sink_: http://andrewsforge.com/article/python-new-package-landscape/ http://aosabook.org/en/packaging.html  https://chriswarrick.com/blog/2018/07/17/pipenv-promises-a-lot-delivers-very-little/#id11 https://realpython.com/pipenv-guide/ https://www.reddit.com/r/Python/comments/aox5ah/moving_away_from_pipenv/ https://medium.com/@grassfedcode/five-myths-about-pipenv-698c5f198e4b https://medium.com/@DJetelina/pipenv-review-after-using-in-production-a05e7176f3f0 https://jacobian.org/2019/nov/11/python-environment-2020/ https://packaging.python.org/glossary/ https://manikos.github.io/a-tour-on-python-packaging#pip http://aosabook.org/en/packaging.html 

* _tldr_: dep mgmt and distro are intermingled cf. `setuptools`; even with things outside either cf. `setup.cfg` https://www.b-list.org/weblog/2020/jan/05/packaging/ ❓ should all apps also be packages from a 'this makes working with other Python constructs easier?' https://hynek.me/articles/python-app-deps-2018/

* _packaging_: blanket term for distribution, dependency mgmt, and environment mgmt https://www.b-list.org/weblog/2020/jan/05/packaging used as synonym for 'distribution' https://www.youtube.com/watch?v=QX_Nhu1zhlg @ 7:10 https://talkpython.fm/episodes/show/245/python-packaging-landscape-in-2020
* _package_: dir containing modules

* `pyproject.toml` does both distro (replaces `setup.py`) and dep mgmt (`requirements.txt`, `Pipfile`, which is backend by the PyPA); tricky w/ Heroku https://jacobian.org/2019/nov/11/python-environment-2020/ https://snarky.ca/what-the-heck-is-pyproject-toml https://github.com/carlosperate/awesome-pyproject
* `distutils`: initial approach to packaging and foundation for current tools (pip); mailing list for packaging https://docs.python.org/3/installing/index.html deprecated https://towardsdatascience.com/all-the-important-features-and-changes-in-python-3-10-e3d1fe542fbf

## distribution

### executable

PyInstaller https://github.com/pyinstaller/pyinstaller https://realpython.com/pyinstaller-python/
* tldr: tars up src/interpreter, then upacks on user's computer and runs
* gets pkgs from your env
* i.e. pyinstaller needs to be installed into same env as the pkgs you want it to bundle
* i.e. can't have pyinstaller installed via pipx (which has it's own Python version) trying to bundle script that needs pkg that pipx doesn't know about
* i.e. pyinstaller is not pulling deps (either from script or lockfile) but rather finding them in your env
> PyInstaller reads a Python script written by you. It analyzes your code to discover every other module and library your script needs in order to execute. Then it collects copies of all those files - including the active Python interpreter! - and puts them with your script in a single folder, or optionally in a single executable file. https://pyinstaller.readthedocs.io/en/v4.9/operating-mode.html
* create binary: `pyinstaller -F <script.py>` https://pyinstaller.readthedocs.io/en/stable/usage.html#what-to-generate
```sh
├── dir
│   └── build  # for debugging https://realpython.com/pyinstaller-python/#build-folder
│   └── dist
│   └──── script_name  # what you give to user
```
* slow for CLIs than PyOxidizer
* supported 3rd party pkg https://github.com/pyinstaller/pyinstaller/wiki/Supported-Packages
* doesn't cross-compile https://stackoverflow.com/a/35878611/6813490
* works on M1 https://github.com/pyinstaller/pyinstaller/issues/5315
* playing nice with pyenv
```sh
$ pyinstaller main.py

OSError: Python library not found: Python, .Python, libpython3.8.dylib, libpython3.8m.dylib, Python3
* On Debian/Ubuntu, you need to install Python development packages:
* apt-get install python3-dev
* apt-get install python-dev
* If you are building Python by yourself, rebuild with `--enable-shared` (or, `--enable-framework` on macOS).

# https://stackoverflow.com/a/70795604 https://github.com/pyenv/pyenv/wiki#how-to-build-cpython-with-framework-support-on-os-x
$ env PYTHON_CONFIGURE_OPTS="--enable-framework" pyenv install 3.5.0
```

PyOxidizer
* can now install Python as single executable as use that to run script!?! https://twitter.com/indygreg/status/1524041572173508608 https://gregoryszorc.com/blog/2022/05/10/announcing-the-pyoxy-python-runner/
* https://github.com/indygreg/PyOxidizer https://gregoryszorc.com/blog/2018/12/18/distributing-standalone-python-applications
* 🚧 blocker w/ importing 3rd party packages https://github.com/indygreg/PyOxidizer/issues/69 https://tryexceptpass.org/article/package-python-as-executable/
* faster than PyInstaller for CLI https://pyoxidizer.readthedocs.io/en/latest/comparisons.html#pyinstaller https://pythonbytes.fm/episodes/show/138/will-pyoxidizer-weld-shut-one-of-python-s-major-gaps
* WIP https://news.ycombinator.com/item?id=23339970
* can produce binaries for all operating systems https://pythonbytes.fm/episodes/show/138/will-pyoxidizer-weld-shut-one-of-python-s-major-gaps
* https://www.pythonpodcast.com/pyoxidizer-python-package-creation-episode-282/

alternatives
* https://github.com/cole-wilson/sailboat
* Beeware https://github.com/beeware/ https://www.youtube.com/watch?v=WjMDXDHBn1I
* _auto-py-to-exe_: https://pythonbytes.fm/episodes/show/160/your-json-shall-be-streamed
* _Bazel_: https://news.ycombinator.com/item?id=23338316 https://github.com/google/subpar
* _bbfreeze_: https://stackoverflow.com/a/29515965/6813490
* _Cython_: compiles to C extension and runs that https://tryexceptpass.org/article/package-python-as-executable/ http://shvbsle.in/computers-are-fast-but-you-dont-know-it-p1/
* _Nuitka_: https://tryexceptpass.org/article/package-python-as-executable/ https://gregoryszorc.com/blog/2018/12/18/distributing-standalone-python-applications/ https://snarky.ca/what-is-the-core-of-the-python-programming-language
* _PEX_: https://gregoryszorc.com/blog/2018/12/18/distributing-standalone-python-applications/
* _py2exe_: https://stackoverflow.com/a/5458807/6813490
* _Shiv_: https://pythonbytes.fm/episodes/show/114/what-should-be-in-the-python-standard-library https://jhermann.github.io/blog/python/deployment/2020/03/08/ship_libs_with_shiv.html https://gregoryszorc.com/blog/2018/12/18/distributing-standalone-python-applications/
* _XAR_: https://gregoryszorc.com/blog/2018/12/18/distributing-standalone-python-applications/

### library

📜 https://docs.python.org/3/distributing/index.html
🧀
* https://pypi.org/manage/account/
* https://test.pypi.org/

get namespace for dataclerk
* PSF https://packaging.python.org/en/latest/tutorials/packaging-projects/
* Real Python https://realpython.com/pypi-publish-python-package/
* Poetry
* Twine https://github.com/pypa/twine
> do people use? https://talkpython.fm/episodes/transcript/208/packaging-making-the-most-of-pycon-and-more
> tool to replace `stup.py` upload https://talkpython.fm/episodes/transcript/64/inside-the-python-package-index

---

* editable installs `pip install -e` https://pgjones.dev/blog/packaging-without-setup-py-2020 https://talkpython.fm/episodes/transcript/208/packaging-making-the-most-of-pycon-and-more 🔍 Twine
* _distribution_: archived package (lib) or binary (executable) https://www.youtube.com/watch?v=QX_Nhu1zhlg @ 6:00 distribution != release https://pydist.com/blog/distributions-vs-releases
* internal https://twitter.com/brianokken/status/1402631045107707908
* _how to_: create archive and put on PyPI https://pgjones.dev/blog/packaging-without-setup-py-2020 https://packaging.python.org/guides/tool-recommendations/#packaging-tool-recommendations don't delete a build from PyPI https://pydist.com/blog/never-delete-a-release https://dustingram.com/articles/2019/04/02/pypi-as-a-service/ https://snarky.ca/how-do-you-verify-pypi-can-be-trusted/ https://www.youtube.com/watch?v=QX_Nhu1zhlg @ 14:30 https://www.youtube.com/watch?v=P3dY3uDmnkU https://www.python.org/dev/peps/pep-0518/ PyPI doesn't have good search mechanism https://github.com/pipxproject/pipx/issues/249#issuecomment-636019556 https://jwodder.github.io/kbits/posts/pypkg-mistakes/ https://news.ycombinator.com/item?id=26733423 fix bad release https://snarky.ca/what-to-do-when-you-botch-a-release-on-pypi/
* internal PyPI https://www.pythonpodcast.com/pulp-with-bihan-zhang-and-austin-macdonald-episode-168/
* example https://github.com/tfeldmann/simplematch
* _deprecation_: https://www.dampfkraft.com/code/how-to-deprecate-a-pypi-package.html https://blog.ovalerio.net/archives/1971 https://sirupsen.com/shitlists/
* _PyPI_: security https://github.com/gitpython-developers/GitPython
* warnings, PYTHONWARNINGS https://www.reddit.com/r/learnpython/comments/a14ow5/psa_when_developing_set_pythonwarnings/ https://docs.python.org/3/using/cmdline.html#cmdoption-w https://www.youtube.com/watch?v=X0AjcpicNOM&list=PL2Uw4_HvXqvYk1Y5P8kryoyd83L_0Uk5K&index=35

* rm support for previous Python version https://adamj.eu/tech/2022/01/11/removing-python-3.6-support-from-my-packages
* _library_: archived package for others to consume as dependency https://docs.python-guide.org/shipping/packaging/ https://pythonwheels.com/
* _history_: https://stackoverflow.com/a/14753678/6813490 https://www.youtube.com/watch?v=QX_Nhu1zhlg @ 7:40
* _project structure_: `src`: https://blog.ganssle.io/articles/2019/08/test-as-installed.html https://pythonbytes.fm/episodes/show/159/brian-s-pr-is-merged-the-src-will-flow https://github.com/taktluyver/flit/pull/260/commits https://bskinn.github.io/My-How-Why-Pyproject-Src/ https://github.com/takluyver/flit/pull/260 https://bskinn.github.io/My-How-Why-Pyproject-Src/ repetitive paths https://github.com/zachvalenta/site-content/commit/7e6b5f66ffd9f6b3b13b19669050289b26d8925b

past
* `setuptools`: uses `setup.py` to create distribution https://manikos.github.io/a-tour-on-python-packaging#mod_setuptools https://testandcode.com/52 @ 29:00 commonly thought of as distro tool but CLI (`easy_install`) was used for dep mtmt before `pip` https://dubroy.com/blog/so-you-want-to-install-a-python-package/
* `setup.py`: specify what parts of library to expose to consumers for `distutils` https://www.pythoncheatsheet.org/#setup.py https://www.b-list.org/weblog/2020/feb/03/how-im-testing-2020/
* `setup.cfg`: hairer version of `setup.py` https://docs.python.org/3/distutils/configfile.html also used for app config https://github.com/pallets/flask/blob/master/setup.cfg

present
* _PEP 517_: API for build tools https://testandcode.com/52 @ 15:00
* _PEP 518_: https://testandcode.com/52 @ 14:00
* `pyproject.toml`: spec for using something other than `setup.py`; used by Poetry, Flit
* _publish_: Flit, Poetry, Twine https://www.youtube.com/watch?v=QX_Nhu1zhlg @ 16:00

formats
* _Wheel_: `.whl`; current fmt, built by pip https://testandcode.com/52 @ 16:00 https://www.youtube.com/watch?v=02aAZ8u3wEQ https://realpython.com/python-wheels/ https://pythonwheels.com/
* _sdist_: `tar.gz`; ❓ does PyPI need this along with `.whl` and why? https://poetry.eustace.io
* _egg_: `.egg` https://packaging.python.org/discussions/wheel-vs-egg/ https://pythonwheels.com/

## dependencies

🗄 `language.md` packaging
📜 https://docs.python.org/3/installing/index.html
📊 https://pepy.tech/

* pinning w/ pip-tools https://lincolnloop.com/blog/python-dependency-locking-pip-tools
* pip-compile, pdm https://www.reddit.com/r/Python/comments/rjwr2d/moving_from_pipenv_to_poetry_or_pdm/
* local PyPI https://testdriven.io/blog/private-pypi/
```sh
# https://github.com/pywharf/pywharf https://stefan.sofa-rockers.org/2019/04/18/python-packaging-gitlab-conda/ https://pythonbytes.fm/episodes/show/24/i-have-a-local-pypi-server-and-so-do-you https://pydist.com https://github.com/devpi/devpi
# create index
mkdir pypi-local

# populate index w/ pkg
pip3 download -r /Users/zach/Desktop/zvmac/materials/sw/lang/python/create-python-app/requirements.txt

# use index for new project
pip3 install --no-index --find-links=~/Desktop/pypi-local coverage
```

pain points
* _transitive - resolution_: i.e. "is there (will there be if I bump this pkg) a transitive dep conflict?" https://docs.python-guide.org/starting/install3/osx/#pipenv-virtual-environments 
* _transitive - rm_: no porcelain to remove deps of deps https://github.com/invl/pip-autoremove ❓ does Poetry `remove` handle this?
* _split dev and prod_: https://github.com/algolia/algoliasearch-client-python/commit/33ff7a9ad39e5a0459795f171cf3424c815a7304  🗄 'Poetry'
* _figure out missing_: https://blog.piwheels.org/how-to-work-out-the-missing-dependencies-for-a-python-package/
* _uninstall unfrozen_: currently solving w/ Makefile `freeze` https://stackoverflow.com/q/13176968/6813490
* _no n versions of same pkg_: Ruby can do this https://pythonbytes.fm/episodes/show/127/that-python-code-is-on-fire @ 13:30

### global (pipx)

🗄 `python-3.10-youtube-ffmpeg.md`

* _global dependency_: something you'd use as a CLI (pipenv, AWS) https://jacobian.org/2018/feb/21/python-environment-2018/
* can always just use pip for user or even global install

pipx
* install: pip, Homebrew https://github.com/pipxproject/pipx/issues/59 

---

* system Python no longer exposed https://news.ycombinator.com/item?id=29238700
* _geographically constrained_: repo you need to navigate to for using CLI
* _trickery_: `bin` symlinks to + script w/ shebang line scoped to local venv https://stackoverflow.com/a/30541898/6813490 https://pythonbytes.fm/episodes/show/123/time-to-right-the-py-wrongs

pipx
* freeze https://github.com/pipxproject/pipx/issues/109
* inject https://github.com/pipxproject/pipx/pull/660 https://pipxproject.github.io/pipx/examples/#pipx-inject-example
* wanted to switch Python-based Homebrew packages (asciinema, httpie, litecli, pgcli, ranger, youtube-dl) but ran into issue w/ youtube-dl, ddgr https://github.com/pipxproject/pipx/issues/232 https://github.com/jarun/ddgr/issues/66 https://stackoverflow.com/a/42098127/6813490 googler worked with Homebrew
* when Python version upgrades it might lose track of the envs and you'll have to reinstall everything https://pythonbytes.fm/episodes/show/127/that-python-code-is-on-fire @ 14:00
* list pkgs like brew `leaves` https://github.com/pipxproject/pipx/issues/390

### operations

also, Poetry is faster (downloads, no need to freeze)

|                 operation                   |      Makefile                          |     Poetry              |
| ------------------------------------------- | ---------------------------------------| ----------------------- |
|  create env                                 |  `python3 -m venv venv`                | `init`                  |  

* create env - new project: `venv` --- `poetry init -n`
* create env - existing project: `venv` + `pip install -r requirements.txt` --- `poetry install`
* create env - existing project - prod: ❌ --- `poetry install --no-dev`
* rm venv: `rm venv` ---  `env remove 3.7` 

* tree view: `make deps` --- `poetry show --tree`

* add dep - prod: `pip install <foo>` + `make freeze` --- `poetry add <pkg>`
* add dep - dev: ❌ --- `poetry add --dev <dep>`
* rm dep - prod: `pip uninstall <pkg>` + `make purge` --- `poetry remove <pkg>`
* rm dep - dev: ❌ --- `remove -D`

* add unsaved dep: `pip install <pkg>` --- ❌
* rm unsaved dep: `make purge` --- ❌

* view env: `ls` --- `poetry env info`
* list dep tree: `pipdeptree` --- poetry show --tree`

### project (Poetry)

📜 https://python-poetry.org/docs/

| operation | dev        | prod          |
| --------- | ---------- | ------------- |
|  init     | init -n    |               |
|  install  | install    |               |
|  add      | add -D     | add           |
|  list     | show       | show --no-dev |
|  dep dir  | env info   |               |
|  rm       | remove -D  | remove        |
| --------- | ---------- | ------------- |

config
* list `config --list`
* file location `~/Library/Application Support/pypoetry` https://python-poetry.org/docs/configuration/#configuration
* set `config virtualenvs.in-project true`

venv
* store venv in project as `.venv`: `config virtualenvs.in-project true` https://python-poetry.org/docs/configuration/#virtualenvsin-project
* file location if not in project: `~/Library/Caches/pypoetry/virtualenvs/`

za
* debug: `<cmd> -vvv`
* gotcha: project directory can't have same name as a dependency used by project https://github.com/python-poetry/poetry/issues/3438
* VS Code support https://github.com/microsoft/vscode-python/wiki/Support-poetry-virtual-environments
* can't show just top-level deps https://github.com/python-poetry/poetry/issues/1990
* `SolverProblemError` = conflict btw Python version in `[tool.poetry.dependencies]` and Python version required by dependency
```python
# run script using env
poetry run python script.py
# use dep as CLI
poetry run flask
```

---

* _alternatives_: pipenv https://github.com/pypa/pipenv/commit/9ba23242 https://hynek.me/articles/python-app-deps-2018/ https://jacobian.org/2019/nov/11/python-environment-2020/ piptools https://www.pythonpodcast.com/devops-in-python-episode-244/
* _environment_: can put in project https://github.com/python-poetry/poetry/issues/1884
* _dependency resolution_: looks at `[tool.poetry.dependencies]` (which is just Python version) and finds dep version that works; presume for every pkg after the first has to do some voodoo to avoid transitive dep conflict
* _design_: distribution (`new <proj>` creates dir structure `init` asks for package name) inspired by Rust's Cargo https://www.youtube.com/watch?v=QX_Nhu1zhlg @ 12:10
* `poetry.lock`: commit to version control https://poetry.eustace.io/docs/basic-usage/#commit-your-poetrylock-file-to-version-control merge conflics https://jokeyrhyme.github.io/2017/08/22/git-conflicts-and-lock-files.html https://www.peterbe.com/plog/how-to-resolve-a-git-conflict-in-poetry.lock
* `<proj>.egg-info`: doesn't need to be under version control https://stackoverflow.com/a/19377063/6813490
* w/ Django https://rasulkireev.com/managing-django-with-poetry

Poetry versions
* _installation_: docs say to use `curl` but `pipx` worked just fine for me https://jacobian.org/2019/nov/11/python-environment-2020/
* _update_: basic `self update` to beta `self update --preview`
* 1.0 backward compatible w/ 0.12 but not vice versa i.e. if you touch lock file w/ 1.0 then 0.12 won't be able to work with it

pkg versions
* update: `update <pkg>` https://python-poetry.org/docs/basic-usage/#updating-dependencies-to-their-latest-versions
```ini
[tool.poetry.dependencies]
python = "^3.6"
django = "^3.0.9"
# I updated to Django 3.1, poetry.lock changed but not pyproject.toml
# meaning pyproj will show minimum version but not necessarily actual version
```

format
* _import_: to go from `requirements.txt` is mostly manual https://jacobian.org/2019/nov/11/python-environment-2020/
* _export_: `export -f requirements.txt > req.txt` https://pythonspeed.com/articles/pipenv-docker/ only dev https://github.com/python-poetry/poetry/issues/1441 ignore https://github.com/python-poetry/poetry/issues/2010

---

* create env - new project: `init - n` creates `pyproject.toml`; deps dir (macOS: `~/Library/Caches/pypoetry` RHEL: `~/.cache/pypoetry/virtualenvs`) and lockfile (`poetry.lock`) not created until you actually install something
* create env - existing project: `install` creates deps dir and installs deps using `poetry.lock` (if present) or `pyproject.toml` (if `poetry.lock` not present) https://poetry.eustace.io/docs/basic-usage/#installing-dependencies ❓ not being able to pick virtualenv name a problem https://hynek.me/articles/python-app-deps-2018/
* create env - existing project - prod: `install --no-dev` https://jacobian.org/2019/nov/11/python-environment-2020/
* rm env: `env remove 3.7`
> logic behind specifying version is that your project could support n versions, don't want to blanket rm all
> if no env associated w/ project dir output of `env info` will have `path` as `NA`

* activate env: `shell`

## pip

📜 https://pip.pypa.io/en/stable/

cmd
* install - user: `install PKG --user` 🗄 `python-3.10-youtube-ffmpeg.md`
* list - global: `list`
* list - user: `list --user`
* lockfile - global: `freeze > FILE`
* lockfile - user: `freeze --user > FILE`
* require venv: `PIP_REQUIRE_VIRTUALENV=true` https://docs.python-guide.org/dev/pip-virtualenv/#requiring-an-active-virtual-environment-for-pip
* install from lockfile: `pip install -r requirements.txt`; run from inside activated virtualenv
* install specific version: `pkg==version`
* uninstall from requirements: `pip uninstall -r requirements.txt -y` https://stackoverflow.com/a/53032141
* view dependency tree https://github.com/naiquevin/pipdeptree

venv 📙 Van Rossum ch. 12
* create: `python -m venv venv`; tied to fs location https://stackoverflow.com/q/32407365
* `python3 -m venv venv; on; pip install -q --upgrade pip setuptools wheel; pip list` 🗄 `.bash_profile`
* activate: `source venv/bin/activate`; sets env var (`$VIRTUAL_ENV`) on activation
> When a virtual environment is active, the `VIRTUAL_ENV` environment variable is set to the path of the virtual environment. https://docs.python.org/3/library/venv.html#creating-virtual-environments

---

* can install a C compiler with pip https://news.ycombinator.com/item?id=31776873

venv https://stackoverflow.com/a/49967371/6813490
* _venv_: use `bin` to make https://stackoverflow.com/questions/45293436/how-to-specify-python-version-used-to-create-virtual-2
* _virtual environment_: Python installation + pkgs [tutorial 12.1, Grinberg 4]
* _Docker_: shouldn't just use whole container as env https://hynek.me/articles/python-app-deps-2018/
* _history_: `venv` and `virtualenv` are not the same  ️https://docs.python.org/3/installing/index.html https://chriswarrick.com/blog/2017/07/03/setting-up-a-python-development-environment/#tools-and-management
* _PEP 582_: https://medium.com/@grassfedcode/goodbye-virtual-environments-b9f8115bc2b6 https://pythonbytes.fm/episodes/show/117/is-this-the-end-of-python-virtual-environments
* _location_: per project or all in `~`
* _sink_: using a Makefile https://github.com/sio/Makefile.venv https://realpython.com/python-virtual-environments-a-primer/

* latest versions don't try to compile, will just get binary https://pythonspeed.com/articles/upgrade-pip

* checking for updates https://stackabuse.com/python-update-all-packages-with-pip-review/
* _upgrade_: `pip install --upgrade pip`
* _bundling_: comes w/ versions >= 2.7.9; don't install using os-managed Python https://pip.pypa.io/en/stable/installing/
* _view dependency tree_: https://github.com/naiquevin/pipdeptree https://github.com/zachvalenta/create-python-app/network/dependencies
* _virtual environment_: not installing into system or user-wise `site-packages` https://www.b-list.org/weblog/2020/jan/05/packaging/
* bash profile `venv` hack 🗄 `pip-venv-hack`
* _freeze_: `pip freeze > requirements.txt`
* _install from frozen_: `pip install -r requirements.txt`

---

* _fuzzy installs_: case insensitive (`flask-sqlalchemy` treated same as `Flask-SQLAlchemy` https://github.com/pallets/flask-sqlalchemy/) converts underscores to hyphen (`flask_whooshalchemy` same as `flask-whooshalchemy` https://github.com/gyllstromk/Flask-WhooshAlchemy https://www.youtube.com/watch?v=bAPcmGNsulc @ 0:55)
```diff
- /U/a/D/vue-firebase-master $ poetry add flask_whooshalchemy

Using version ^0.56 for flask_whooshalchemy
  - Installing blinker (1.4)
  - Installing whoosh (2.7.4)
  - Installing flask-whooshalchemy (0.56)

+ /U/a/D/vue-firebase-master $ poetry add flask-whooshalchemy

Using version ^0.56 for flask-whooshalchemy
  - Installing blinker (1.4)
  - Installing whoosh (2.7.4)
  - Installing flask-whooshalchemy (0.56)
```

---

* dependency resolver = hashed output like Poetry and pipenv? https://github.com/pypa/pip/issues/988
* `list` results matching PyPI https://github.com/pypa/pip/issues/7260
* _different versions_: can install different versions of dep e.g. `pip install flask-dance[sqla]` https://www.youtube.com/watch?v=MiHVTHzIgyE @ 1:15
* _bundled_: not part of stdlib but comes w/ Python install (since 3.4) via installer file (which means can update independently of Python version)
* `-editable`: meaning you can edit the source code of the pkg i.e. if you're developing a library and want to test out how it works without having to reinstall every time you update https://stackoverflow.com/a/35064498/6813490
* _invocation_: use `python -m pip` to ensure that you're using the version of `pip` bundled w/ the Python install https://stackoverflow.com/a/25749976/6813490
* _cache_: will check local before going to network https://pip.pypa.io/en/stable/reference/pip_install/#caching
* editable mode https://github.com/pallets/flask/blob/master/CONTRIBUTING.rst
* _conf_: `~/.config/pip/pip.conf` https://pip.pypa.io/en/stable/user_guide/#config-file
```conf
[global]
index-url = http://download.zope.org/ppix # CLI arg is `-i`
```
* _sink_: https://pydist.com/blog/pip-install 

# REPL

📙 Van Rossum ch. 2, 14
🗄
* `sql.md` munge
* `theory.md` notation

| REPL          | pkg    | features                           |
| --------------|--------|------------------------------------|
| python        | stdlib | readline, history substitution     |
| iPython       | PyPI   | color, ipdb, magic func            |
| bpython       | PyPI   |                                    |
| ptpython      | PyPI   |                                    |

exploratory programming
* _REPL_: interface to interpreter + prompt https://docs.python.org/3/tutorial/interpreter.html#interactive-mode
* aka OODA loop https://scholars-stage.org/the-ooda-loop-ancient-china-style/ https://en.wikipedia.org/wiki/John_Boyd_%28military_strategist%29#OODA_loop https://dominiccummings.substack.com/p/regime-change-2-a-plea-to-silicon https://dominiccummings.substack.com/p/how-could-labour-win-swap-dud-dead
* _debugger_: REPL + program state e.g. pdb
* _db CLI_: REPL + db state e.g. visidata
* _notebook_: IDE + data e.g. Jupypter
* _spreadsheet_: proprietary notebook https://www.youtube.com/watch?v=llgTl9BDuKw

human-computer interaction
* human-computer interaction http://worrydream.com/MagicInk/
* visualizing music https://www.youtube.com/watch?v=23vumiogTQk
* the tree https://www.amazon.com/dp/1616892188
* aka interaction design https://ncase.me/loopy/
* music education https://dennisdesantis.com/
* sankey diagram https://github.com/ricklupton/floweaver
* http://www.designishistory.com/1940/will-burtin/
* http://www.designishistory.com/1940/ladislav-sutnar/
* mind bicyle https://github.com/pel-daniel/mind-bicycles
* Nicky Case
* https://news.ycombinator.com/item?id=23702552
* Tufte https://postlight.com/podcast/computing-is-everywhere https://en.wikipedia.org/wiki/Edward_Tufte https://blog.codinghorror.com/recommended-reading-for-developers/ 
* _Tufte handout_: have taste, use graphics https://bookdown.org/yihui/rmarkdown/tufte-handouts.html

---

* Light Table: watch (continuous println on an expression) https://youtu.be/52SVAMM3V78 1:15 https://tonsky.me/blog/interactive-development/ https://news.ycombinator.com/item?id=3836978
* https://github.com/pel-daniel/mind-bicycles
* Bret Victor, visual programming https://news.ycombinator.com/item?id=26371818 Dynamicland isn't going anywhere https://news.ycombinator.com/item?id=26725370
* https://news.ycombinator.com/item?id=26612894

## command line

📜
* https://docs.python.org/3/tutorial/interpreter.html
* https://docs.python.org/3/tutorial/interactive.html
* https://docs.python.org/3/tutorial/appendix.html#interactive-mode
> When commands are read from a tty, the interpreter is said to be in interactive mode. https://docs.python.org/3/tutorial/interpreter.html#interactive-mode

bpython 
* undo `CTRL r`
* autocomplete `CTRL f/e`

---

* https://news.ycombinator.com/item?id=29947891 https://news.ycombinator.com/item?id=29947891
> the point here is to have context and reload when you're working rapidly (script, interviewing)
> importlib? non-breakpoint pdb modes?
* preload: pipx inject
> is there a way we could namespace these i.e. one for networking, for CLI dev? https://pipxproject.github.io/pipx/examples/#pipx-inject-example
* reload src: point is to avoid continual exit/rerun https://news.ycombinator.com/item?id=23793054 https://mikelevins.github.io/posts/2020-12-18-repl-driven/

init
* point to init script w/ interface (`bpython -i <script>`) https://stackoverflow.com/a/14244342 https://stackoverflow.com/a/56844640 🗄 `algos`
* set `PYTHONSTARTUP` (`export PYTHONSTARTUP='./repl.py' && poetry run bpython`) https://docs.python.org/3/using/cmdline.html#envvar-PYTHONSTARTUP
* helpers for `locals()` on pythonpath https://stackoverflow.com/a/21961813/6813490
* sink https://arpitbhayani.me/blogs/python-prompts https://github.com/bpython/bpython/blob/ae4a502a443e024bd82ed1a7b88adf8be2068a2c/doc/sphinx/source/django.rst https://github.com/bpython/bpython/search?q=PYTHONSTARTUP&unscoped_q=PYTHONSTARTUP https://stackoverflow.com/a/14244310 https://stackoverflow.com/a/34774703 https://stackoverflow.com/a/4289945 https://docs.bpython-interpreter.org/en/latest/django.html https://docs.djangoproject.com/en/3.0/ref/django-admin/#shell check out this lib https://github.com/sloria/konch/blob/master/konch.py
* reload: `from importlib import reload; reload (mod)` https://realpython.com/run-python-scripts/#using-importlib-and-imp normal reimport doesn't work https://realpython.com/run-python-scripts/#taking-advantage-of-import lib https://github.com/hoh/reloadr https://github.com/breuleux/jurigged
* history: save https://stackoverflow.com/a/33880964 readline error manifests in garbled cmd history (have only seen when setting breakpoint in Flask) https://stackoverflow.com/a/3486617

## iPython

🗄 pdb
📜 https://ipython.readthedocs.io/en/stable/index.html
🔗 https://jakevdp.github.io/PythonDataScienceHandbook/01.00-ipython-beyond-normal-python.html

* command
```python
# run iPython and debug at site of error https://lukeplant.me.uk/blog/posts/repl-python-programming-and-debugging-with-ipython/ https://stackoverflow.com/a/21508070
from IPython import embed; embed()
# use already running iPython to debug at site of error
%debug
# pretty print obj
pp
# paste from system clipboard
%paste
```

* _line magic_: `%` operates on single line
* list https://ipython.readthedocs.io/en/stable/interactive/magics.html#magic-lsmagic
* _cell magic_: `%%` operates on n lines
* _automagic_: don't need prefex for line magic
* relationship to shell https://jakevdp.github.io/PythonDataScienceHandbook/01.05-ipython-and-shell-commands.html
* tab to view obj attr https://stackoverflow.com/q/41812447

cmd to check out https://jakevdp.github.io/PythonDataScienceHandbook/01.03-magic-commands.html
* edit https://ipython.readthedocs.io/en/stable/interactive/magics.html#magic-edit
* macro https://ipython.readthedocs.io/en/stable/interactive/magics.html#magic-macro
* debug https://ipython.readthedocs.io/en/stable/interactive/magics.html#magic-debug
* doc string https://ipython.readthedocs.io/en/stable/interactive/magics.html#magic-pdoc
* profile https://ipython.readthedocs.io/en/stable/interactive/magics.html#magic-prun time https://ipython.readthedocs.io/en/stable/interactive/magics.html#magic-time
* run file https://ipython.readthedocs.io/en/stable/interactive/magics.html#magic-run

## Jupyter

📜 https://jupyter.readthedocs.io/en/latest/index.html

history
* _iPython_: REPL + syntax highlighting, access to Bash cmd
* _IPython Notebook_: IPython + persistence, web browser, visualizations (chart, Markdown)
* _Jupyter_: IPython Notebook + kernels for other languages (R, F#, Java)
* _Jupyter Lab_: pretty UI, less features https://stackoverflow.com/a/52392304
* https://github.com/jtpio/jupyterlite

install
* Conda recommended https://jupyter.readthedocs.io/en/latest/install.html#id3
* pip works fine https://jupyter.readthedocs.io/en/latest/install.html#alternative-for-experienced-python-users-installing-jupyter-with-pip
* poetry worked as well http://jupyterlab.io/install.html

za
* `.ipynb_checkpoints`: most recent state of `<file>.ipynb` https://stackoverflow.com/a/46422176/6813490 ignore in version control https://stackoverflow.com/a/39997938/6813490
* _kernel_: interpreter
* notebooks as articles https://news.ycombinator.com/item?id=27367948
* reproducibility https://jvns.ca/blog/2017/11/12/binder--an-awesome-tool-for-hosting-jupyter-notebooks/ https://news.ycombinator.com/item?id=24943962
* to Markdown https://github.com/mwouts/jupytext
* alternatives https://github.com/twosigma/beakerx https://zeppelin.apache.org/ https://www.datacamp.com/community/blog/jupyter-notebook-r https://github.com/ottomatica/docable-notebooks https://datacrayon.com/shop/product/data-analysis-with-rust-notebooks/
* design https://news.ycombinator.com/item?id=25538454 https://www.fast.ai/2019/12/02/nbdev/ http://willcrichton.net/notes/programming-in-the-debugger https://ljvmiranda921.github.io/notebook/2020/03/06/jupyter-notebooks-in-2020/ Somers https://www.theatlantic.com/science/archive/2018/04/the-scientific-paper-is-obsolete/556676/

## pdb

🗄 iPython
📙 Beazley ch. 14
📜
* `help pdb`
* https://docs.python.org/3/library/pdb.html
* https://docs.python.org/3/library/debug.html

context
* `a`: func args
* `p <obj>`: print obj https://docs.python.org/3/library/pdb.html#pdbcommand-p 🗄 `.pdbrc`
* `i <obj>`: print obj attr 🗄 `.pdbrc`
* `loc`: print obj in scope 🗄 `.pdbrc`
* `pp <expresion>`: same but pprint
* `__return__`: view return val from function https://stackoverflow.com/a/18674516
* `whatis`: = `type()`
* `interact`: start REPL w/ local var in context
> how to exit REPL w/ out exit pdb? -> `!` run new code

control flow
* _step in_: `s` = enter func at current line
* _step over_: `n` = execute func at current line or exit current func
* _step out_: `r` = exec to end of current func
* `c`: continue exec to completion (or next breakpoint)
* `until <LOC>`: exit loop and jump to LOC https://docs.python.org/3/library/pdb.html?highlight=until#pdbcommand-until https://stackoverflow.com/a/61151333
* next iteration in loop: breakpoint inside loop + `c` https://stackoverflow.com/a/28414891

paging
* _list point (lp)_: LOC to list around
* != current LOC, != breakpoint
* ❓ lp follows current LOC as determined by control flow cmd?
* `l`: list n LOC from lp and then mv lp (hence `l .` to reset)
* `l .`: reset lp to current LOC https://stackoverflow.com/a/23064293
* doens't work on 2.7
* `ll`: list page at list point
* `w`: location in call stack
```python
# list src after navigation cmd
# = pdbpp 'sticky mode' https://github.com/pdbpp/pdbpp#sticky-mode
alias n n;;l
alias r r;;l
```

exec
```sh
# RUN FROM REPL
import pdb
import ur_script
script.div(6, 0)            # throws err
pdb.pm()                    # post-mortem mode

# RUN FROM SHELL
python3 -m pdb mymodule.py  # automatically restarts https://www.youtube.com/watch?v=P0pIW5tJrRM 2:50
python -i script.py         # interactive; `python --help` -> "inspect interactively after running script"
```

---

todo
* `h`
* `r`
* `u / d`
* `interact`

config
* `.pdbrc`: `$HOME` is default file location https://docs.python.org/3/library/pdb.html?highlight=pdbrc#debugger-commands
* aliases https://docs.python.org/3.2/library/pdb.html#pdbcommand-alias
* comments https://nedbatchelder.com/blog/200704/my_pdbrc.html https://www.youtube.com/watch?v=_kCKBXtA2jQ
* command history buggy w/ readline incompatability https://stackoverflow.com/questions/6348034/python-pdb-command-history-not-working-on-windows

internals https://www.youtube.com/watch?v=QU158nGABxI
* `settrace` registers callback on interpreter for function call, LOC executed, func return value, exceptions raised [3:45]
```python
def simple_tracer(frame, event):  # 4:30
```
* trickier with multithreading [10:00]
* BYO w/ bdb [11:45]

pdb++ https://github.com/pdbpp/pdbpp
* main reason to use seem to be syntax highlighting and tab completion https://github.com/pdbpp/pdbpp#what-is-it
* pytest workaround https://github.com/pdbpp/pdbpp/issues/392 https://github.com/zachvalenta/algos/blob/master/Makefile#L43
* overrides pdb breakpoint https://github.com/pdbpp/pdbpp/issues/281
* `track`: (requires pypy)
* `display`: (couldn't figure out how this worked first time around)

alternatives
* _pudb_: https://github.com/inducer/pudb https://realpython.com/python-packages/#pudb-for-visual-debugging
* _ipdb_: https://stackoverflow.com/a/15976544/6813490 https://adamj.eu/tech/2021/02/21/improve-your-django-experience-with-ipython/
* _bdb_: level down from pdb https://stackoverflow.com/a/10302538/6813490
* _gdb_: deep bad things https://wiki.python.org/moin/DebuggingWithGdb
* `print()`: if you don't know how to use a debugger https://twitter.com/raymondh/status/1266668437020897280 https://github.com/gruns/icecream https://github.com/cool-RR/PySnooper
> It takes less time to decide where to put print statements than to single-step to the critical section of code https://news.ycombinator.com/item?id=26928696

# ZA

naming
* _classes_: camel case
* _modules_: start w/ letter or underscore
* _pkg_: all seem to use hyphens instead of underscores https://stackoverflow.com/a/36611371
* case is significant https://www.python.org/dev/peps/pep-0008/#descriptive-naming-styles

underscores https://dbader.org/blog/meaning-of-underscores-in-python
* _single_: placeholder for throwaway values from unpacking
* in REPL, refers to result of last operation
* _single leading_: won't be imported in `from <mod> import *` https://stackoverflow.com/a/8689983
* _single trailing_: break naming conflict
* _double leading_: naming mangling i.e. measure to prevent accidental overrides
* _doubled_: dunder methods

misc
* open browser `python -m webbrowser -n "https://www.python.org"` https://medium.com/@martin.heinz/python-cli-tricks-that-dont-require-any-code-whatsoever-e7bdb9409aeb
* using other language in Python e.g. Julia https://www.peterbaumgartner.com/blog/incorporating-julia-into-python-programs/
* 2to3 https://news.ycombinator.com/item?id=24461157
* _callable_: any obj that impl `__call__` e.g function, method, classes e.g. `MyClass()` https://eli.thegreenplace.net/2012/03/23/python-internals-how-callables-work
* _community_: Ken Reitz (requests) Donald Stuft (PyPA) Raymond Hettinger (core) Ned Batchelder (coverage), Tim Peters (Zen of Python `import this`, Timsort) Al Sweigart (author) Trey Hunner (blogger) Armin Ronacher (Flask) Brett Cannon (core) Nick Coghlan (core) Eli Bendersky (Google, buddies w/ Coghlan)
* _destructuors_: https://eli.thegreenplace.net/2009/06/12/safely-using-destructors-in-python
* `eval()`: take string and evaluate as if expression from language
* _line continuation_: "join consecutive lines if the last character of the line is a backslash" [HG 3.2.5 pg. 56] can use parens https://stackoverflow.com/a/53180/6813490
* `print()`: implicitly adds `\n` under the hood; workaround is `print('hello zv', end="")`
* `__pycache__`: holds bytecode in the form of `.pyc` https://stackoverflow.com/a/28365204/6813490 speeds up module loading https://docs.python.org/3/tutorial/modules.html#compiled-python-files suppress creation of with `export PYTHONDONTWRITEBYTECODE=1` more on bytecode https://blog.jse.li/posts/pyc/
* _Python2_: can't test Python2 code using Python3 if you're using parts of stdlib that have been deprecated between releases (urllib2, xrange); Tauthon to backport Python3 features https://www.pythonpodcast.com/tauthon-python-2-fork-episode-265/
* _style_: style guides https://www.python.org/dev/peps/pep-0008/ https://github.com/google/styleguide/blob/gh-pages/pyguide.md PEP8 error codes https://pep8.readthedocs.io/en/release-1.7.x/intro.html#error-codes line length http://jakevdp.github.io/blog/2017/11/09/exploring-line-lengths-in-python-packages/ https://nickjanetakis.com/blog/80-characters-per-line-is-a-standard-worth-sticking-to-even-today blank lines (2 after imports, 2 before functions, 1 before methods) https://www.python.org/dev/peps/pep-0008/#blank-lines
* _trailing commas_: for last el in collection https://docs.python.org/3/faq/design.html#why-does-python-allow-commas-at-the-end-of-lists-and-tuples https://www.python.org/dev/peps/pep-0008/#when-to-use-trailing-commas

governance
* Steering Council https://mail.python.org/pipermail/python-committers/2019-February/006520.html quasi-official (PyPA, PyCQA)
* _PEP_: RFCs for Python
* 0 (establish what a PEP is) 8 (style guide) 20 (Zen of Python) https://talkpython.fm/episodes/show/153/how-python-evolves https://peps.python.org/

## concurrency

📙 Beazley ch. 12
🗄
* web
* `system.md` concurrency

big picture
* Python as a language spec supports multiple threads
* CPython cannot execute cannot run threads in parallel https://stackoverflow.com/a/3086582
* Python is good at concurrency (IO e.g. networking) https://news.ycombinator.com/item?id=22907891
* Python is bad at parallelism (CPU e.g. search) http://esr.ibiblio.org/?p=8161

libraries https://testdriven.io/blog/concurrency-parallelism-asyncio/
* `multithreading`: actually parallel bc spawns own process i.e. heavier
* `asyncio`: single processor; pre-emptive multi-tasking (OS interrupts itself); lighter than threads
* `threading`: single processor; cooperative multi-tasking (code tells OS when to interrupt)

semantics https://python.hamel.dev/concurrency/
* thread
* process
* coroutine https://jeffknupp.com/blog/2013/04/07/improve-your-python-yield-and-generators-explained/

---

* task groups https://realpython.com/python311-new-features/#nicer-syntax-for-asynchronous-tasks
* parallelism https://github.com/taichi-dev/taichi
* threading https://news.ycombinator.com/item?id=22514004
* https://www.erichgrunewald.com/posts/gradually-migrating-python-code-to-asyncio/
* https://superfastpython.com/threading-in-python/
* functools.partial for actual parallelization?
* https://www.amazon.com/dp/1937785653
* https://github.com/rednafi/think-async

event loops https://questions.wizardzines.com/event-loops.html
* _event loop_: wrapper around OS service that tells you about network traffic https://www.pythonpodcast.com/episode-40-ben-darnell-on-tornado/
* also used in aeronautics https://news.ycombinator.com/item?id=27115372
* just a for loop https://softwareengineering.stackexchange.com/q/214889/322090

* https://lwn.net/Articles/872869/
* _GIL_: https://pythonspeed.com/articles/python-gil/ https://pythonbytes.fm/episodes/show/23/can-you-grok-the-gil http://python-notes.curiousefficiency.org/en/latest/python3/multicore_python.html https://www.youtube.com/watch?v=7RlqbHCCVyc http://www.dabeaz.com/python/UnderstandingGIL.pdf https://simonwillison.net/2021/Sep/29/the-gil-and-its-effects-on-python-multithreading/
changing would break C code https://old.reddit.com/r/Python/comments/sy369l/your_python_4_dream_list/
parallel https://towardsdatascience.com/parallelizing-python-code-3eb3c8e5f9cd
async https://www.youtube.com/watch?v=olT7ejlv0uE&list=PL2Uw4_HvXqvYk1Y5P8kryoyd83L_0Uk5K&index=43
https://calpaterson.com/async-python-is-not-faster.html
https://snarky.ca/unravelling-async-and-await/
https://www.encode.io/articles/python-async-frameworks-beyond-developer-tribalism
https://pythonbytes.fm/episodes/show/184/too-many-ways-to-wait-with-await
https://nullprogram.com/blog/2020/05/24/
https://whatisjasongoldstein.com/writing/im-too-stupid-for-asyncio/
https://news.ycombinator.com/item?id=22901856
📍 define 'asynchronous', 'concurrent', 'parallel' https://pythonbytes.fm/episodes/show/161/sloppy-python-can-mean-fast-answers
https://www.cloudcity.io/blog/2019/02/27/things-i-wish-they-told-me-about-multiprocessing-in-python/ what does multiprocessing mean exactly? https://news.ycombinator.com/item?id=25220674
multiprocessing https://github.com/spotify/pedalboard
https://realpython.com/intro-to-python-threading/
https://realpython.com/python-concurrency/
* _sink_: 搜 Gmail 'maestro system design'
https://realpython.com/python-async-features/
https://news.ycombinator.com/item?id=22396740
https://lucumr.pocoo.org/2020/1/1/async-pressure/
https://news.ycombinator.com/item?id=22514004
* http://aosabook.org/en/posa/working-with-big-data-in-bioinformatics.html
* https://news.ycombinator.com/item?id=23243237

🗄 `py-concurrency.pdf` https://www.youtube.com/watch?v=iG6fr81xHKA 'Flask for web dev' chapter 2 https://testdriven.io/blog/building-a-concurrent-web-scraper-with-python-and-selenium/ https://stackabuse.com/overview-of-async-io-in-python-3-7/ https://pyvideo.org/pygotham-2018/how-i-learned-to-stop-worrying-and-love-atomic-banking-blunders-and-concurrency-challenges.html https://realpython.com/quizzes/python-concurrency/

* _asyncio_: stdlib async lib; came in w/ 3.4 https://www.roguelynn.com/archives/
* _uvloop_: faster replacement for asyncio; impl using Cython and libuv (C lib for async)
* _Twisted/Tornado_: Python 2 era event loops, used in Scrapy http://masnun.rocks/2016/11/17/exploring-asyncio-uvloop-sanic-motor/ Tornado is also an app framework https://www.pythonpodcast.com/twisted-with-moshe-zadka-episode-170/ https://glyph.twistedmatrix.com/2019/06/kernel-python.html http://aosabook.org/en/twisted.html
* _gevent_: something to do w/ greenlet http://www.gevent.org/ http://flask.pocoo.org/docs/1.0/design/#thread-locals used by Grinberg in Flask sockets https://blog.miguelgrinberg.com/post/easy-websockets-with-flask-and-gevent

---

https://tonybaloney.github.io/posts/async-test-patterns-for-pytest-and-unittest.html

* _thread locals_: exists for duration of thread, seems globally available to your src but are actually copied for each thread https://stackoverflow.com/a/11984017 ❓ why are they typically a bad idea? http://flask.pocoo.org/docs/1.0/design/#thread-locals

* enable isolation amid multi-tentancy (i.e. multiple users) https://blog.sentry.io/2018/11/14/how-to-build-saas-application
https://stackoverflow.com/questions/1408171/thread-local-storage-in-python
https://stackoverflow.com/questions/104983/what-is-thread-local-storage-in-python-and-why-do-i-need-it


---

📺 https://training.talkpython.fm/courses/explore_async_python/async-in-python-with-threading-and-multiprocessing

* https://www.youtube.com/watch?v=OxzVApXKWYM
* https://medium.com/@anthonypjshaw/9440d28fa93d
* https://www.youtube.com/watch?v=MCs5OvhV9S4&t=4s
* https://www.youtube.com/watch?v=5dMOYf0b_20
* https://www.youtube.com/watch?v=w2nKIGhXPAM
* https://realpython.com/python-concurrency/
* https://realpython.com/intro-to-python-threading/
* https://www.youtube.com/watch?v=bckD_GK80oY
* https://realpython.com/courses/python-3-concurrency-asyncio-module/
* https://www.youtube.com/watch?v=9zinZmE3Ogk
* https://www.youtube.com/watch?v=MCs5OvhV9S4
* https://bytes.yingw787.com/posts/2019/01/12/concurrency_with_python_threads_and_locks/
* https://bytes.yingw787.com/posts/2019/01/11/concurrency_with_python_why/
* requests have async plugin now https://github.com/encode/requests-async

## control flow

🗄 `language.md`
📜 https://docs.python.org/3/tutorial/controlflow.html

* _switch statement replacements_: bisect https://stackoverflow.com/a/61030734/6813490 https://www.youtube.com/watch?v=gllUwQnYVww https://github.com/ralsina/enum_switch https://pythonbytes.fm/episodes/show/135/macos-deprecates-python-2-will-stop-shipping-it-eventually https://pythonbytes.fm/episodes/show/135/macos-deprecates-python-2-will-stop-shipping-it-eventually https://docs.python.org/3/faq/design.html#why-isn-t-there-a-switch-or-case-statement-in-python enums https://florian-dahlitz.de/blog/why-you-should-use-more-enums-in-python
* _pass_: results in NOP https://wsvincent.com/python-pass-statement/
* returns neither True nor False

operators
* _logical_: `and` and `or` short-circuit https://docs.python.org/3/tutorial/datastructures.html#more-on-conditions
* _comparison_: can be chained e.g. `a > b == c` https://docs.python.org/3/tutorial/datastructures.html#more-on-conditions

true and false
* _truthy_: non-empty collections, num greater than zero
* _falsy_: empty collections, zero, None
```python
# toggle boolean https://stackoverflow.com/a/8381955 https://realpython.com/python-boolean/
x = True
x = not x

# syllogism https://blog.carlmjohnson.net/post/2020/python-square-of-opposition/
all(['hi', 'hey'])  # True
all(['hi', 'hey', ''])  # False
any(['hi', 'hey', ''])  # True
any([''])  # False
```

* if
```python
# unaffected by execution of previous if statements https://stackoverflow.com/a/53545252
def if_example():
    if True:
        print("i will print")
    if True:
        print("i will also print")

# multiline
if (
    'spam' in email['sender'] or
    'spam' in email['subject'] or
    'spam' in email['metadata']
    ):
else:

# ternary
print("bigger \n") if a > b else print("smaller")
this() if x else that()
return True if x else False
# assignment
var = foo if condition else bar
```

## interpreter

📙 Shaw cpyton internals
🗄
* `language.md` compilers
* pdb
* REPL

using interpreter from shell https://docs.python.org/3/using/cmdline.html
* script: `python <mod>` https://realpython.com/run-python-scripts
* script + pdb: `python -i <mod>` https://docs.python.org/3/using/cmdline.html#cmdoption-i
* use module: `python -m unittest discover` https://docs.python.org/3/using/cmdline.html#cmdoption-m
* cmd inline: `python -c "import example.foo; foo.bar()"` https://docs.python.org/3/using/cmdline.html#cmdoption-c

stages https://www.youtube.com/watch?v=QU158nGABxI 25:30
* parse https://www.pythonpodcast.com/cpython-parser-replacement-episode-285/
* compile
* execute (interpreter loop)

C exentions 📙 Beazley ch. 15
* simplistic interpreter = C extensions = Python for datascience https://lucumr.pocoo.org/2018/7/13/python/
* can write extensions in Rust https://towardsdatascience.com/nine-rules-for-writing-python-extensions-in-rust-d35ea3a4ec29 https://github.com/RustPython/RustPython

---

Shannon plan, PEP 659, adaptive interpreter https://realpython.com/python311-new-features/#faster-code-execution

misc
* _contributing_: https://medium.com/@Captain_Joannah/so-you-want-to-contribute-to-cpython-gather-here-5a2694148ca4 http://emilyemorehouse.com/blog/015-my-path-to-becoming-a-python-core-developer/ http://lukasz.langa.pl/cv/ https://paper.dropbox.com/doc/Contributing-to-CPython--AuND60K_lABiNS7PHp0KZ9hoAg-JlgnduI6kw9MJIaGPpN9G
* _portable_: https://www.scylladb.com/2019/02/14/the-complex-path-for-a-simple-portable-python-interpreter-or-snakes-on-a-data-plane/
* _optimization_: minimize function calls and obj attr lookup https://gregoryszorc.com/blog/2019/01/10/what-i've-learned-about-optimizing-python/
* why Python doesn't have `main()` https://news.ycombinator.com/item?id=23904313
* _sink_: https://realpython.com/cpython-source-code-guide https://hackernoon.com/has-the-python-gil-been-slain-9440d28fa93d https://realpython.com/run-python-scripts/#whats-the-python-interpreter https://snarky.ca/what-is-the-core-of-the-python-programming-language

* going faster https://talkpython.fm/episodes/show/339/making-python-faster-with-guido-and-mark
* https://www.freecodecamp.org/news/hacking-together-a-simple-graphical-python-debugger-efe7e6b1f9a8/ https://github.com/puremourning/vimspector
https://tenthousandmeters.com/blog/python-behind-the-scenes-6-how-python-object-system-works/
CPython 🗄 `cpython-internals.pdf` https://talkpython.fm/episodes/show/240/a-guided-tour-of-the-cpython-source-code https://github.com/python/cpython
* has no formal spec https://www.pythonpodcast.com/cpython-formal-specification-episode-288/
* _Python_: language spec; very much tied to CPython e.g. metaclasses https://news.ycombinator.com/item?id=23698846
* _components_: stdlib in Python, core objects and IO in C
* _PVM_: virtual machine https://leanpub.com/insidethepythonvirtualmachine/read
* _CPython_: compiler (reference impl of lang spec) + PVM https://eli.thegreenplace.net/2010/09/18/python-internals-symbol-tables-part-1#id5; core written in C https://docs.python-guide.org/starting/which-python/#implementations libs written in Python https://realpython.com/python-logging-source-code/ how to contribute https://pythonbytes.fm/episodes/show/37/rule-over-the-shells-with-sultan
* _PEM_: execution model
* compiled to bytecode https://www.pythoninsight.com/2018/09/python-basics-bytecode/ https://snarky.ca/not-unravelling-generator-expressions/
* executes in the PVM https://realpython.com/run-python-scripts/#how-does-the-interpreter-run-python-scripts https://stackoverflow.com/q/441824/6813490 https://leanpub.com/insidethepythonvirtualmachine/read https://stackoverflow.com/q/6889747/6813490
* simplistic interpreter = C extensions = Python for datascience https://lucumr.pocoo.org/2018/7/13/python/
* can write extensions in Rust https://towardsdatascience.com/nine-rules-for-writing-python-extensions-in-rust-d35ea3a4ec29 https://github.com/RustPython/RustPython
* _bytecode_: https://opensource.com/article/18/4/introduction-python-bytecode https://nullprogram.com/blog/2019/02/24/ https://snarky.ca/unravelling-attribute-access-in-python/ https://www.youtube.com/watch?v=QU158nGABxI 23:00 28:30
* compiler execution flow: Python src to bytecode, VM runs bytecode https://eli.thegreenplace.net/2012/03/23/python-internals-how-callables-work https://eli.thegreenplace.net/2010/06/30/python-internals-adding-a-new-statement-to-python/
> CPython bytecode is evaluated by the the mammoth function PyEval_EvalFrameEx in Python/ceval.c. The function is scary but it's nothing more than a fancy dispatcher of opcodes.

alternatives
* unique insofar as has to fit many use cases (web, CLI, security) https://talkpython.fm/episodes/show/265/why-is-python-slow 47:00
* things that need to be fast will be written in C https://talkpython.fm/episodes/show/265/why-is-python-slow 50:00
* _pypy_: JIT, supports Python 2 https://news.ycombinator.com/item?id=22928030 http://aosabook.org/en/pypy.html https://ao.gl/when-your-python-code-is-much-faster-with-pypy/ https://www.reddit.com/r/Python/comments/bv50uz/is_anyone_using_pypy_on_production/ https://realpython.com/pypy-faster-python/ https://avi.im/blag/2021/fast-sqlite-inserts/ 📙 Beazly 595
* _numba_: just add annotation https://talkpython.fm/episodes/show/265/why-is-python-slow 37:00 https://news.ycombinator.com/item?id=30205848 📙 Beazly 595
* _pyjion_: https://talkpython.fm/episodes/show/340/time-to-jit-your-python-with-pyjion
* _Cython_: write Python, get perf of C++ 🗄 'executables'
* _others_: Jython (Java) Iron Python (.NET) call Go from Python https://opendatagroup.github.io/development/2019/06/13/go-ffi.html

## math

🗄 `computers.md` theory/numeral systems
🔗 https://github.com/cosmologicon/pywat
📙 Beazley ch. 3

* _infix operator_: `*`

floating point arithmetic 📙 Van Rossum ch. 15
* comparing floats: `math.isclose(0.1 + 0.2, 0.3)` https://davidamos.dev/the-right-way-to-compare-floats-in-python/
> You can specify the relative tolerance with the rel_tol keyword argument of math.isclose() which defaults to 1e-9. In other words, if abs(a - b) is less than 1e-9 * max(abs(a), abs(b)), then a and b are considered "close" to each other. This guarantees that a and b are equal to about nine decimal places.
* rounding https://stackoverflow.com/a/43661374
```python
# rm decimal
int(1.9)  # 1

# round to closest
round(1.9)  # 2
round(1.94, 1)  # 1.9

# round down
math.floor(1.9)  # 1

# round up
math.ceil(1.1)  # 2
```

---

* use `localcontext` when dealing w/ decimals https://orbifold.xyz/numbers.html

```python
###
# INTS & FLOATS https://davidamos.dev/the-right-way-to-compare-floats-in-python/ 📙 Van Rossum ch. 15
###

# increment operators https://stackoverflow.com/a/15376520

# + -> calls __add__()
num = 0
num + 1
num  # 0
# += -> calls __iadd__(), can't use in return statement
num = 0
num += 1
num  # 1

def inc(num):
    return num + 1 # ✅
    return num += 1  # ❌

###################################################

# main types
# integers are objects https://pythonspeed.com/articles/python-integers-memory/
int()  # can be as big as your memory can deal with https://realpython.com/python-data-types/#integers
float()

# can also represent binary and complex
0b10  # 2  https://realpython.com/python-data-types/#integers
42+7j  # <class 'complex'> https://realpython.com/python-data-types/#complex-numbers [Saha 1.6]

# conversions -> can't convert float string to int [Saha 1.8]
float('1')  # 1.0
int('1')  # 1
float('1.0')  # 1.0
int('1.0')  # ValueError

# validate floats
1.0.is_integer()  # True
1.3.is_integer()  # False

# integers turn to floats if division https://orbifold.xyz/numbers.html
4/3

# avoid floats with floor division operator [Saha 1.2]
4//3

# variables holding integers btw -5 and 256 are just references to existing obj in Python integer cache https://wsvincent.com/python-wat-integer-cache/ https://arpitbhayani.me/blogs/python-caches-integers
a = 8
b = 8
id(a)  # 4304845536
id(b)  # 4304845536

# negative infinity https://www.interviewcake.com/article/python/big-o-notation-time-and-space-complexity
float("-inf")

# square root via exponent operator [Saha 1.3]
8 ** (1/3)
```

## metaprogramming

📜 https://docs.python.org/3/library/language.html
🗄 `language.md`
📙 Beazley ch. 9

* view source https://stackoverflow.com/a/1562795
```python
from inspect import getsource
print(getsource(ur_func))
```

working with AST
* inspect https://hakibenita.com/automating-the-boring-stuff-in-django-using-the-check-framework
* https://www.mattlayman.com/blog/2018/decipher-python-ast/
* https://talkpython.fm/episodes/show/152/understanding-and-using-python-s-ast
* get data structure from string `ast.literal_eval(ds_as_str)` https://stackoverflow.com/a/17768535

decorators
* _decorator_: factory + functionality
* use cases
```python
# logging

# caching

# sanitization

# app config https://bytepawn.com/python-decorators-for-data-scientists.html

# execeptions https://dev.to/fcurella/refining-exceptions-with-context-decorators-31i5

# login https://realpython.com/primer-on-python-decorators/#a-few-real-world-examples

# pagination https://stackoverflow.com/questions/53638221/unable-to-handle-two-links-having-different-pagination-using-decorator
```

---

* https://bas.codes/posts/python-decorators
* https://blog.luisrei.com/articles/flaskrest.html
* https://stackoverflow.com/questions/308999/what-does-functools-wraps-do
* https://samireland.com/writing/decorators/ https://rednafi.github.io/digressions/python/2020/05/13/python-decorators.html
* _decorator_: factory that takes func and adds functionality via inner function; introduced in 2.4 via PEP 318
* _basics_: https://realpython.com/primer-on-python-decorators/#a-few-real-world-examples https://www.youtube.com/watch?v=MjHpMCIvwsY
* _factory_: https://joeriksson.io/blog/Decorator-with-arguments/ https://realpython.com/inner-functions-what-are-they-good-for/#conclusion https://stackoverflow.com/a/28695034/6813490 https://www.learnpython.org/en/Decorators https://stackoverflow.com/questions/10957409/python-naming-conventions-in-decorators https://realpython.com/inner-functions-what-are-they-good-for/#conclusion https://zenhack.net/2016/12/25/why-python-is-not-my-favorite-language.html

* pre-2.4
```python
def my_decorator(func):
    def wrapper():
        print(f"my_decorator is wrapping {func}")
        func()
    return wrapper

def use_decorator():
    print("calling use_decorator")

use_decorator = my_decorator(use_decorator)
```

* syntactic sugar https://realpython.com/primer-on-python-decorators/#simple-decorators
```python
def my_decorator(func):
    def wrapper():
        print(f"my_decorator is wrapping {func}")
        func()
    return wrapper

@my_decorator
def use_decorator():
    print("calling use_decorator")
```

* decorator that can handle the decorated functions args
```python
def my_decorator(func):
    def wrapper(*args, **kwargs):  # wrapper takes function args just like my_decorator takes function itself
        print(f"my_decorator is wrapping {func}")
        func(*args, **kwargs)
    return wrapper

@my_decorator
def use_decorator(name):
    print(f"calling use_decorator with args {name}")
```

* decorator w/ introspection
```python
import functools

def my_decorator(func):
    @functools.wraps(func)
    def wrapper():
        print(f"my_decorator is wrapping {func}")
        func()
    return wrapper

@my_decorator
def use_decorator():
    print("calling use_decorator")
```

## version mgmt

📜
* https://github.com/pyenv/pyenv
* https://realpython.com/intro-to-pyenv
🗄 `python-3.10-youtube-ffmpeg.md`

pyenv
* _pyenv_: wrapper that passes cmd to appropriate version http://akbaribrahim.com/managing-multiple-python-versions-with-pyenv/#how-pyenv-works https://rutar.org/writing/managing-python-versions-with-pyenv/
* can use different interpreter (PyPy, Jython) https://realpython.com/intro-to-pyenv/
* install: Homebrew https://jacobian.org/2019/nov/11/python-environment-2020/ Linux https://mitelman.engineering/blog/python-best-practice/automating-python-best-practices-for-a-new-project/
* fs: `~/.pyenv/versions`
* cmd
```sh
# list cmd
pyenv commands
# list which version in use
pyenv which python
# list installed versions
pyenv versions
# list versions available for install https://stackoverflow.com/a/58138512 upgrade pyenv to grab latest https://stackoverflow.com/a/43996315
pyenv install -l
# set local version (creates `.python-version` in $CWD)
pyenv local 3.9
# set global version e.g. 3.9, system
pyenv global <ver>
# list library version https://realpython.com/intro-to-pyenv/#which
pyenv which <library>
```

pyenv at United Masters
* macOS M1 issues https://news.ycombinator.com/item?id=26018722
* x86 brew to fix pyenv https://www.mejorcodigo.com/p/97778.html
```sh
if command -v pyenv 1>/dev/null 2>&1; then
    eval "$(pyenv init --path)"
fi
eval "$(brew shellenv)"
eval "$(pyenv init --path)"

# install brew x86_64
arch -x86_64 /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
# install brew arm64
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
# alias Brew
alias brew86="arch -x86_64 /usr/local/Homebrew/bin/brew"
# install pyenv
brew86 install pyenv
# in case doesn't get linked add to the PATH brew86 dirs (consider to put it at the begining of your .zbashrc file)
export PATH=/usr/local/Homebrew/bin:/usr/local/Homebrew/sbin:$PATH
# install python through pyenv
pyenv install 3.8.5
# necessary?
$ brew86 install openssl readline sqlite3 xz zlib
```

versions https://docs.python.org/3/whatsnew/index.html https://nedbatchelder.com/text/which-py.html
* major https://en.wikipedia.org/wiki/History_of_Python#Table_of_versions
* minor/patch https://blog.python.org/
* don't switch too early https://pythonspeed.com/articles/switch-python-3.10/
* _89_: initial
* _00_: Python 2
* _08_: Python 3 https://nedbatchelder.com/blog/201803/whats_in_which_python_3436.html
* _18_: 3.7
* _19_: 3.8 https://realpython.com/courses/cool-new-features-python-38/
* _20_: Python 2 EoL

version inheritance
* Homebrew
* pipx: installed by Homebrew but can/will have different Python version as dependency
* Poetry: inherits from pipx
* project: inherits from Poetry (e.g. qing/send2track)

Anaconda
* it's just some random company https://chriswarrick.com/blog/2017/07/03/setting-up-a-python-development-environment/
* _conda_: pkg manager + Python version (400 MB); install via `miniconda`; 400MB; can install databases, non-Python pkg
* _anaconda_: all the pkgs (3 GB); install via `anaconda` https://stackoverflow.com/a/30057885/6813490
* ❓ mini/conda play nice w/ existing Python install? https://www.thisismetis.com/assets/files/Metis-Bootcamp-Curriculum-52f9979f4f638857bc185b0b788d6d832efb7f34d3b240e199dc6d3f2eef40ed.pdf
* https://mlpipes.com/changing-the-python-version-in-conda/ https://conda.io/docs/user-guide/install/index.html https://www.anaconda.com/blog/developer-blog/using-pip-in-a-conda-environment/ http://jakevdp.github.io/blog/2016/08/25/conda-myths-and-misconceptions/ http://www.sexchrlab.org/blog/2015/10/26/managing-multiple-python-environments-using-anaconda https://tdhopper.com/blog/my-python-environment-workflow-with-conda/ virtual env https://janakiev.com/til/jupyter-virtual-envs/

options
* ❌ system: pkg mgmt (yum) require own version https://realpython.com/intro-to-pyenv/#why-not-use-system-python
* ❌ macOS command line tools https://justinmayer.com/posts/homebrew-python-is-not-for-you/ https://docs.brew.sh/Homebrew-and-Python#python-3x
* ❌ PSF: no uninstaller https://chriswarrick.com/blog/2017/07/03/setting-up-a-python-development-environment/#macos https://docs.python.org/3/using/index.html
* ❌ Homebrew: will update interpreter under your feet https://justinmayer.com/posts/homebrew-python-is-not-for-you/ https://realpython.com/intro-to-pyenv/#what-about-a-package-manager
* ❓ Anaconda
* ❓ nix; https://github.com/DavHau/mach-nix https://github.com/nix-community/poetry2nix
* ❓ asdf: https://justinmayer.com/posts/homebrew-python-is-not-for-you/
* ✅ pyenv

non-trivial
* new versions have syntax/features unsupported by other tools https://pythonspeed.com/articles/major-python-release/
* _PEP 394_: `python` should continue to point to OS version for comptability reasons https://github.com/sdispater/poetry/issues/536#issuecomment-507897724
* easy to shoot yourself in the foot https://xkcd.com/1987 but it's still your fault https://snarky.ca/deconstructing-xkcd-com-1987/
* too many versions on local https://www.hackerfactor.com/blog/index.php?/archives/825-8-Reasons-Python-Sucks.html
* Vincent https://talkpython.fm/episodes/show/190/teaching-django Guido https://twitter.com/brettsky/status/991172186911076352

after you've already installed PSF https://wsvincent.com/announcing-python3-website/ 
> shim: repoint `python3` to Hombrew, reinstall pipx using that and then reinstall Poetry using pipx
* _macOS_: `python` 'legacy approaches'
* _PSF_: `python3`; zbin, Poetry, pipx, pip3 and pip (Mojave upgrade repointed) use PSF
* _brew_: both 2 and 3, unsure if other Homebrew deps use 🗄 `ddgr.log` `httpie-plus-python.log`
```text
tldr: There should be a section on how to uninstall a PSF version.

My suspicion is this: due to all the usual factors (Python as a teaching language, growing popularity) a disproportiate percentage of people will come to the site after they've taken the very natural step of 1) Googling 'python' 2) landing on the PSF site 3) downloading Python from the PSF. By the time they find your site, it will be too late.

Just thought of this; I'm skimming Al Sweigart's 'Cracking Codes in Python', explicitly aimed at a beginner Python audience, and of course the intro points people to the PSF install.

I myself am in this situation. I have Python 3.6 installed from the PSF. 📍 how to point to Homebrew version https://stackoverflow.com/a/4584180/6813490 would pyenv be able to paper over this?

Also, great to see the site. I heard you on the Talk Python to Me and your comments there about installation being much more difficult than the community seems to give it credit very much resonated with me.
```
```sh
# can point to Homebrew version, open REPL and import dataclasses

# PSF
/Library/Frameworks/Python.framework/Versions
# Homebrew
/usr/local/Cellar/python/3.7.5/Frameworks/Python.framework/Versions
```

## web

📙 Beazley ch. 11
🗄
* `application.md` utils
* `language.md` frameworks

requests 📜 https://requests.readthedocs.io/en/latest/
* alternatives: https://github.com/search?utf8=%E2%9C%93&q=aiohttp https://github.com/encode/httpx single-file https://github.com/slingamn/mureq
* `raise_for_status`: raise exception for 400/500 https://requests.readthedocs.io/en/master/user/quickstart/#json-response-content
```python
res = requests.post(url, data=data)
res.raise_for_status()
```
* mock requests https://github.com/jamielennox/requests-mock
* timeouts https://findwork.dev/blog/advanced-usage-python-requests-timeouts-retries-hooks/ https://robertovitillo.com/default-timeouts/
```python
# BASICS
requests.get(url)
requests.post(url, data=data)
requests.put(url, data=data)

# DOWNLOAD FILE
with open("tmp.text", "wb") as f:
    f.write(res.content)

# DOWNLOAD FILE WITH AUTH TOKEN https://stackoverflow.com/a/44699717
res = requests.get(
    'https://gitlab.com/zachvalenta/pre-commit-test/repository/archive.tar.gz?ref=master',
    headers={'PRIVATE-TOKEN': 'urPrivateToken'}
)
if res.url == "https://gitlab.com/users/sign_in":
    print("set token")
    os._exit(0)
with open(r'zjv_test.tar.gz', 'wb') as f:
    f.write(res.content)

# UPLOAD FILE https://2.python-requests.org/en/master/user/quickstart/#post-a-multipart-encoded-file https://2.python-requests.org/en/master/user/advanced/#post-multiple-multipart-encoded-files
my_file = {"file": open("foo.txt", "rb")}  # idk if 'file' significant here
requests.post(url, files=my_file)  # PUT also works fine

# RM FILE
res = requests.delete(url, auth=(user, pw))
```

frameworks
> Web development is often broad, not deep - problems span many domains https://docs.djangoproject.com/en/2.0/intro/whatsnext/
> A framework is a text where you fill in the blanks. The framework defines the grammar, you bring some of the words. https://blog.startifact.com/posts/framework-patterns.html
* components: HTTP, routes, ORM
* BYO https://www.destroyallsoftware.com/screencasts/catalog https://www.youtube.com/watch?v=7kwnjoAJ2HQ https://testdriven.io/courses/python-web-framework/ https://www.amazon.com/dp/1937785637 https://rubyonrails.org/doctrine/

---

WSGI 
* interface btw app server and framework https://docs.python-guide.org/scenarios/web/#wsgi bc pre-WSGI which framework you picked determined which web server you could use https://www.pythonpodcast.com/episode-43-wsgi-2/ @ 08:00
* _interface_: contract e.g. "app server will do these things in this way as specified by WSGI and app framework will hook into them in this way as specified by WSGI and that way gunicorn will work with any WSGI-compliant app framework and Flask will work with any-WSGI compliant app server"
* _constraints_: single-threaded https://stackoverflow.com/a/32217701 doesn't do async or WebSockets https://pythonbytes.fm/episodes/show/48/garbage-collection-and-memory-management-in-python https://www.pythonpodcast.com/episode-43-wsgi-2/ @ 18:00
* _supported by_: servers (gunicorn, uWSGI, mod_wsgi) frameworks (Flask, Django, Falcon, Pyramid)
* https://stackoverflow.com/a/38685758/6813490 https://talkpython.fm/episodes/show/13/flask-web-framework-and-much-much-more @ 30:00 https://djangodeconstructed.com/2018/02/15/how-a-request-becomes-a-response-diving-deeper-into-wsgi

ASGI
* _ASGI_: async alternative
* frameworks: Django (Channels) Quart (Flask on async) Twisted (don't think actually ASGI but does async) new (Sanic, Starlette, FastAPI built on Starlette)
* servers: uvicorn, Daphne
* sink: https://www.youtube.com/watch?v=7kwnjoAJ2HQ @ 10:55 Django moving this way https://docs.djangoproject.com/en/dev/releases/3.0/ async db https://github.com/encode/orm https://github.com/django/asgiref https://www.pythonpodcast.com/django-channels-and-the-asynchronous-web-with-andrew-godwin-episode-180/ https://github.com/florimondmanca/awesome-asgi  https://pythonbytes.fm/episodes/show/148/the-asgi-revolution-is-upon-us
