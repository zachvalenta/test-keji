# TODO

## 参考

📜 https://golang.org/doc/effective_go.html

## current

## queue

* project structure for CLI and testing https://github.com/quii/learn-go-with-tests https://eli.thegreenplace.net/2022/file-driven-testing-in-go/ https://sourcegraph.com/notebooks/Tm90ZWJvb2s6MTM2Nw==
* https://lets-go.alexedwards.net/
* https://pocketbase.io/

## done

* _20_: research packaging
* _19_: version mgmt (uninstall macOS pkg, reinstall `go` and `dep` w/ brew)
* _17_: PluralSight course w/ Roberto and Josh

# LANG

🔗 https://gist.github.com/prologic/5f6afe9c1b98016ca278f4d507e65510
📜 The Go Programming Language

* is not easy https://www.arp242.net/go-easy.html
* https://golang.design/history/
* lodash https://github.com/samber/lo
* dates https://www.digitalocean.com/community/tutorials/how-to-use-dates-and-times-in-go
* _case_: uppercase (available on import) lower (unavailable on import)
* _design_: no exceptions, user-defined inheritance https://www.capitalone.com/tech/software-engineering/go-is-boring/ have to build API yourself https://www.arp242.net/go-easy.html https://drewdevault.com/2021/04/02/Go-is-a-great-language.html
> More concisely, I think of Go as an "internet programming language", distinct from the systems programming languages that inspired it. Its design shines especially in this context, but its value-add is less pronounced for other tasks in the systems programming domain - compilers, operating systems, etc https://drewdevault.com/2021/02/21/On-the-traits-of-good-replacements.html
* _error handling_: https://benhoyt.com/writings/go-intro/ https://dev.to/web3coach/how-to-handle-errors-in-go-5-rules-2bgf https://rauljordan.com/2020/07/06/why-go-error-handling-is-awesome.html https://github.com/kisielk/errcheck
* _generics_: https://blog.golang.org/generics-next-step
* _types_: bool string int (+ specific types) no type hierarchy [Go in Action 1.1.3]

alias import
```golang
import (
    "rsc.io/quote"
    quoteV3 "rsc.io/quote/v3"
)
```

JSON 
* https://www.youtube.com/watch?v=Osm5SCw6gPU https://akrabat.com/converting-json-to-a-struct-in-go/ https://eli.thegreenplace.net/2020/representing-json-structures-in-go/ https://www.youtube.com/watch?v=52yMK6p_cAg 
* generate struct from JSON https://mholt.github.io/json-to-go/
* default values https://github.com/creasty/defaults
```golang
type Book struct {
    Title string `json: "title"`
    Author string `json: "author"`
}
```

## concurrency

* vs. concurrency in other languages https://eli.thegreenplace.net/2018/go-hits-the-concurrency-nail-right-on-the-head/
* http://www.doxsey.net/blog/go-concurrency-from-the-ground-up https://rcoh.me/posts/why-you-can-have-a-million-go-routines-but-only-1000-java-threads/ https://utcc.utoronto.ca/~cks/space/blog/programming/GoConcurrencyStillNotEasy https://divan.dev/posts/go_concurrency_visualize/

* _goroutines_: abstraction on top of threads [Poulton 11.4] scheduled by Go runtime instead of OS [ibid @ 0:50] KB vs. 1MB for OS thread [ibid @ 1:10]
* _channels_: communication between go routines [‘Go in Action’ 1.1.2]
* _deadlocks_: https://medium.com/a-journey-with-go/go-how-are-deadlocks-triggered-2305504ac019
* `defer`: execute after surrounding code block returns
```golang
func main() {
	defer fmt.Println("world")
	fmt.Println("hello")
}
```

## collections

