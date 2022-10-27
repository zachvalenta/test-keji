# TODO

## 参考

🔍
* https://serverfault.com/
* https://unix.stackexchange.com/
📚
* Evans linux
* Evans za
* Kerrisk lpi
* Stutz cookbook

## current

## next

* try and reorg file system according to `operations.md`

## done

* _22_: dev env
* _21_: macOS (failed upgrade to Big Sur)
* _19_: backups (Dropbox as placeholder until Tarsnap) macOS (upgrade to Mojave) 📙 `evans-random.pdf`
* _18_: phone (switch to new number, 'unknown number' problem, WhatsApp debacle)

# PACKAGING

🔍 https://repology.org/ https://github.com/ziglang/zig/wiki/Install-Zig-from-a-Package-Manager
🙂 https://xkcd.com/2347/

* os has to trust pkgs to a degree https://lwn.net/Articles/770784/ https://news.ycombinator.com/item?id=23678409
* not a solved problem and no consensus on how it should be solved https://news.ycombinator.com/item?id=24140848
* BYO https://nullprogram.com/blog/2018/03/27/
* tracking stats https://lwn.net/Articles/826216/
* never update anything if you can avoid it https://blog.kronis.dev/articles/never-update-anything

semantics
* _app_: runs on your box
* _executable_: runs on someone else's box
* _library_: used in someone else's app/executable/library
* less e.g. jQuery
* _framework_: lib + default methods called
* more e.g. React

CI
* _pipline stages_: fetch (clone from repo) build (install deps, compilation) test (run unit tests) deploy (put artifact somewhere so CD can pick it up and run it)
* _what not to build_: `.git`, dev deps
* _options_: hosted Git 🗄 `git.md` Jenkins https://itnext.io/jenkins-is-getting-old-2c98b3422f79 https://www.youtube.com/watch?v=WWcijE7ifcA BYO http://aosabook.org/en/500L/a-continuous-integration-system.html

binaries
* _management_: Artifactory, Nexus, Github Package Registry, Pulp https://pulpproject.org/ people also use these for language libraries and object stores as well https://devops.stackexchange.com/a/1900
```python
# upload
my_file = {"file": open(f"{file_name}", "rb")}
requests.put(artifactory_url, files=my_file, verify=False, auth=(user, pw))

# list archives in dir http://stackoverflow.com/a/55892053
requests.get(artifactory_url, verify=False, auth=(user, pw)).json()['children']
```
* _precompiled binary_: using what you've been given e.g. broot needs Rust as build dep, I don't have Rust, but I can still grab broot from Homebrew; downside is that in the app's build process, could be trying to run something sudo or trying to download one of its dependencies w/out verifying a checksum https://www.vitavonni.de/blog/201503/2015031201-the-sad-state-of-sysadmin-in-the-age-of-containers.html
* notarized binary: https://www.kencochrane.com/2020/08/01/build-and-sign-golang-binaries-for-macos-with-github-actions/
* _build from source_: can set compiler flags to optimize for your os (e.g. turn off debugging metrics so it runs faster) https://softwareengineering.stackexchange.com/a/167507 https://golang.org/doc/install#download
* containerized runtimes e.g. flatpak, Steam https://ludocode.com/blog/flatpak-is-not-the-future https://news.ycombinator.com/item?id=30408161

## build systems

📙 Meckleberg gnu make

Make
* docs: `gnu-make.pdf` https://www.gnu.org/software/make/manual/make.html https://tech.davis-hansson.com/p/make/ http://gromnitsky.users.sourceforge.net/articles/notes-for-new-make-users/ https://www.openmymind.net/An-Awful-Introduction-To-Make/ https://makefiletutorial.com/ https://daniel.feldroy.com/posts/autodocumenting-makefiles
* good for compilation https://www.youtube.com/watch?v=SdmYd5hJISM&lc=UgyBo0rkqGXZgLDmsRZ4AaABAg.9KU4gvKdDyN9KU9XbK1Cyl
* using shell script to handle more args https://www.youtube.com/watch?v=SdmYd5hJISM
* lot of blockers if you want it to work on Windows https://carolynvanslyck.com/blog/2021/01/mage-is-my-favorite-make/
* rules are run in separate shell https://stackoverflow.com/a/49621071
* control flow https://stackoverflow.com/a/14864888 https://stackoverflow.com/a/5553445 https://nullprogram.com/blog/2017/08/20/
* documentation at the level of the rule https://www.thapaliya.com/en/writings/well-documented-makefiles/ https://diamantidis.github.io/tips/2020/07/01/list-makefile-targets
* autocomplete https://stackoverflow.com/questions/4188324/bash-completion-of-makefile-target https://stackoverflow.com/questions/33760647/makefile-autocompletion-on-mac
* directories https://github.com/zachvalenta/query-sandbox
* _phony_: target that is name for a recipe vs. file name https://stackoverflow.com/a/3931814/6813490
* snippets
```makefile
#
# VARAIABLES
#

# reference env var https://stackoverflow.com/questions/28890634/how-to-get-a-shell-environment-variable-in-a-makefile
${var}

# args https://blog.mindlessness.life/2019/11/17/the-language-agnostic-all-purpose-incredible-makefile.html
env="dev"  # global
make deploy env=qa
deploy:
	echo $(env)

make bdd-dev,qa
bdd-%:
	poetry run behave --tags @${*}

#
# MISC
#

# syntax: whole thing called a rule (like CSS) http://gromnitsky.users.sourceforge.net/articles/notes-for-new-make-users/#4b6d995-adhere-to-the-common-terminology
target: prereq1 prereq2
    recipe

# points make to target (vs. file of same name) https://krzysztofzuraw.com/blog/2016/makefiles-in-python-projects.html
.PHONY

# combine rules https://stackoverflow.com/a/3519634
dummy: target1 target2

# ignore failure i.e. won't stop another recipe from running if it fails https://stackoverflow.com/a/53039783
ur-recipe:
    - rm $(file)

# hide cmd output https://stackoverflow.com/a/18105278
cmd:
    @poetry run pytest
```

