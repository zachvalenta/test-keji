# TODO

## 参考

`python.md` testing

## current

## next

❓ why isn't doctest used more?
* vim-test: run test under cursor https://www.youtube.com/watch?v=7VP7TdItuEs https://www.semicolonandsons.com/episode/IDE-like-refactors-snippets-tests-hover-docs-commenting-and-git 1:40
* vim-projectionist: switch btw src and test https://subvisual.com/blog/posts/133-super-powered-vim-part-i-projections/ https://www.semicolonandsons.com/episode/IDE-like-refactors-snippets-tests-hover-docs-commenting-and-git 1:15
* https://blog.thea.codes/my-python-testing-style-guide
* https://www.destroyallsoftware.com/screencasts/catalog/functional-core-imperative-shell https://bytes.yingw787.com/posts/2018/11/07/data_driven_testing/
* doubles
* testing types

## done

* _2020_: pre-commit for Git hooks, behave for bdd
* _2019_: switch to pytest
* _2018_: exposure to coverage and Git hooks, course on unit testing in Python
* _2017_: integration test suite using Selenium
* _2016_: basics at Zip Code

# INTEGRATION

* testing object store (S3) https://www.sanjaysiddhanti.com/2020/04/08/s3testing/ https://www.youtube.com/watch?v=NBICMF0i4Ok

HTTP
* https://github.com/kevin1024/vcrpy
* https://github.com/hiredscorelabs/cornell