* container pkg: list, ring, heap https://therebelsource.com/blog/exploring-container-package-in-go-list-ring-and-heap/9zTBiMaaYg
* _map_: map/dictionary 🗄 `algos.md` https://tour.golang.org/moretypes/22
* _struct_: user-defined type
```golang
// declare (type Book or type struct?)
type Book struct {
    Title string
    Author string
}
// init
book := Book{Title: "Go in Action", Author: "William Kennedy"}
```

* _slice_: resizable; doesn't store array data, but manipulating alters underlying array https://www.openmymind.net/The-Minimum-You-Need-To-Know-About-Arrays-And-Slices-In-Go/
```go
[]bool{true, true, false}  // build array and slice on top all in one go w/ slice literal
// https://tour.golang.org/moretypes/10 --> same syntax as Python
// https://tour.golang.org/moretypes/11 --> length (slice) capacity (length of underlying array)
// https://tour.golang.org/moretypes/16 --> range to loop over slice and get index and value
```

* _array_: fixed size
```go
primes := [6]int{2, 3, 5, 7, 11, 13}
fmt.Println(primes[4]) // 11
mySlice := primes[1:4]
fmt.Println(mySlice) // [3 5 7]
```

## functions

* _naked returns_: return all; don't use for longer functions https://tour.golang.org/basics/7
capitalize function sig to export from package, type-id order in Golang/Python vs. C/Java https://blog.golang.org/gos-declaration-syntax

```go
// basic
func add(x int, y int) int {
    return x + y
}

// omit redundant type info
func add(x, y int) int {
    return x + y
}

// return n items
func swap(x, y string) (string, string) {
    return y, x
}

// naked return returns named values
func multi(num int) (x, y int) {
    x = num + 2  // this doesn't count as a short declaration bc x,y are params
    y = num * 2
    return
}
```

## project structure

https://github.com/mikestefanello/pagoda
https://autostrada.dev/

https://eli.thegreenplace.net/2019/simple-go-project-layout-with-modules/ https://github.com/golang-standards/project-layout/issues/117 https://github.com/golang/go/issues/45861
https://christine.website/blog/within-go-repo-layout-2020-09-07 https://github.com/golang-standards/project-layout https://commandercoriander.net/blog/2017/12/31/writing-go/ https://eli.thegreenplace.net/2019/simple-go-project-layout-with-modules/ https://bencane.com/stories/2020/07/06/how-i-structure-go-packages/#/3 simple https://github.com/healeycodes/conways-game-of-life  https://bencane.com/2020/12/29/how-to-structure-a-golang-cli-project/ https://adhoc.team/2021/03/29/simple-web-app-in-golang/

```sh
# MAIN
├── cmd/  #  python my_script.py
├── internal/  #  _internal 
├── pkg/  #  code that code also be used by other projects; 类似 Django app https://commandercoriander.net/blog/2017/12/31/writing-go/
├── vendor/  #  venv

# ANCILLARY
├── api/  #  Swagger
├── build/  #  Dockerfile, .gitlab-conf.yaml
├── config/  #  conf files I guess
├── init/  #  systemd
├── web/  #   js
```

## variables

📝 in Go docs, 'declaration' either means 'declaration' or 'initialization' 😞

* _long initialization_: `var myVar int = ` https://tour.golang.org/basics/8
* _short declaration_: `myVar := 42`; declaration + assignment; only at function scope https://tour.golang.org/basics/10

* _assignment_ https://tour.golang.org/basics/7
```golang
func multi(num int) (x, y int) {
    x = num + 2  // ❓ not short declaration bc x,y are params i.e. already declared
    y = num * 2
    return
}
```

* _zero values_: aka default assignment; lead to bugs https://news.ycombinator.com/item?id=20266747
```golang
var myBool // false
var myString // ""
var myInt // 0
```

# USES

## CLI

Bubble Tea https://www.youtube.com/watch?v=ZA93qgdLUzM