taxonomy
* _build system_: build executables (esp. for C, C++)
* dependency graphs, build systems https://rhodesmill.org/brandon/slides/2021-06-colombia-remote/
* analyze dependency graph https://github.com/loov/goda
* or just a grab bag of commonly run commands https://en.wikipedia.org/wiki/List_of_build_automation_software
* aka task runner https://github.com/go-task/task
* _make_: run cmds together
* still awesome https://news.ycombinator.com/item?id=19900955
* better than Bash script bc more declarative, dep tree https://stackoverflow.com/a/3798664
* _cmake_: cross-platform buildfiles https://stackoverflow.com/a/25790020 http://aosabook.org/en/cmake.html
* _redo_: Make for the Linux nerd's Linux nerd https://fzakaria.com/2020/06/08/my-love-letter-to-redo.html
* _Bazel_: Make for FANG https://eng.uber.com/go-monorepo-bazel/ https://github.com/bazelbuild/bazel https://testdriven.io/blog/bazel-builds/ https://www.youtube.com/watch?v=zaymCO1A1dM
* others: https://taskfile.dev https://jvns.ca/blog/2020/10/26/ninja--a-simple-way-to-do-builds/ https://pypyr.io/ https://www.pantsbuild.org/ BYO http://aosabook.org/en/500L/contingent-a-fully-dynamic-build-system.html https://github.com/go-task/task
* Nx https://github.com/nrwl/nx

## dependencies

🗄
* `golang.md` packaging
* `python.md` packaging

> years ago websites were made of files; now they are made of dependencies https://alexdanco.com/2019/10/26/everything-is-amazing-but-nothing-is-ours/

* incl comment for each dep explaining need https://www.semicolonandsons.com/episode/The-Hidden-Costs-of-Software-Dependencies 13:15
* update lockfile periodically https://news.ycombinator.com/item?id=30578276

semver
* _patch_: update all patches w/out changing minor e.g. `~1.3.7` gets everything up to `1.4.0`
* _minor_: update all patch + minor w/out changing major e.g. `^1.3.7` gets everything up to `2.0.0` https://stackoverflow.com/a/22345808 
* definitions fuzzy e.g. what does "major" actually mean e.g. breaking change? for what percentage of users? https://gist.github.com/jashkenas/cbd2b088e20279ae2c8e https://snarky.ca/why-i-dont-like-semver/
* Golang brings into the realm of module/packges namespace (and therefore imports), meaning a version that is backwards incomptable must have a new namespace https://research.swtch.com/vgo-import https://news.ycombinator.com/item?id=16431299 🗄 `golang.md` 'semantic import versioning'
* contradictory interpretations? https://poetry.eustace.io/docs/basic-usage/#version-constraints https://docs.npmjs.com/about-semantic-versioning#using-semantic-versioning-to-specify-update-types-your-package-can-accept https://poetry.eustace.io/docs/versions/ https://research.swtch.com/deps

---

* dependabot for Python https://pyup.io/

> However. How can curl disappear? Curl is not just one of the most important dependencies, it's also one of the most resilient dependencies. When you or me install curl, we rarely install it from the official website. Curl is more likely to come from a mirror, vendored into a library we're using, there are a lot of forks in proprietary code bases etc. Curl is an unkillable dependency. Not only can the website go down, also the original developer could probably go away and someone would pick up the work, it's that useful. Let's contrast this for a second with the situation on npm...A few days ago the developer behind that library [colors] decided to release a new version of the library that no longer does what it advertised on the tin. Since it was a minor update quite a few people ended up with that version. They didn't however even know that they were depending on “that one package”, they probably pulled it in because something else in their dependency chain needed it. https://lucumr.pocoo.org/2022/1/10/dependency-risk-and-funding/

* _dependency resolution_: dep A and B both rely on pkg C, but they need different versions, what to do?
* _language dep ecosystem_: central pkg repo; each pkg w/ dependency manifest (`package.json`) lockfile (`poetry.lock`) and each version tagged according to semver https://blog.golang.org/versioning-proposal
* _determinism_: can pin version in human-readable file (`requirements.txt`) but then subject to library developers' interpretation of semver, whereas lockfile (`poetry.lock`) will give you exact build of dependency https://yarnpkg.com/blog/2017/05/31/determinism/ https://www.youtube.com/watch?v=wRHi8Ui5vWA
* _snapshot_: non-prod release https://stackoverflow.com/a/5901460/6813490
* _reproducible build_: attack vector in pkg distribution is discrepancy between src and artifact https://robertheaton.com/2018/11/17/reproducible-beliefs/ 🗄 `linux.md` Make
* _vendoring_: deps themselves under version control https://hacker-tools.github.io/package-management/ https://nullprogram.com/blog/2020/01/21/ protection against library disappearing, a bad push to master under the same version that you're using https://ukiahsmith.com/blog/a-gentle-introduction-to-golang-modules/
* _fat binary_: app has all dependencies packaged, to run successfully only needs a kernel (vs. anything in the user space)
* _pin_: get exact dependency versions https://pythonspeed.com/articles/reproducible-docker-builds-python/