UI
* synthetic https://docs.datadoghq.com/synthetics/
* mocking API = faster test runs but highe chance of rot; tooling (json-server, duckrails)
* visual diff https://css-tricks.com/video-screencasts/178-percy-catches-visual-changes-in-any-workflow/
* browser automation: JS (Cypress, https://github.com/puppeteer/puppeteer, Selenium) Python https://github.com/microsoft/playwright-python https://github.com/golemhq/golem 
* view user flow, Chrome recorder panel https://developer.chrome.com/docs/devtools/recorder/ https://www.thoughtworks.com/radar/tools?blipid=202203004
* capture disappearing element https://stackoverflow.com/a/38783090/6813490
* cross browser https://www.browserling.com/

## db

🗄
* `db.md` migrations
* `django.md` migrations
* `system.md` application config

approaches
* clone https://github.com/postgres-ai/database-lab-engine
* db as normal and eat the speed costs https://changelog.com/podcast/145 https://corecursive.com/045-david-heinemeier-hansson-software-contrarian/ 48:00
* speed up by disabling `fsync` (system call to write to disk) bc you don't care if the data is actually written to disk https://pythonspeed.com/articles/faster-db-tests/ http://aosabook.org/en/nosql.html https://www.mongodb.com/docs/manual/reference/glossary/#std-term-fsync
* db in container https://github.com/orlangure/gnomock https://www.dudley.codes/posts/2020.10.02-golang-docker-integration-tests/ https://github.com/testcontainers https://www.thoughtworks.com/radar/languages-and-frameworks?blipid=201911027
> Imagine you have some application code that opens a connection to a Postgres database and queries some customer data. The customary way to test this code would be to create a test database and populate it with test customer data. However, what if application code modifies rows in the database, like removing customers? If the above code runs on a modified database, it may not return the expected customer. Therefore, it's important to reset the state of the database between test cases so that tests behave predictably. But connecting to a database is slow. Running queries is slow. And resetting the state of an entire database between every test is really slow. Various mocking libraries are another alternative to using a test database. These libraries intercept calls at some layer of the application or data access stack, and return canned responses without needing to touch the database. The problem with many of these libraries is that they require the developer to manually construct the canned responses, which is time-consuming and fragile when application changes occur. copyist includes a Go sql package driver that records the low-level SQL calls made by application and test code. When a Go test using copyist is invoked with the "-record" command-line flag, then the copyist driver will record all SQL calls. When the test completes, copyist will generate a custom text file that contains the recorded SQL calls. The Go test can then be run again without the "-record" flag. This time the copyist driver will play back the recorded calls, without needing to access the database. The Go test is none the wiser, and runs as if it was using the database. https://github.com/cockroachdb/copyist
* testing writes http://eradman.com/posts/database-test-isolation.html

## behave/BDD

📜 https://behave.readthedocs.io/en/latest/ https://github.com/behave/behave

* CLI
```sh
# view stdout https://stackoverflow.com/a/28551235/6813490 https://stackoverflow.com/a/41969164/6813490
behave --no-capture --no-color --tags @foo

# exclude tag
--tags ~@tag1        # single
--tags ~@tag1, tag2  # n
```

* project setup
```sh
# default https://behave.readthedocs.io/en/latest/gherkin.html?highlight=directory#feature-testing-layout
├── features
│   └── foo.feature
│   └── bar.feature
│   └──── steps
│   └─────── baz.py

# with config https://behave.readthedocs.io/en/latest/behave.html?highlight=configuration#configuration-files
├── bdd
│   └── features
│   └──── foo.feature
│   └── steps
│   └──── foo.py

# .behaverc
[behave]
paths=dj_app/bdd
```

* step syntax
```python
from behave import given, then

@given('we have behave installed')
def step_impl(context):
    pass

@then('behave will test them for us!')  # actual identifier in decorator
def step_impl(context):  # function identifier identical; must take `context` as arg
    assert context.failed is False  # vanilla assertions
```

misc
* alternative https://github.com/pytest-dev/pytest-bdd 
* same syntax as Cucumber https://stackoverflow.com/a/52027041
* few commits but seems active https://github.com/behave/behave/projects/4#card-50138436)
* Django integration: https://behave.readthedocs.io/en/latest/usecase_django.html https://whoisnicoleharris.com/2015/03/19/bdd-part-two.html https://semaphoreci.com/community/tutorials/setting-up-a-bdd-stack-on-a-django-application
> we got around at work bc we're just using to hit our deployed endpoints

BDD in general
* origins (RSpec, Cucumber)
* _step_: line of human readable text corresponding to step definition (code)
* _scenario_: collection of steps
* _feature_: collection of scenarios
* keywords: given (preconditions) when (start) and (intermediate steps) then (assertion)
* be declarative, not imperative https://wiki.saucelabs.com/display/DOCS/Best+Practice%3A+Imperative+v.+Declarative+Testing+Scenarios
```text
# THIS
Given I am on the Login Page
When I sign in with correct credentials
Then I should see a welcome message

# NOT THIS
* Given I open a browser
* And I navigate to http://example.com/login
* When I type in the username field bob97
* And I type in the password field F1d0
* And I click on Submit button
* Then I should see the message Welcome Back Bob
```

# ZA

* _testdox_: generate docs from test method metadata/description https://pypi.org/project/pytest-testdox/

## approaches

speed https://gumroad.com/l/suydt
* fast to slow: autofmt, lint, unit tests, integration tests https://pythonspeed.com/articles/slow-tests-fast-feedback/ https://pythonspeed.com/articles/slow-tests-fast-feedback/
* run relevant tests first https://pythonspeed.com/articles/slow-tests-fast-feedback/
* _test splitting_: parallelize https://devblog.kogan.com/blog/django-test-splitting-on-circleci
* slow = time waste = less testing https://pythonspeed.com/articles/high-cost-slow-tests/

approaches
* _test last_: write code -> write tests
* _test first_: design tests -> write code -> write tests
* _TDD_: (write some code -> write a test) * ∞
* _BDD_: README-driven

misc
* _black box testing_: describe behavior via tests (so you can rewrite for feature parity) https://stackoverflow.blog/2022/03/09/rewriting-bash-scripts-in-go-using-black-box-testing/?cb=1
* test shape / distribution https://martinfowler.com/articles/2021-test-shapes.html
* testing as just another form of feedback, along with production error logs, user response https://softwareengineeringdaily.com/2019/08/28/facebook-engineering-process-with-kent-beck/
* people don't take testing seriously https://news.ycombinator.com/item?id=26156924
* one assertion per test case
* super specific method names
* write tests for the code you wish you had, write tests that aren't more trouble than they're worth https://lukeplant.me.uk/blog/posts/test-smarter-not-harder/
* testing pyramid http://blog.codepipes.com/testing/software-testing-antipatterns.html more integration than anything else https://kentcdodds.com/blog/write-tests https://www.semicolonandsons.com/episode/continuous-integration-testing-basics-and-what-to-test
* settings create exponential increase in test cases https://www.youtube.com/watch?v=glZ1C-Yu5tw
* there's no way to re-write something that isn't tested without losing functionality https://danluu.com/julialang/
* tests are the only docs that don't rot https://return.co.de/blog/articles/why-you-should-start-using-junit-5/
* everything that's not tested will break https://return.co.de/blog/articles/everything-not-tested-will-break/
* tests are about design (if the src is britter so, too, the tests) https://www.openmymind.net/Tests-Are-About-Design/
* writing tests takes time, debugging without them takes more
* coverage https://corecursive.com/066-sqlite-with-richard-hipp/
> I’d been doing some work for Rockwell Collins, an avionics manufacturer, Rockwell Collins, and they introduced me to this concept of DO-178B. It’s a quality standard for safety-critical aviation products, and unlike so many quality standards, this one’s actually readable. Now, it does have a lot of bureaucratic stuff in it, but you can actually buy a copy of this. You do have to buy it. It’s a couple hundred dollars, but it’s a reasonably thin volume and you can read through it, and with sufficient study you can understand what they’re talking about, so I did that, and I actually started following some of their processes, and one of the key things that they push is, they want 100% MCDC test coverage. That’s modified condition decision coverage of the code. Your tests have to cause each branch operation in the resulting binary code to be taken and to fall through at least once.
> It’s pretty easy to get up to 90 or 95% test coverage. Getting that last 5% is really, really hard and it took about a year for me to get there, but once we got to that point, we stopped getting bug reports from Android.
> How do you count tests? We’ll have a test case but it’ll be parametrized, so that one test case might run 100, 1,000, 100,000 tests, just by looping, by changing one of the parameters. For a typical release, we’ll do billions of tests, but we have, I think it’s on the order of 100,000 distinct test cases. Yes, so we’ll do billions of tests.
>  There is a huge difference between covering all lines and covering all code path permutations. You can have 100% code coverage and still have bugs. https://twitter.com/kamranahmedse/status/1070773424644083712

## doubles

* don't teardown db btw test runs
> Better yet, when your tests don't assume they're starting from a clean sheet, you can run your tests with a dump from production loaded into your database. This can help confirm that data access patterns you're using will work when the database, as a whole, is at production size. https://calpaterson.com/against-database-teardown.html

https://romantomjak.com/posts/testing-python-code-that-makes-http-requests.html
https://pythonspeed.com/articles/faster-db-tests/
https://talkpython.fm/episodes/show/287/testing-without-dependencies-mocking-in-python

* _mock_: override method so you can test; `unittest.mock` vs. `pytest.monkeypatch` https://www.b-list.org/weblog/2020/feb/03/how-im-testing-2020/ mock vs. magicmock https://stackoverflow.com/questions/17181687/mock-vs-magicmock https://realpython.com/python-mock-library/ https://joshpeak.net/posts/2019-06-18-Advanced-python-testing.html env var https://adamj.eu/tech/2020/10/13/how-to-mock-environment-variables-with-pytest
* mocks https://github.com/tommyboytech/t3/pull/11146/files
* _testing external resources_: use real thing, use Docker version https://github.com/schireson/pytest-mock-resources/ https://yanglinzhao.com/posts/test-elasticsearch-in-django
* https://blog.cleancoder.com/uncle-bob/2014/05/14/TheLittleMocker.html

* _double_: replace dependencies to isolate SUT e.g. "assume API is working, does my code work?" https://nedbatchelder.com/text/test3/test3.html#51 + 53, 56, 56
* _stub_: hard-coded answer; if double returns value it should be a stub https://www.quora.com/Software-Testing-What-is-the-difference-between-Mocks-and-Stubs
* _fake_: 类似 stub but w/ impl (still diff than real impl); common fakes incl. db, fs, server; verified fake https://pythonspeed.com/articles/verified-fakes/
* _mock_: 类似 fake but record what calls were made https://nedbatchelder.com/text/test3/test3.html#61

__terms__

* _spy_: 类似 mock but can view post-mortem

* _why use?_ prevent unit tests from becoming integration tests; isolation i.e. don't let test of A break bc A's call to B failed i.e. test one thing at a time
* _dummy object_: when you have to pass in something for a required argument; `fun(a=real_obj,b=None)`

https://nedbatchelder.com//blog/201908/why_your_mock_doesnt_work.html

📰  https://stackoverflow.com/questions/3459287/whats-the-difference-between-a-mock-stub https://martinfowler.com/articles/mocksArentStubs.html https://nedbatchelder.com//blog/201908/why_your_mock_doesnt_work.html https://blog.cleancoder.com/uncle-bob/2014/05/14/TheLittleMocker.html

🗣 mocking promotes unnecessary abstraction http://250bpm.com/blog:86

📙 [mock cookbook](https://chase-seibert.github.io/blog/2015/06/25/python-mocking-cookbook.html) + https://www.toptal.com/python/an-introduction-to-mocking-in-python + https://medium.com/@yeraydiazdiaz/what-the-mock-cheatsheet-mocking-in-python-6a71db997832 + https://realpython.com/python-mock-library/
* https://medium.com/ryans-dev-notes/python-mock-and-magicmock-b3295c2cc7eb
* https://thoughtbot.com/upcase/test-doubles
https://thoughtbot.com/upcase/test-doubles
* fake
* mock --> have an example from Python Cookbook with stdout https://www.youtube.com/watch?v=Ldlz4V-UCFw  https://pythonspeed.com/articles/verified-fakes/
* spy
* _monkey patch_: changing code at run-time

* https://medium.com/@yeraydiazdiaz/what-the-mock-cheatsheet-mocking-in-python-6a71db997832
* https://www.quora.com/Software-Testing-What-is-the-difference-between-Mocks-and-Stubs
* https://blog.pragmatists.com/test-doubles-fakes-mocks-and-stubs-1a7491dfa3da
* https://stackoverflow.com/questions/3459287/whats-the-difference-between-a-mock-stub/51998394#51998394

## formal methods

* __formal methods__: use math for testing
* aka automated reasoning
> Automated-reasoning tools can be incredibly fast, even when the domains are infinite (e.g., unbounded mathematical integers rather than finite C ints). Unfortunately, the tools may answer "Don’t know" in some instances.
```c
// question: could f ever return false?
bool f(unsigned int x, unsigned int y) {
   return (x+y == y+x);
}

// testing proof: call f on all possible pairs of values of the type unsigned int
// UINT_MAX typically 4B = 20 quintillion f calls to consider = need 1500 years
void main() {
   for (unsigned int x=0;1;x++) {
      for (unsigned int y=0;1;y++) {
         if (!f(x,y)) printf("Error!\n");
         if (y==UINT_MAX) break;
      }
      if (x==UINT_MAX) break;
   }
}

// algebra proof: that x + y = y + x -> f always returns true
```

* _TLA+_: https://buttondown.email/hillelwayne/archive/a-very-brief-intro-to-formal-methods-aka-my-job/ https://www.hillelwayne.com/post/why-dont-people-use-formal-methods/ https://www.learntla.com/introduction/ https://lamport.azurewebsites.net/tla/tla.html https://medium.com/@bellmar/introduction-to-tla-model-checking-in-the-command-line-c6871700a6a2 https://nchammas.com/writing/how-not-to-die-hard-with-hypothesis hypothesis testing https://github.com/pandera-dev/pandera Pact, contract testing https://www.thoughtworks.com/radar/tools?blipid=202110074

## semantics

source code
* _production code_: app itself
* _SUT_: prod code + env + collaborators + fixture/factory 🗄 `db.md` migration
* _collaborator_: system deps e.g. db, cache, server

test code & components
* _test code_: code testing app
* _case_: smallest unit of test code; generation https://github.com/randoop/randoop https://www.reddit.com/r/Python/comments/63e7sm/automated_test_case_generation/ https://github.com/usagitoneko97/klara check Python podcasts https://github.com/tjkendev/python-testcase-generator https://eli.thegreenplace.net/2014/04/02/dynamically-generating-python-test-cases https://github.com/se2p/pynguin
* _suite_: collection of cases
* _runner_: run tests, reports results; BYO https://www.destroyallsoftware.com/screencasts/catalog
* _harness_: testing framework https://stackoverflow.com/a/11628329/6813490

test types
* _unit test_: test on a method; runs in memory; some people consider smallest unit as including db https://calpaterson.com/against-database-teardown.html
* _integration test_: uses IO (fs, network), db, another app; two flavors (API-only, UI + API)
* _smoke test_: integration that tests something basic
* _regression test_: prod data
* _load testing_: send many requests at system https://github.com/Miserlou/NoDB https://news.ycombinator.com/item?id=23937256 https://github.com/nakabonne/ali https://github.com/locustio/locust https://github.com/fcsonline/drill https://github.com/hatoo/oha https://github.com/rednafi/stress-test-locust
* _fuzz_: provide random input, see what breaks https://labs.mwrinfosecurity.com/blog/what-the-fuzz/ https://www.fuzzingbook.org/ https://github.com/fuzzitdev/pythonfuzz https://dgraph.io/blog/post/continuous-fuzzing-with-go/ https://github.com/ffuf/ffuf randomize execution order https://github.com/pytest-dev/pytest-randomly https://github.com/google/atheris https://blog.burntsushi.net/projects/ https://github.com/ffuf/ffuf
* _mutation_: change src and see if tests detect https://blog.scottlogic.com/2017/09/25/mutation-testing.html https://rachelcarmena.github.io/2017/09/01/do-we-have-a-good-safety-net-to-change-this-legacy-code.html https://nedbatchelder.com/blog/201903/mutmut.html https://github.com/mutpy/mutpy
* _exhaustiveness_: https://news.ycombinator.com/item?id=25428583
* _property-based_: https://increment.com/testing/in-praise-of-property-based-testing/ https://datascience.blog.wzb.eu/2019/11/08/property-based-testing-for-scientific-code-in-python/ https://florian-dahlitz.de/blog/test-your-python-code-using-hypothesis https://www.youtube.com/playlist?list=PLP1DxoSC17LZTTzgfq0Dimkm6eWJQC9ki https://www.hillelwayne.com/post/property-testing-complex-inputs/ using API schemas https://www.youtube.com/watch?v=1lo7idI7uq8 https://github.com/schemathesis/schemathesis https://www.youtube.com/watch?v=uN6JjpzVsAo&list=PL2Uw4_HvXqvYk1Y5P8kryoyd83L_0Uk5K&index=71 https://nchammas.com/writing/how-not-to-die-hard-with-hypothesis
> If we have a function that operates on data and have a hard time figuring out what to test, hypothesis is a great library that can help. Rather than explicitly state the exact objects you want to run through a test, hypothesis generates examples of inputs that follow certain properties you define. https://www.peterbaumgartner.com/blog/testing-for-data-science/
> Testing-by-example (as opposed to property-based testing) is based on the programmer coming up with examples of inputs and asserting that when given those inputs the program produces the right outputs - or at least - the right sort of outputs. https://calpaterson.com/against-database-teardown.html
> At its simplest, property-based testing is the inverse of normal unit testing. Instead of providing some amount of data and a transformation so the computer can assert a property, you provide a property and a transformation, so the computer can provide some data. https://bytes.yingw787.com/posts/2021/02/02/property_based_testing/
```python
# unit testing - you provide the data
def test_addOne():
    assert addOne(5) == 6

# property testing - you just make the assertion
@given(st.integers())
def test_addOne(_input):
    assert addOne(_input) == _input + 1
```