visual
* _games_: https://ebiten.org/
* _GUI_: https://github.com/AllenDang/giu https://github.com/fyne-io/fyne
* _TUI_: https://github.com/jroimartin/gocui https://github.com/rivo/tview/ https://github.com/charmbracelet/bubbletea https://github.com/charmbracelet/bubbles https://github.com/fatih/color prompt https://github.com/manifoldco/promptui https://news.ycombinator.com/item?id=32331367 https://news.ycombinator.com/item?id=32333290
* _visualization_: https://github.com/go-echarts/go-echarts

project structure
* start here https://blog.ultirequiem.com/chigo#heading-starting-the-project
```sh
mkdir chigo
go mod init github.com/UltiRequiem/chigo
mkdir internal pkg cmd
touch pkg/root.go internal/root.go cmd/root.go
tree
├── cmd        # main
│   └── root.go
├── go.mod
├── internal   # business logic
│   └── root.go
└── pkg        # util
    └── root.go
```
```golang
// sketch of pkg

from "internal" import printFromStdin, printWithColors

help, fileArguments, files = parametersAndFlags()

if help {
   printHelp()
   exit()
}

if fileArguments {
   filesText = joinFiles(files)
   printWitColors(filesText)
   exit()
}

printFromStdin()
```
```golang
// take list of files and get text from them
package internal

import "os"

func JoinFiles(files []string) (string, error) {
    text := ""

    for _, file := range files {
        fileText, err := os.ReadFile(file)

        if err != nil {
            return "", err
        }

        text += string(fileText) + "\n"
    }

    return text, nil
}

```
* _components_: input, output, actual task
* _sink_: https://clig.dev/ https://medium.com/@jdxcode/12-factor-cli-apps-dd3c227a0e46 https://www.youtube.com/watch?v=eMz0vni6PAw https://eryb.space/2020/05/27/diving-into-go-by-building-a-cli-application.html https://blog.carlmjohnson.net/post/2020/go-cli-how-to-and-advice/ email author -> 艘 'Golang article typo'
```sh
├── main.foo  # single line returning exit code from internals https://blog.carlmjohnson.net/post/2020/go-cli-how-to-and-advice/
│   └── file_1.txt
│   └── file_2.txt
```

* binaries for multiple architectures https://www.thoughtworks.com/radar/tools?blipid=202203018 https://github.com/goreleaser/goreleaser
* https://towardsdatascience.com/how-to-create-a-cli-in-golang-with-cobra-d729641c717
* _stdlib_:  https://media.pragprog.com/titles/rggo/first.pdf approach 1 https://eryb.space/2020/05/27/diving-into-go-by-building-a-cli-application.html https://github.com/erybz/go-grab-xkcd approach 2 https://blog.carlmjohnson.net/post/2020/go-cli-how-to-and-advice/ https://github.com/carlmjohnson/go-grab-xkcd `flags` not good? https://golang.org/pkg/flag/ https://news.ycombinator.com/item?id=23319770 https://news.ycombinator.com/item?id=23321901
* _Cobra/Viper_: Hugo, Kubernetes https://news.ycombinator.com/item?id=23319172 scaffold https://github.com/spf13/cobra/blob/master/cobra/README.md module support https://github.com/spf13/cobra/issues/1054 https://github.com/spf13/cobra/issues/795 https://github.com/spf13/cobra/pull/817 https://qua.name/antolius/making-a-testable-cobra-cli-app
* _cli_: https://github.com/urfave/cli https://github.com/ayoisaiah/goname/blob/master/cmd/goname/main.go https://news.ycombinator.com/item?id=23321576
* _alternatives_: terminal GUI https://github.com/rivo/tview other options https://go.dev/solutions/clis/ https://github.com/jessevdk/go-flags https://github.com/jaffee/commandeer
* _interactive prompt_: https://github.com/AlecAivazis/survey
* output https://github.com/nikolaydubina/calendarheatmap https://xkcd.com/1138/ https://github.com/vbauerster/mpb https://github.com/cirruslabs/echelon https://github.com/gookit/color/ https://github.com/Delta456/box-cli-maker colors https://github.com/muesli/termenv