problems
* failure modes: easy to impl what you need yourself, marginal improvement over built-in https://www.semicolonandsons.com/episode/The-Hidden-Costs-of-Software-Dependencies 5:00 if deps abandoned can always fork and use your own forks [ibid 5:15]
* _compatability matrix_: which version goes with which other version https://docs.docker.com/compose/compose-file/#compose-and-docker-compatibility-matrix
* _diamond dependency_: species of transitive dependency problem https://www.youtube.com/watch?v=8ng4v1g5q7s
* bleeds over in reproduciblity crisis https://www.youtube.com/watch?v=8ng4v1g5q7s
* _dep hell_: choosing one dep leads you to choosing related dependencies based on that and increases coupling https://www.semicolonandsons.com/episode/The-Hidden-Costs-of-Software-Dependencies 8:30
* _transitive_: dep A and B both depend on different versions of dep C
* _resolution_: figuring out subdepedencies for a dependency https://github.com/sdispater/mixology https://pyfound.blogspot.com/2020/03/new-pip-resolver-to-roll-out-this-year.html 
* _boolean satisfiability problem (SAT)_: dependency resolution, basically https://codingnest.com/modern-sat-solvers-fast-neat-underused-part-1-of-n/ NP complete https://en.wikipedia.org/wiki/Boolean_satisfiability_problem https://stackoverflow.com/a/9378268/6813490 used by Composer https://stackoverflow.com/q/37818396 https://news.ycombinator.com/item?id=14508546 https://jix.one/the-assembly-language-of-satisfiability/

## Homebrew

📜 https://docs.brew.sh/
🗄
* `application.md` TLS
* `python.md` version mgmt

* install: requires Xcode command line tools
* how to blow away everything?

---

info
* _list cmd_: `commands`
* _help for cmd_: `help <cmd>`
* _healthcheck_: `doctor`
* _search available_: `search`

dependencies
* _list installed - top level_: `leaves` https://apple.stackexchange.com/a/279078
* _list installed - transitive_: `ls` https://github.com/Homebrew/brew/issues/8257
* _pkg info_: `info <pkg>`
* _dependency graph_: `brew deps --tree --installed` https://apple.stackexchange.com/a/322371 https://github.com/martido/homebrew-graph

terms
* _formulae_: Ruby class that manages install; create your own https://www.youtube.com/watch?v=fbyrLo6yx8M
* _tap_: repo of formulae not maintained by Homebrew https://stackoverflow.com/a/37973017/6813490
* _bottle_: pre-compiled i.e. you don't need to download and build, just download i.e. faster
* _services_: integrates w/ MacOS launchctl to start program on OS boot

file system locations
* _Homebrew_: `/usr/local/Homebrew`
* _installs_: `/usr/local/Cellar` 🔗 `/usr/local/bin`
* installs deps just for building pkg https://github.com/Homebrew/brew/issues/634#issue-169347205

installation
* _install_: `install` curl to URL, compare download against checksum; `--prefix` (specific install location)
* _uninstall_: `uninstall`
* uninstall Homebrew itself https://github.com/homebrew/install#uninstall-homebrew
* _upgrade_: `upgrade`; there's another cmd `update`, akin to git fetch?
* _upgrade all outdate_: `brew outdated | xargs brew upgrade`

older versions
* _pin_: `pin` https://www.fernandomc.com/posts/brew-install-legacy-hugo-site-generator/
* _find older version_: look in homebrew core https://github.com/Homebrew/homebrew-core https://www.fernandomc.com/posts/brew-install-legacy-hugo-site-generator/ https://flaviocopes.com/homebrew-install-older-version/
> brew cleanup works against this
* _switch to different installed version_: `switch` https://github.com/thoughtbot/til/blob/master/homebrew/using_different_homebrew_formula_versions.md `link` does the same? https://stackoverflow.com/a/54175781

## managers

* _devbox_: isolate pkg by user/shell https://github.com/jetpack-io/devbox
* _whatis_: show description from manpage db https://github.com/Idnan/bash-guide#c-whereis
* man (UNIX) vs. info (GNU) https://askubuntu.com/a/9332 man pages for systems calls as well (`sendfile`) [`evans-linux.pdf` 11]
* help: `man`, `info`, `whatis`, `man 2 <cmd>` (for system calls)
* _man pages_: following links (like at bottom of cmus manpage) https://unix.stackexchange.com/a/18161/331460 set pager `export MANPAGER=bat` https://askubuntu.com/a/679058
* offline documentations https://devdocs.io/

apt
* _os that use_: Debian, Ubuntu, Mint
* _dpkg_: alternative that just installs pkg, not subdeps https://askubuntu.com/a/309121 list pkgs `dpkg-query -l`
```sh
# list installed
apt list -installed

# yes to interactive prompts
-y
export DEBIAN_FRONTEND=noninteractive

# update package listing so we know what packages exist
apt-get -y update

# grab security updates
apt-get -y upgrade

# ⚠️ sometimes have to update and upgrade or the package you're trying to donwload won't even be found
# install https://stackoverflow.com/a/50870967
RUN apt-get -y install <pkg>

# don't install subdeps (or does recommended here mean something else?) https://pythonspeed.com/articles/system-packages-docker/
apt-get -y install --no-install-recommends <pkg>

# clean up file cache https://pythonspeed.com/articles/system-packages-docker/
apt-get clean
rm -rf /var/lib/apt/lists/*
```