- [ ] packaging - recreate Cobra scaffold `golang/packaging`

* ✅ try to run app
* snapshot (env, fs, previous notes at bottom of file, Makefile)
* cp project somewhere else, rm deps (clean --modcache), 'clone', run
* cp project somewhere else, rm deps (not folders), 'clone', run
* cp project somewhere else, rm deps (folders), 'clone', run
* push to GH, rm deps (clean --modcache), clone, run
* push to GH, rm deps (not folder), clone, run
* push to GH, rm deps (folders), clone, run
* basic project w/out deps https://golang.org/doc/code.html
* get set up on work machine

## web

* https://www.allhandsontech.com/programming/golang/web-app-sqlite-go/
* URL shortener https://jrstupkadev.medium.com/golang-url-shortener-22ba6c970792
* basic
```golang
package main

import "net/http"

func main() {
	http.HandleFunc("/", func(w http.ResponseWriter, r *http.Request) {
		w.Write([]byte("Hello, Go"))
	})
	http.ListenAndServe(":8000", nil)
}
```
* https://www.allhandsontech.com/programming/golang/web-app-sqlite-go/
* app config https://github.com/spf13/viper
* vanilla https://eli.thegreenplace.net/2021/life-of-an-http-request-in-a-go-server/
* _db_: `database/sql` (SQLAlchemy engine) gorm (SQLAlchemy ORM) https://eli.thegreenplace.net/2019/to-orm-or-not-to-orm/ https://www.calhoun.io/using-postgresql-with-go  https://github.com/go-reform/reform https://entgo.io/ https://github.com/upper/db in mem KV https://github.com/sdslabs/kiwi generate SQL https://github.com/Masterminds/squirrel CLI https://upper.io/v4/ query builder https://github.com/doug-martin/goqu
* _internationalization (i18n)_: https://phrase.com/blog/posts/internationalization-i18n-go/
* _microservice_: https://github.com/micro/micro https://blog.m3o.com/2020/11/16/building-a-blog-with-micro.html
* frameworks: Buffalo, Gin, Echo 
* routing: https://benhoyt.com/writings/go-routing/
* servers: https://eli.thegreenplace.net/2021/rest-servers-in-go-part-1-standard-library/
* https://www.honeybadger.io/blog/go-web-services/ https://www.youtube.com/channel/UC2GHqYE3fVJMncbrRd8AqcA/videos https://www.usegolang.com/sample/?__s=aqtioiz6aumf2qzwpp96 https://www.youtube.com/playlist/?__s=aqtioiz6aumf2qzwpp96&list=PLVEltXlEeWglOJ42pCxf22YVyxkzan3Xg https://www.usegolang.com/ https://www.youtube.com/playlist/?__s=aqtioiz6aumf2qzwpp96&list=PLVEltXlEeWglOJ42pCxf22YVyxkzan3Xg  https://github.com/go-resty/resty https://github.com/gojek/heimdall https://benhoyt.com/writings/go-routing/ https://github.com/projectdiscovery/httpx

# ZA

env var
* _GO111MODULE_: off (modules outside $GOPATH) https://golang.org/doc/code.html on (modules w/in $GOPATH) https://www.youtube.com/watch?v=H_4eRD8aegk @ 2:54 🗄 `go111.log`
* _GOBIN_: location for `go install`; defaults to `$GOPATH/bin`; set w/ `go env -w GOBIN="$PWD"` https://golang.org/doc/code.html#Command
* _GOENV_: config location
* _GOROOT_: where Go is installed https://stackoverflow.com/a/30295306/6813490
* _GOPATH_: still used but only by the Go installation at large, not for package management https://ukiahsmith.com/blog/a-gentle-introduction-to-golang-modules/ previously pointed to central location (typically `~/go`) for all Go code (src, deps) holding 3 directories (`src`, `pkg`, `bin`) https://golang.org/doc/gopath_code.html

cmds
* _docs_: `doc <mod>` https://blog.golang.org/using-go-modules
* _run_: `run <path/to/file>`
* _binary_: create (`build`) create and mv to `$GOPATH/bin` (`install`) https://www.zombiezen.com/blog/2020/09/how-i-packaged-go-program-windows-linux/
* _rm_: `go clean` ❓ rm what?

design / governance
* controlled by Google https://news.ycombinator.com/item?id=27610108 https://drewdevault.com/2022/05/25/Google-has-been-DDoSing-sourcehut.html
* releases every 6 months https://golang.org/project/
* https://blog.golang.org/open-source https://news.ycombinator.com/item?id=12889302 https://utcc.utoronto.ca/~cks/space/blog/programming/GoIsGooglesLanguage

---

* commands https://github.com/nikolaydubina/go-recipes
* _documentation_: https://blog.golang.org/go.dev https://blog.golang.org/pkg.go.dev-2020
* _gotchas_: http://devs.cloudimmunity.com/gotchas-and-common-mistakes-in-go-golang/
* _memory allocation_: https://blog.learngoprogramming.com/a-visual-guide-to-golang-memory-allocator-from-ground-up-e132258453ed https://notes.eatonphil.com/implementing-a-jq-clone-in-go.html
* _OO_: http://patshaughnessy.net/2015/9/25/what-do-perl-and-go-have-in-common
* _Python_: https://news.ycombinator.com/item?id=22304131
* _style_: https://github.com/golang/go/wiki/CodeReviewComments
* plugins https://eli.thegreenplace.net/2021/plugins-in-go/

## libs

🔍 https://github.com/avelino/awesome-go

* _debug_: can use gdb but delve recommended https://golang.org/doc/gdb https://www.youtube.com/watch?v=r033vEzL6a4
* _env var_ https://endaphelan.me/guides/golang/a-no-nonsense-guide-to-environment-variables-in-go/
* _fake data_: https://github.com/brianvoe/gofakeit
* _feature flag_: https://github.com/thomaspoignant/go-feature-flag
* _file system_: https://github.com/spf13/afero
* _Excel_: https://github.com/360EntSecGroup-Skylar/excelize https://xuri.me/excelize/
* _filesystem_: https://github.com/spf13/afero
* _Git_: https://github.com/go-git/go-git
* _GraphQL_: https://gqlgen.com/ https://sourcehut.org/blog/2020-06-10-how-graphql-will-shape-the-alpha/
* _lint_: https://github.com/golangci/awesome-go-linters
* _logging_ https://github.com/bloom42/rz-go
* _Markdown_: https://github.com/yuin/goldmark
* _math_: https://github.com/montanaflynn/stats
* _profiler_ https://dave.cheney.net/2013/06/30/how-to-write-benchmarks-in-go https://blog.golang.org/profiling-go-programs https://marcan.st/2017/12/debugging-an-evil-go-runtime-bug https://artem.krylysov.com/blog/2017/03/13/profiling-and-optimizing-go-web-applications/ https://github.com/DataDog/go-profiler-notes/blob/main/guide/README.md https://notes.eatonphil.com/implementing-a-jq-clone-in-go.html
* _refactoring_: http://blog.ralch.com/tutorial/golang-tools-refactoring/ http://www.gorefactor.org/
* _REPL_: https://github.com/cosmos72/gomacro https://stackoverflow.com/questions/8513609/does-go-provide-repl
* _search_ https://blevesearch.com/
* _security_ https://github.com/securego/gosec
* _serialization_: https://github.com/bytedance/sonic
* _testing_: https://github.com/stretchr/testify https://eli.thegreenplace.net/2020/faking-stdin-and-stdout-in-go/ https://www.youtube.com/channel/UC2GHqYE3fVJMncbrRd8AqcA/videos https://quii.gitbook.io/learn-go-with-tests/ mock db https://github.com/cockroachdb/copyist/ mocks https://github.com/stretchr/testify https://github.com/jarcoal/httpmock https://www.youtube.com/watch?v=U-eO9_lNi7w
* time https://github.com/mergestat/timediff
* _TOML_: https://github.com/pelletier/go-toml
* _YAML_: https://github.com/goccy/go-yaml