* _apk_: for Alpine
* _Snap_: Ubuntu thing https://lwn.net/Articles/825005/
* _lmod_: pkg + change env https://lmod.readthedocs.io/en/latest/ `module list` (what you have loaded) `module avail` (what you can load)
* _Nix_: https://pythonspeed.com/articles/reproducible-docker-builds-python/ https://news.ycombinator.com/item?id=23251754 https://github.com/NixOS/nix/issues/2925 https://news.ycombinator.com/item?id=30205848
> doesn't seem ready to supplant Homebrew yet https://github.com/NixOS/nix/issues/2925
* _rpm_: pkg format and, confusingly, pkg manager for RHEL https://stackoverflow.com/a/8201051/6813490
* _Tasksel_: install packages in bundled fashion (LAMP stack)
* _yum_: Red Hat (RHEL, Fedora)
* _Windows_: Chocolately, Nuget; uses Powershell under the hood

# PROCESSES

📙
* Arpaci ch. 13-23
* Kerrisk lpi 2.7
* Galvin dinosaur ch. 3-5

https://thorstenball.com/blog/2014/06/13/where-did-fork-go/
> Every process running on a Unix system started out as a call to fork(2) followed by a call to execve(2). Well, not every process, since the first process, the init process, the one that starts up the rest of the operating system, didn’t. But every process that came after. The idea is rather simple: fork(2) creates a new process and execve(2) turns the new process into the kind of process you want it to be.
> Let’s say you’re a shell and your user wants to start his productivity utility vimwonderhorse. Now, the first thing you’ve got to do is to start a new process. The reason for that is simple: when the user quits vimwonderhorse you should still be there and wait for the user’s input again. If you, as the shell, would have changed into vimwonderhorse and the user quit, well, then you would be gone, too. So you start a new process with fork(2).

semantics
* _thread_: instance of executing program; components incl stack, heap, text (src) data (var)
* _process_: group of threads https://stackoverflow.com/a/47824267 [LPI 2.7]
* _job_: group of processes [LPI 2.13]

types
* _privileged_: any process started by root
* _single-threaded_: program in single thread, IO in separate threads e.g. JS [`go-in-practice.pdf` 1.3.4]
* _multi-threaded_: program in n threads
* _daemon_: long-running background process; no controlling terminal [LPI 34]

segments [LPI 31]
* _text_: program source code in machine-code form; read-only so process can't modify [LPI 6.115]
* _data_: static variables (won't change so thread-safe) [LPI 6.116]
> less sure about this definition
* _stack_: 🗄 `architecture.md` memory
* _heap_: 🗄 `architecture.md` memory

creation
* `fork()`: called by existing process (parent) to create new process (child), which is a duplicate [LPI 2.7 31]
* inheritance: child process shares read-only access to parent's program data and gets copy of parent's get data, stack, heap [LPI 2.7 32]
* `execve()`: syscall to load new program, which destroys parental segments [LPI 2.7 32] user-space wrappers incl `execv`, `execle` https://en.wikipedia.org/wiki/Exec_(system_call)#Nomenclature

---

* https://sirupsen.com/progress
* each program executed by the shell starts a new process [LPI 2.13]
* _location_: $CWD of their parent process [LPI 2.5]
* _initial process_: PID 1, called `init` (or `systemd` on RHEL) [LPI 2.7]
* _inheritance_: process created when parent calls `fork()`; child inherits UID/GID and stack, heap, data [LPI 2.7]
* `execute()`: child gets their own stack, heap, data [LPI 2.7] 
* _termination_: process calls `exit()` or killed by a signal [LPI 2.7] if parent process killed transitively kill child process

communcation
* _signals_: restart `-HUP/-1` terminate (sent to process) `-TERM/-15` terminate/sigterm (sent to kernel) `kill -KILL/-9 <pid>`
* _intra-process communication (IPC)_: signals, writing to disk (for slow apps), file locking, pipes, message queues 📙 Kerrisk 37, 877

memory
* _hard limit_: inherited from parent
* _soft limit_: can be set by user [LPI 2.7]
* _load average_: CPU capacity to deal w/ processes; view w/ `uptime`; 1.0 is perfect capacity but anything above 0.70 should be investigated bc otherwise won't have any headroom for increases https://scoutapm.com/blog/understanding-load-averages
* _OOM killer (out-of-memory)_: https://unix.stackexchange.com/q/153585/331460 https://serverfault.com/a/571326/415712 https://lwn.net/Articles/391222/

telemetry
* _commands_: `uptime`, `top`
* _debug_: strace, application logs 
* _PID_: process ID; written to file https://stackoverflow.com/a/8296204/6813490 lookup PID using process name https://stackoverflow.com/a/11547409/6813490
* _PPID_: parent process ID
* `lsof`: open files https://danielmiessler.com/study/lsof/ GUI https://github.com/sveinbjornt/Sloth
* _PID by port_: `lsof -i :<port>`
* _$CWD by PID_: `lsof -p <PID> | grep cwd` https://unix.stackexchange.com/a/94359/331460
* `pstree`: tree of processes

* pgrep https://www.freecodecamp.org/news/fzf-a-command-line-fuzzy-finder-missing-demo-a7de312403ff/
* procs: ps replacment in Rust https://github.com/dalance/procs
* `ps`: processes associated with current shell
* pgrep https://hacker-tools.github.io/shell/
* `ps -u`: associated with specific user
* `ps -e`: associated with all users
* `ps -f`: info on PPID
* `ps -ejH`: show trees

## threads

🔍 https://softwareengineering.stackexchange.com/questions/tagged/concurrency
📚
* Arpaci ch. 26-33
* Bryant ch. 12

basics
* _concurrency_: design tasks that can be independently executed
* best for network-bound tasks e.g. callbacks, task queue
* aka async
* _parallelism_: execute tasks simultaneously
* best for CPU/IO-bound tasks
* aka multi-threading

problems 📙 Galvin chapters 5/7 Tanenbaum chapter 6
* _deadlock_: waiting
* i.e. each thread thinks the other is using resource, causing each to 1) not use resource 2) wait indefinitely for other thread to "stop" using resource
* _livelock_: hallway problem
* i.e. each thread constantly changing to resolve lock but making no progress (the hallway example)
* _race condition_: sequence of events screws up correctness
* vs. data race https://stackoverflow.com/a/18049303 https://www.avanderlee.com/swift/race-condition-vs-data-race/ https://blog.regehr.org/archives/490
> knock knock / race condition / who's there? https://twitter.com/iamdevloper/status/399991896862638081
* _thread safety_: threads don't overwrite data from other threads