## packaging

🗣 `golang-packaging.md`
🗄 `golang/packaging`
📜 https://golang.org/ref/mod https://github.com/golang/go/wiki/Modules#table-of-contents
🔍 https://pkg.go.dev/
🔗 https://encore.dev/guide/go.mod

start here
* https://eli.thegreenplace.net/2020/you-dont-need-virtualenv-in-go/
> reinstall go to clean out previous pkgs?
* workspaces https://dev.to/gophers/what-are-go-workspaces-and-how-do-i-use-them-1643

workflow
* `mod init`: create module path
* _add deps_: import dependency in your module's source and then try to execute your code in some way (build, test) and go will grab the deps https://blog.golang.org/using-go-modules can use `go download` but don't need to (cf. `go help mod download`); `go get -u ./...` https://engineering.kablamo.com.au/posts/2018/just-tell-me-how-to-use-go-modules
* _list deps_: `list -f '{{ .Imports }}'` (top-level) https://dave.cheney.net/2014/09/14/go-list-your-swiss-army-knife `list -m all` (top-level's subs) https://blog.golang.org/using-go-modules `mod download -json` https://stackoverflow.com/a/52082860/6813490 `go list -f '{{ .Deps }}'` (everything) https://dave.cheney.net/2014/09/14/go-list-your-swiss-army-knife https://www.reddit.com/r/golang/comments/bdtrti/best_way_to_visualize_library_dependencies_with/
* _rm unused_: `mod tidy`

vocabulary
* _source file_: `.go` file https://golang.org/doc/code.html https://golang.org/ref/spec#Packages
* _package_: dir w/ n source files https://rakyll.org/style-packages/ https://golang.org/ref/spec#Packages
* _module_: n pkg + `go.mod` https://blog.golang.org/using-go-modules seems synonymous w/ 'repo' https://blog.golang.org/using-go-modules
* `go.sum`: lock file; check into version control https://blog.golang.org/using-go-modules
* `main`: `func main` (entry point, necessary to compile to bin) `package main` (holds `func main`) `main.go` (holds `func main`) https://www.callicoder.com/golang-packages/
* _import path_: namespace https://stackoverflow.com/q/46312734/6813490 https://blog.golang.org/using-go-modules
* _module path_: seems like same thing as 'import path' https://engineering.kablamo.com.au/posts/2018/just-tell-me-how-to-use-go-modules https://golang.org/ref/mod#tmp_2 required if you're outside $GOPATH https://blog.golang.org/using-go-modules
* _module cache_: where modules get downloaded to `$GOPATH/pkg/mod` https://stackoverflow.com/a/52082860 https://stackoverflow.com/a/52127364 ❓ seems like you can only blow away the entire module cache (`clean -modcache`) vs. the Poetry approach of deleting per project https://github.com/golang/go/issues/32976

upgrade
* _psuedo-version_: untagged commit
* latest tagged: `go get <mod>`; defaults to `@latest` https://blog.golang.org/using-go-modules 'upgrading dependencies'
* list versions: `go list -m -versions <mod>`
* get specific version: `go get <mod>@<version>`
* versioning gotcha https://donatstudios.com/Go-v2-Modules https://qvault.io/2020/09/15/gos-major-version-handling-sucks-from-a-fanboy/