storage problems
* _split brain_: data inconsistencies https://en.wikipedia.org/wiki/Split-brain
* e.g. two application instances write to database and search index such that each reads their own value from index 📙 Kleppmann 491/453
* solutions is either serve inconsistencies or serve old results until system heals
* _segmentation fault_: process tries to use inaccessible memory https://corecursive.com/066-sqlite-with-richard-hipp/

---

* _copy on write_: processes share memory until they need to write, at which point make copy of memory section and write to it (thereby avoiding a page fault) 🗄 `evans-linux.pdf` [3] https://brandur.org/ruby-memory
* _mutex_: OS version of a lock https://jvns.ca/blog/2016/01/23/sendfile-a-new-to-me-system-call/ https://lwn.net/Articles/827180/ https://mortoray.com/2019/02/20/how-does-a-mutex-work-what-does-it-cost/
* _serial_: execution inside single thread https://pre-commit.com/#hooks-require_serial
* _history_: end of Moore's Law (clock speed increases slowing) = more cores per machine = more parallelization [Kleppmann 6]
* _actor model_: concurrency w/in single process [Kleppmann 4.138] https://news.ycombinator.com/item?id=27505267
* polling/blocking https://drewdevault.com/2019/03/25/Rust-is-not-a-good-C-replacement.html https://cs61.seas.harvard.edu/site/2018/Shell3/ https://en.wikipedia.org/wiki/Polling_(computer_science)

## tracing

🗄
* processes
* `python.md` profiling
* `system.md` monitoring
📚
* Evans debug tools
* Evans perf
* Evans strace
* Evans tracing

vocab
* _monitor_: continuous; track errors
* _trace_: ad-hoc; explore errors
* _profile_: ad-hoc; hunt optimization

---

* strace, ptrace https://nullprogram.com/blog/2018/06/23/
* magic trace https://github.com/janestreet/magic-trace
* ptrace https://medium.com/@lizrice/a-debugger-from-scratch-part-1-7f55417bc85f
* strace https://jvns.ca/blog/2021/04/03/what-problems-do-people-solve-with-strace/
* dtruss https://blog.safia.rocks/post/173241985600/unraveling-rm-what-happens-when-you-run-it

❌ normal debugging: know the language, look at src, print statements/debugger
✅ `strace` debugging: 'these are the system calls your program is making'
📝 don't run strace on production processes (or anything that needs to run at normal speed)

# ZA

* sysadmins https://xkcd.com/705/
> Somewhere there’s a database programmer surrounded by empty Mountain Dew bottles whose husband thinks she’s dead. And if these people stop, the world burns. Most people don’t even know what sysadmins do, but trust me, if they all took a lunch break at the same time they wouldn’t make it to the deli before you ran out of bullets protecting your canned goods from roving bands of mutants. http://www.stilldrinking.org/programming-sucks
* trash: https://github.com/andreafrancia/trash-cli recover deleted files https://sabotage-linux.github.io/blog/6/ alternative to rm https://github.com/alanzchen/rm-protection
* _tar_: work w/ compressed files
* extract `-xf`
* compress w/ gzip `.tar.gz`
* aunpack/atoo https://hacker-tools.github.io/command-line/
* _line termination_: delimiter for end of line
* NL on *nix, CRLF on Windows https://stackoverflow.com/a/12747850/6813490
* sockets 📙 Bryant (11)

logging
* `syslog`: daemon that ingests logs and routes to log files
* `/var/log`: storage location
* viewer https://lnav.org/
* `journalctl`: view systemd and kernel logs https://hacker-tools.github.io/machine-introspection/

ports 🗄 `tcp-ip.md` packet
* _hosts file_: `/etc/hosts`; map of domains to IP addresses
* _privileged_: ports < 1024 are privileged and can only be bound to processes running as root
* _port knocking_: https://news.ycombinator.com/item?id=23187662
* _netstat_: check if port open https://askubuntu.com/a/224396 https://serverfault.com/a/309058 macOS has different flags https://www.lifewire.com/using-netstat-command-on-mac-4176069

Raspberry Pi
* use for Funkwhale
* https://uglyduck.ca/my-pi-desktop/
* https://news.ycombinator.com/item?id=24965614
* https://www.canakit.com/raspberry-pi-4-8gb.html
* https://www.jeffgeerling.com/project/raspberry-pi-dramble
* https://www.jeffgeerling.com/blog/2020/i-replaced-my-macbook-pro-raspberry-pi-4-8gb-day
* desktop https://www.raspberrypi.org/products/raspberry-pi-4-desktop-kit/

daemons
* _systemd_: manage daemons https://opensource.com/article/20/4/systemd
* https://github.com/torfsen/python-systemd-tutorial
* https://systemd-by-example.com/
* can conf service to start on boot, restart if crashes https://www.reddit.com/r/Ubuntu/comments/7j5qgj/gunicorn_daemon_vs_gunicornservice_on_ubuntu_1604/
* preceded by Upstart https://www.digitalocean.com/community/tutorials/how-to-serve-flask-applications-with-uwsgi-and-nginx-on-ubuntu-14-04 https://christine.website/talks/systemd-the-good-parts-2021-05-16 https://unixsheikh.com/articles/systemd-isnt-safe-to-run-anywhere.html
> To configure services, you pretty much have to interact with systemd these days, for better or for worse. Most services on your system will have a systemd service file that defines a systemd unit. These files define what command to run when that services is started, how to stop it, where to log things, etc. They’re usually not too bad to read, and you can find most of them in /usr/lib/systemd/system/. You can also define your own in /etc/systemd/system . Once you have a systemd service in mind, you use the systemctl command to interact with it. systemctl enable UNIT will set the service to start on boot (disable removes it again), and start, stop, and restart will do what you expect. If something goes wrong, systemd will let you know, and you can use journalctl -u UNIT to see the application’s log. You can also use systemctl status to see how all your system services are doing. If your boot feels slow, it’s probably due to a couple of slow services, and you can use systemd-analyze (try it with blame) to figure out which ones. https://hacker-tools.github.io/machine-introspection/

boot
* _bootloader_: loads os e.g. GRUB
* _BIOS_: first step when powering on i.e. before bootloader
* boot https://utcc.utoronto.ca/~cks/space/blog/linux/LinuxBootOverview?

man pages
* Visidata handles this well
* run by Michael Kerrisk https://man7.org/tlpi/faq/index.html#many_errata https://www.kernel.org/doc/man-pages/
* why do they look so much worse in the terminal? https://man7.org/linux/man-pages/man1/bash.1.html 🗄 `shell.md` bat
* colorize https://danyspin97.org/blog/colorize-your-cli/
* with bat https://github.com/sharkdp/bat#man https://github.com/eth-p/bat-extras
* how to make one for your own program: https://github.com/bootandy/dust/issues/45 https://github.com/sharkdp/bat/blob/master/assets/manual/bat.1.in https://github.com/Canop/broot/blob/master/man/page `man bat -w` https://unix.stackexchange.com/a/6892/331460 http://www.tldp.org/HOWTO/Man-Page/

## denv

🗄 `km.md` file system

```sh
├── /Users/zach/Documents/materials/stem/dev/os/denv
│   └── bin
│   └──────── fr
│   └──────── jb
│   └──────── jbc
│   └──────── kcm
│   └──────── m2h  # symlink to Python repo
│   └──────── qing # symlink to Python repo
│   └──────── this-week
│   └──────── upper-structures
│   └──────── vimv
│   └── dotfiles  # mv pkg to logs
│   └──────── db  # psqlrc, sqliterc, visidatarc, litecli.conf, pgcli.conf
│   └──────── editors  # vimrc, settings, keybindings, markdown
│   └──────── poetry  # pdb, Poetry
│   └──────── shell  # bash/zh (profile, rc), powerline/starship/git-prompt
│   └── fonts
│   └──────── fira-mono-regular.otf
│   └──────── fira-mono-regular-windows-compatible.otf
│   └── logs
│   └──────── brew
│   └──────── nodenv
│   └──────── pip
│   └──────── pipx
│   └──────── pyenv
│   └──────── za
```

shell utils 🗄 `shell.md`
* file find: fd
* file explorer: broot
* file list: exa
* pager: bat
* text search: ripgrep
* git: diff-so-fancy, tig
* prompt: powerline-shell (pipx)
* sql/munge: csv, miller, visidata (pipx)
* Python: black, flake8, poetry (pipx)

## distros

📙
* Galvin dinosaur 18-20
* Kerrisk 1