`go.mod`
* human-readable list of deps
* check into version control https://blog.golang.org/using-go-modules
* only lists direct dependencies https://blog.golang.org/using-go-modules 'adding a dependency'
* necessary for module outside `$GOPATH/src`
* defaults to latest version of module if you don't specify https://blog.golang.org/using-go-modules 'adding a dependency'
* _directive_: keyword for each line e.g. `go` (version https://golang.org/ref/mod#tmp_11)
* `indirect`: subdependency https://blog.golang.org/using-go-modules won't be written to `go.mod` unless you perform an upgrade; what *seems* to be happening in the tutorial is that `golang.org/x/text` is a subdep and its parents (`rsc.io/quote`) doesn't specify its version so we just grab latest version which happens to be pseudo version, but when you run `go get golang.org/x/text` it grabs the latest tagged version (which actually should be less recent than the pseudo version, right? otherwise why wouldn't parent dep just specify the stable older version it wanted) and therefore because we're being more specific we have to write it to `go.mod`

misc
* `get`: download and compile module; use global cache (`bin`, `pkg`) https://www.youtube.com/watch?v=71hgdExuCbg 3:50 ❓ dep hell avoided by per-project lockfile? https://dev.to/tbpalsulich/why-go-modules-are-faster-than-gopath-blj
* `install`: compile module; subset of `go get` https://stackoverflow.com/q/24878737 
* _distribution_: https://github.com/goreleaser/goreleaser
* find outdated deps https://github.com/psampaz/go-mod-outdated

design, legacy
* no central repo like PyPI or NPM https://nullprogram.com/blog/2020/01/21/ https://brandur.org/golang-packages 
* 📍 https://blog.golang.org/module-compatibility
* $GOPATH was weird https://news.ycombinator.com/item?id=17061713 
* road to modules: prelim module support in 1.11 and default from 1.13 https://blog.golang.org/using-go-modules https://blog.golang.org/versioning-proposal previous approaches included dep (from Go 1.9-1.10) and Glide https://brandur.org/golang-packages 

* projects move versions more slowly https://benjamincongdon.me/blog/2019/11/11/The-Value-in-Gos-Simplicity
* language seems somewhat Clojure like i.e. doesn't especially encourage using a ton of deps
> Note that while the go command makes adding a new dependency quick and easy, it is not without cost. Your module now literally depends on the new dependency in critical areas such as correctness, security, and proper licensing, just to name a few. - https://blog.golang.org/using-go-modules

* _vendoring_: 🗄 `system.md` https://engineering.kablamo.com.au/posts/2018/just-tell-me-how-to-use-go-modules https://www.youtube.com/watch?v=AIo0UBcvnPg
* _minimum version selection (MVS)_: get the lowest version that will satisfy needs i.e. if `go.mod` needs 1.2 Go won't download an available higher version https://ukiahsmith.com/blog/a-gentle-introduction-to-golang-modules/

* _semantic import versioning_: what would be a new major version of same package in semver becomes a new module https://research.swtch.com/vgo-import 'adding a dependency on a new major version'
> At the same time, allowing different major versions of a module (because they have different paths) gives module consumers the ability to upgrade to a new major version incrementally. In this example, we wanted to use quote.Concurrency from rsc/quote/v3 v3.1.0 but are not yet ready to migrate our uses of rsc.io/quote v1.5.2. The ability to migrate incrementally is especially important in a large program or codebase. - https://blog.golang.org/using-go-modules

## version mgmt

installation
* ✅ use golang.org https://golang.org/doc/install#download
* uninstall: rm `~/go`, `/usr/local/go` https://golang.org/doc/install#uninstall
* use pkg manager https://quii.gitbook.io/learn-go-with-tests/go-fundamentals/install-go https://howistart.org/posts/go/1/ 
* pkg manager bundles tooling (compile, cover, doc)
> my version is Homebrew
* tooling location: `go env GOTOOLDIR` https://golang.org/doc/install#install 🗄 `go help environment`

version mgmt
* ✅ just use version name https://go.dev/doc/manage-install
* version mgmt tool https://github.com/moovweb/gvm