* non-C operating systems e.g. SerenityOS https://news.ycombinator.com/item?id=30851955
* _DOS (disk os)_: os that came after punch cards and magnetic drums i.e. computers 1980s to mid 90s
* _Plan9_: os from Bell Labs after UNIX https://seh.dev/go-legacy/
* [Rob Pike talk](https://www.youtube.com/watch?v=_2NI6t2r_Hs&t=1105s)
* The Open Group, an industry consortium (IBM Huawei DoD) controls UNIX name and compliance; no Linux distro qualifies [LPI 1, 1.3.3, 1.3.8]
* how to keep Linux distros consistent? The Linux Standard Base [LPI 1.3.8]
* _distros_: Ubuntu (default) Debian (tricky config) Red Hat (Enterprise, Fedora, CentOS and fork https://changelog.com/podcast/427) Kali (security) Arch, Mint (personal) Raspian (IoT) Alpine (lightweight) https://distrochooser.de/ https://news.ycombinator.com/item?id=23816007 https://news.ycombinator.com/item?id=16315087
* _Linux Foundation_: sponsors Linux, Cloud Foundry, Cloud Native Computing Foundation (which itself maintains Kubernetes) 
* OpenBSD https://unixsheikh.com/articles/openbsd-6.9-has-been-released-kudos-to-all-involved.html
* _Unices_: enterprise (Unix, Solaris) open (BSD, Linux) BSD doesn't do bluetooth https://news.ycombinator.com/item?id=25949784
* BSD: http://eradman.com/posts/openbsd-workstation.html
* _Nix_: https://news.ycombinator.com/item?id=31557430

history
* _1969_: Unix (Bell Labs; Ken Thompson)
* _1975_: Sixth Edition, first to be used widely outside AT&T [LPI 1.1]
* _1979_: Seventh Edition; awk, sed, tar, Bourne shell [LPI 1.1]
* _1979_: BSD (Ken Thompson); TCP/IP implementation, sockets API
* _1983_: Sun OS (based off BSD), followed up Solaris
* _1983_: System V proceeds from AT&T breakup https://danielmiessler.com/blog/the-differences-between-bsd-and-system-v-unix/
* _1984_: macOS; similar to FreeBSD https://wiki.freebsd.org/Myths http://www.paulgraham.com/mac.html
* _1985_: Stallman starts GNU and FSF, by early 90s has OS sans kernel
* _1993_: Novell acquires UNIX from AT&T
* _1994_: Linux 1.0 released
* _1995_: Debian; buster (current LTS) stretch, slim (previous) https://wiki.debian.org/DebianReleases#Production_Releases
* _2000_: RHEL
* _2004_: Ubuntu (Canonical is company behind it)
* _2011_: Elementary https://news.ycombinator.com/item?id=26658317

## file system

📙 Galvin dinosaur 11-13

file descriptors
* _file descriptor_: reference to file created when os opens file so that your program can do stuff w/out touching underlying file directly
* akin to Vim buffer
* useful for passing between processes https://jeffknupp.com/blog/2016/03/07/python-with-context-managers/ 
* _0_: stdin
* _1_: stdout
* _2_: stderr
* _&_: both stdout and stderr https://askubuntu.com/a/350216
* also way to mark file descriptor e.g. `2>&1` = "redirect file descriptor 2(stdout) to file descriptor 1" (without `&1` the redirect would assume a file named `1`)  https://askubuntu.com/a/350216 https://stackoverflow.com/a/818284

links
* _symlink_: file pointing to source file
* commands pass through to source file
* deleting soft link doesn’t affect source
* file w/ the name/path to another file in it 📙 `evans-linux.pdf` 4
* syntax: `ln -sf /path/to/source /path/to/link`
* `-f`: overwrite if file already exists at location
* _hard link_: file pointing to inode
* still works if original deleted (不明觉厉) https://hacker-tools.github.io/backups/
* doesn't take up file space https://www.lifewire.com/create-symbolic-links-ln-command-4059723

za
* file name sorting https://rhodesmill.org/brandon/slides/2021-06-colombia-remote/
* trailing slash in path https://tookmund.com/2022/04/importance-of-the-trailing-slash

---

* https://www.youtube.com/watch?v=HbgzrKJvDRw
* file metadata vs. xattrs https://the.exa.website/features/xattrs

* https://news.ycombinator.com/item?id=29164727
https://www.youtube.com/watch?v=Ftg8fjY_YWU 3:40
https://www.youtube.com/watch?v=dDwXnB6XeiA
https://fasterthanli.me/series/reading-files-the-hard-way
* the kids don't even know what directories are https://www.theverge.com/22684730/students-file-folder-directory-structure-education-gen-z
* _XDG base directory specification_: put config files in `/config` https://0x46.net/thoughts/2019/02/01/dotfile-madness/
* _inode_: file ID; ‘index node’ https://wizardzines.com/comics/inodes/
* `/var`: for [variable data files](https://unix.stackexchange.com/a/264345)

locations
* `~/.config`: config for CLIs (http-prompt, wireshark)
* `/tmp`: can be either stored on disk or using tmpfs
* `/dev/shm`: alternative to `/tmp` https://superuser.com/a/45509 https://pythonspeed.com/articles/gunicorn-in-docker/
* `/dev/null`: special file for redirecting stuff you don't care about e.g. stderr `rm FILE 2> /dev/null` https://askubuntu.com/a/12099
* _tmpfs_: looks like storage but is actually memory https://docs.gunicorn.org/en/stable/faq.html#how-do-i-avoid-gunicorn-excessively-blocking-in-os-fchmod
* _FHS_: standard for where things should be located on Linux [‘Practical Guide to Linux Commands’ pg. 12] https://apple.stackexchange.com/a/119265/328389 https://www.youtube.com/watch?v=FSxab6etkzg
* _Mac_: `/private/tmp` = 类似 Linux var/tmp, kinda https://apple.stackexchange.com/a/131080 `/usr/local` Homebrew, git, go `/Library` (SDKs) `/System/Library/Frameworks` (binaries)
* _Linux_: `var`/`tmp` temp files `/etc` (settings files, third-party installs) [Clinton 'Linux in Action' 30] `/mnt` (additional volumes) [Sweigert Automate the Boring Stuff chapter 8]
* throw away stdout: `2>/dev/null` https://askubuntu.com/q/350208
* `/dev/null`: black hole `rm local.db 2> /dev/null; sqlite3 local.db < schema.sql`
📝 [`/dev/null`](https://askubuntu.com/a/12099) special file for dumping this sort of thing

files
* _file_: sequence of bytes https://netflixtechblog.com/building-netflixs-distributed-tracing-infrastructure-bb856c319304
* _file handle_: https://stackoverflow.com/a/3385261/6813490 https://danluu.com/file-consistency/
* _file path_: absolute (from root) relative (to CWD)
* _node_: ❓ file, pipe, other stuff c.f. `os.mkdnod()`
* _socket_: type of file that enables communications https://www.youtube.com/watch?v=Lbfe3-v7yE0 figure out how it works with Postgres
* _link_: how file is known by file system i.e. possible to have a file unlinked from file system and therefore cannot be opened by other programs https://pymotw.com/2/tempfile/
* rm broken https://github.com/sahib/rmlint

file system
* _file system_: mapping from file name to file contents i.e abstraction of persistent storage hw [Think OS chapter 4 intro]; way to represent data from hard disk to os; doesn’t seem like os is responsible for creation of the file system [LPI 1.2.2]
* non-POSIX https://weinholt.se/articles/non-posix-filesystems/
* IPFS https://www.youtube.com/watch?v=5Uj6uR3fp-U https://macwright.com/2017/08/09/decentralize-ipfs.html https://austinvernon.eth.link/blog/ipfsbasics.html https://austinvernon.eth.link/blog/ipfscodeexample.html
* BYO https://blog.carlosgaldino.com/writing-a-file-system-from-scratch-in-rust.html
* _exFAT_: MS fs for external HD https://superuser.com/q/1292689
* _mount_: 名 (files accessible to OS) 动 (make file system accessible to OS) `df` disk free on mounts https://www.youtube.com/watch?v=gZUVaPPFBJY
* _design_: Linux (single hierarchical dir structure) vs. Windows (each disk has own dir structure) [LPI 27] most operating systems support several types of file systems
* _impl_: NTFS (Windows) EXT, FAT (Linux) HFS+ (Mac) [Think OS 4.2]
* new ones: https://lwn.net/Articles/824855/
* _journal_: ledger of action
* written to before action taken
* in event of power outage can just restart from the journal
* _file metadata_: name, type, size, location, timestamps (create, access, modify)
* _virtual file system_: https://github.com/jedevc https://stackoverflow.com/questions/2910229/what-is-a-virtual-file-system-or-a-file-system-in-userspace https://github.com/rianhunter/dbxfs
* _NFS (network file system)_: access files over network as if they were on local storage; uses ONC protocol https://en.wikipedia.org/wiki/Network_File_System https://git-scm.com/book/en/v2/Git-on-the-Server-The-Protocols
* _timestamps_: access (file opened) modify (contents of file edited) change (inode modified i.e. permissions) https://unix.stackexchange.com/a/132661/240456
* _file corruption_: see if things are weird `cat -v` fix w/ `dos2unix`
* _alternate data stream_: hidden data embedded in file; similar to extended attributes in EXT https://www.youtube.com/watch?v=rF4sIxDIhEk
* _Autopsy_: forensics tool for Windows * forensics https://news.ycombinator.com/item?id=26271735

## kernel

🗄 `languages.md` 'C'

🔍 https://livegrep.com/search/linux

📦 https://git.kernel.org/

* _info_: `sysctl -n hw.ncpu` (number of cores) should be file `/etc/<distro>-release` (although of course not on macOS)
* _user space_: shell, user processes
* _kernel space_: stuff kernel controls
* _components_: https://makelinux.github.io/kernel/map/
* _things kernel does_: talks to cpu, mem, disk, network e.g. keyboard interrupt to figure out which key you type, knows you have HD and how to write to it, schedules procceses https://jvns.ca/blog/2013/10/02/day-3-what-does-the-linux-kernel-even-do/
* _driver_: kernel module for managing hardware device
* BYO https://s-matyukevich.github.io/raspberry-pi-os/
* kernel message logs https://zaiste.net/posts/shell-commands-rust/#rmesg
* _sink_: https://softwareengineeringdaily.com/2019/03/14/linux-kernel-development-with-shuah-khan/

system calls
* aka syscall
* https://blog.cerebralab.com/If_I_were_to_select_the_worst_Linux_syscall
* API for kernel space e.g. create file, spawn process http://thevivekpandey.github.io/posts/2017-09-25-linux-system-calls.html
* actually pretty tricky, hence most common sys calls being wrapped by glibc
> Why does glibc do that? Why call clone(2) instead of fork(2)? And why does it wrap system calls in library functions? After digging around a bit I found out that making a system call is actually harder than just calling fork() somewhere in my code. I’d need to know the unique number of system call I was about to make, set up registers, call a special instruction (which varies on different machine architectures) to switch to kernel mode and then handle the results when I’m back in user space. By providing a wrapper around certain system calls glibc makes it a lot easier and portable for developers to use system calls. There is still the possibility to use syscall(2) to call system calls somewhat more directly. - https://thorstenball.com/blog/2014/06/13/where-did-fork-go/

## users / groups

🔗 https://jvns.ca/blog/2017/11/20/groups/

users
* _UID_: user id; `root` is 0
* _GID_: group id
* logged in: `w`
* many programs create username and perform operations as that user
* macOS root user disabled by default but admin users can enable
* all logged in users: `who`
* switch user: `su <user>`; for root `su -`
* create user: `adduser` 
* give user sudo privilege: `visudo` (I think just opens `/etc/sudoers`)

groups
* _GID_: group ID 
* groups for user: `groups <user>` (or just `groups` for yourself)
* `wheel`: users who can `sudo` https://en.wikipedia.org/wiki/Wheel_(computing) 📘
* `/etc/group`: lists group name, pass, GID, users in group [LPI 26]

permissions 🗄 `installs/terraform/tf-path.log`
* _categories_: u (user/owner) g (group) o (other) a (all)
* _alphabetic notation_: `chmod o=rwx` (all perms to other) `chmod +x` (singl perm to all) `chmod o+x` (add perm) `chmod o-x` (rm perm) https://www.guru99.com/file-permissions.html
* _octal_: actually binary! [`evans-linux.pdf` 16]
* _default_: 666 (file) 755 (dir)
* _unmask_: adjust default permissions https://www.digitalocean.com/community/tutorials/linux-permissions-basics-and-how-to-use-umask-on-a-vps
* read/write/execute have slightly different meanings when applied to directories [LPI 2.5]
* https://blog.lizzie.io/linux-containers-in-500-loc.html
