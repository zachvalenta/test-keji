# TODO

## 参考

## current

## queue

* design 📙 Ramalho @ ch. 1
* compilation📙 Nystrom crafting https://craftinginterpreters.com
* encoding 📙 Bryant computer systems chapter 1

## done

* _19-_: Python, SQL
* _18_: Python, Spring Boot
* _17_: PHP, SQL
* _16_: JavaScript, Java

# COMPILATION

🔗 https://en.wikipedia.org/wiki/Execution_(computing)
🔍 https://softwareengineering.stackexchange.com/questions/tagged/compiler
📚
* Ball interpreter
* Nystrom crafting

* _hot reload_: change program while it runs http://www.jakubkonka.com/2022/03/16/hcs-zig.html

---

* Bryant (5)
* Nisan nand2tetris (4, 6-11)

types of code 📙 Bryant computer systems (3)
* _machine code_: binary; handled by compiler's backend https://hacks.mozilla.org/2017/02/a-crash-course-in-assembly/
* _instuction set_: pattern of bits/int/char that map to cmd https://en.wikipedia.org/wiki/Machine_code#Instruction_set https://steveklabnik.com/writing/is-webassembly-the-return-of-java-applets-flash
* _intermediate representation (IR)_: final step before machine code; handled by compiler's front end https://hacks.mozilla.org/2017/02/a-crash-course-in-assembly/
* _instruction_: individual line of machine code https://hacks.mozilla.org/2017/02/a-crash-course-in-assembly/
* _bytecode_: step after src but before IR? uses hex? https://www.youtube.com/watch?v=QU158nGABxI 23:55 🗄 `python.md` interpreter

* Conery ch. 10
* bytecode, control flow graphs (CFG) https://bernsteinbear.com/blog/discovering-basic-blocks/

types of compilation
* _just-in-time (JIT)_: 
* _ahead-of-time (AOT)_: https://news.ycombinator.com/item?id=22346540
* _adaptive_: quickening https://realpython.com/python311-new-features/#faster-code-execution

compilers
* _cc_: original compiler https://simonwillison.net/2022/Jan/30/a-cgo-free-port-of-sqlite/
* _gcc_: 
* _Clang_: 
* _LLVM_: 

compilation
* _compilers_: gcc, Clang, cl (MS) LLVM (from source to IR, then optimize IR http://aosabook.org/en/llvm.html)
* _output_: machine code ['Go in Practice' 18]
* _CLI options_: `Wall` warn all `-o` choose own name instead of a.out `std` spec
```sh
gcc foo.c -Wall -o my_program m -std='c99'
./my_program
```
* `.a`: lib whose code is embedded into your library
* `.so`: lib whose code is referenced by your library https://stackoverflow.com/a/9809250
* _header file_: imports

* _bootstrapping_: wrote core of compiler in another language and then use that core to build the rest of the compiler in the source language i.e. self-compilation https://softwareengineering.stackexchange.com/a/76640 https://stackoverflow.com/a/18126181
* _executable_: runtime + binary compatible with user os architecture
* for user's machine vs. your server https://testandcode.com/52 @ 29:00
* aka freeze in Python land https://docs.python-guide.org/shipping/freezing/

don't have good topic name for this yet
* _parser_: generates AST from src https://drewdevault.com/2018/12/28/Anatomy-of-a-shell.html
* _AST_: src as tree https://sadh.life/post/ast/
* translate AST from c to Golang src https://simonwillison.net/2022/Jan/30/a-cgo-free-port-of-sqlite/
```python
def area_of_circle(radius):
    pi = 3.14
    return pi * radius * radius

area_of_circle(5)

                 (program)
                /         \
  (area_of_circle r)      (main)
  /           |             |
define    calculate        run area_of_circle
  pi        area             with r = 5
           /   |
     multiply  (pi, r, r)
```
* _grammar_: rules for language's AST https://hakibenita.com/automating-the-boring-stuff-in-django-using-the-check-framework#parsing-the-code
* FFI parser https://scottlocklin.wordpress.com/2021/04/01/obvious-and-possible-software-innovations-nobody-does/
* FFI, JNI https://news.ycombinator.com/item?id=31353740
* _compilation target_: compilation fmt e.g. another lang (JS https://www.youtube.com/watch?v=3LWgbjVWLug 3:00) or binary (WASM) https://steveklabnik.com/writing/is-webassembly-the-return-of-java-applets-flash

times https://stackoverflow.com/q/846103
* _compile time_: compile code; err on static err (syntax, typing)
* _run time_: exec code; err on dynamic err (zero division, run out of mem)
* _import time_: exec code; leads to suble errors
> In Java, import foo means "I depend on the `foo` module; please have the virtual machine link me to it when I run." In Python, import `foo` means "look for `foo.py` in the path, execute it, store local variables in a module object, and assign that module to the `foo` variable in my scope." The difference is that the Python version can run essentially arbitrary code, including importing other modules which then import other modules in turn. https://www.benkuhn.net/importtime/

* linker https://news.ycombinator.com/item?id=27444647 https://gankra.github.io/blah/swift-abi/ 📙 Bryant (7)
https://web.eecs.utk.edu/~azh/blog/teenytinycompiler1.html

🗣 people to ask for help https://github.com/yiblet https://notes.eatonphil.com/starting-a-minimal-common-lisp-project.html
🔗 https://news.ycombinator.com/item?id=24066570
🔗 start here https://www.destroyallsoftware.com/screencasts/catalog
* hosted language: language using 3rd-party compiler (as Clojure uses JVM)
https://keleshev.com/compiling-to-assembly-from-scratch/ https://news.ycombinator.com/item?id=24609774

translators https://en.wikipedia.org/wiki/Symbol_table https://stackoverflow.com/a/3434252
* _assembler_: transform assembly to something less abstract, sometimes machine code and sometimes something a few levels up https://stackoverflow.com/questions/3434202/what-is-the-difference-between-native-code-machine-code-and-assembly-code/3434252#comment25665803_3434252
* _interpreter_: 
* _compiler_: transform high-level language to IR; 'self-hosting' is written in language it's compiling https://robertheaton.com/2017/10/24/what-is-a-self-hosting-compiler/

instructions
> where do virtual machines fit in this taxonomy? https://www.capitalone.com/tech/software-engineering/go-is-boring/
* _symbol table_: map of idenifiers (aka symbol) to type and scope https://en.wikipedia.org/wiki/Symbol_table#Example https://eli.thegreenplace.net/2010/09/18/python-internals-symbol-tables-part-1 https://drewdevault.com/2021/03/19/A-new-systems-language.html

implementations https://github.com/marcpaq/b1fipl
* make a Lisp https://news.ycombinator.com/item?id=21670442
* _JS_: https://github.com/jamiebuilds/the-super-tiny-compiler
* _Ruby_: Ruby Under a Microscope https://codon.com/compilers-for-free from Python https://www.ruby-lang.org/en/documentation/ruby-from-other-languages/to-ruby-from-python/
* _Python_: https://bernsteinbear.com/blog/bytecode-interpreters/ https://ruslanspivak.com/lsbasi-part1/ http://www.aosabook.org/en/500L/a-python-interpreter-written-in-python.html http://www.thedigitalcatonline.com/blog/2017/05/09/a-game-of-tokens-write-an-interpreter-in-python-with-tdd-part-1/ https://github.com/danistefanovic/build-your-own-x#build-your-own-programming-language http://aosabook.org/en/500L/a-python-interpreter-written-in-python.html https://codewords.recurse.com/issues/seven/dragon-taming-with-tailbiter-a-bytecode-compiler http://www.trevorblackwell.com/#faq
* _general_: https://www.youtube.com/watch?v=wSdV1M7n4gQ&t=157s + https://increment.com/programming-languages/crash-course-in-compilers/ + https://blog.wesleyac.com/posts/language-todos + https://blog.felixangell.com/compilers-brief-and-brisk + https://medium.com/basecs
* _Jit_ https://www.youtube.com/watch?v=2BB39q6cqPQ https://eli.thegreenplace.net/2013/11/05/how-to-jit-an-introduction
* _Ball_: src not in repo https://www.reddit.com/r/golang/comments/5eiiw6/writing_an_interpreter_in_go_now_available/ user impl https://github.com/mmyoji/go-monkey https://github.com/skatsuta/monkey-interpreter https://github.com/ELD/monkey-lang-go https://github.com/dnutiu/monkeyInterpreter
* _SQL_: http://aosabook.org/en/sqlalchemy.html

clean up
* _compiled_: src type checked, then run
* _reference implementation_: primary implementation of language (CPython) as compared to other alternate implementations (PyPy, Jython)
* need to have same errors
> We crashed Oracle, including commercial versions of Oracle. We crashed DB2. Anything we could get our hands on, we tried it and we managed to crash it, but the point was that we wanted to make sure that SQLite got the same answers for all of these queries, or equivalent answers, because a lot of these queries, they’re indeterminate and the rows might come out in a different order because you [crosstalk 00:25:10] order by clause, so we wanted to make sure that all the database engines got equivalent answers. Mostly, we wanted to make sure that SQLite was getting the same answers everybody else is. https://corecursive.com/066-sqlite-with-richard-hipp/
* syntax trees https://eli.thegreenplace.net/2009/02/16/abstract-vs-concrete-syntax-trees https://www.pythonpodcast.com/episode-113-jedi-code-completion-with-david-halter/
* _interpreted_: src code run straight away
* _JIT_: normal interpreter but will compile hot paths https://carolchen.me/blog/jits-impls/
* _output_: assembly (for GCC) https://cs.stackexchange.com/questions/14749/why-do-compilers-produce-assembly-code
* writing language compiler in that language https://stackoverflow.com/questions/18247888/how-can-a-c-compiler-be-written-in-c
* _grammar_: syntax for programming language https://blog.robertelder.org/computer-science-for-engineers/
* https://github.com/aalhour/awesome-compilers http://steve-yegge.blogspot.com/2007/06/rich-programmer-food.html https://www.destroyallsoftware.com/talks/the-birth-and-death-of-javascript https://medium.com/basecs https://ruslanspivak.com/lsbasi-part1/ https://nicoleorchard.com/blog/compilers https://github.com/jamiebuilds/the-super-tiny-compiler/blob/master/README.md http://aosabook.org/en/500L/static-analysis.html https://increment.com/programming-languages/crash-course-in-compilers/ https://corecursive.com/037-thorsten-ball-compilers/ https://news.ycombinator.com/item?id=22731505 https://www.pythoninsight.com/2018/09/python-basics-bytecode 

## steps

* _assemble_: convert from HLA to assembly
* _disassemble_: show assembly for HLA https://realpython.com/python311-new-features/#faster-code-execution https://florian-dahlitz.de/blog/disassemble-your-python-code 
```python
import dis
dis.dis(fn)
```

[Conery 216]
* _lex_: tokenize [Conery 218] https://www.aaronraff.dev/blog/how-to-write-a-lexer-in-go
* _lexical analysis_: https://docs.python.org/3/reference/lexical_analysis.html
* _parse_: 
* _semantic analysis_: 
* _optimization_: most of diff btw compilers is here [Conery 216]
* _code generation_: 

* _token_: atomic unit of significance
```python
tokens = {
    "variable": "foo",
    "operator": "=",
    "number": 10
}
```

## semantics

📜 https://docs.python.org/3/reference/index.html

units
* _expression_: value + operator
* an eval to single value e.g. `y + 13` (number) `price > 0` (bool) 📙 Sweigart automate [14]
* _statement_: 动 an action e.g. function call (`logger.debug(ex)`) assignment (`x = 42`) https://beautifulracket.com/appendix/why-racket-why-lisp.html
* compositions of n expressions 📙 Haverbeke [ch.2]
* _block_: 名 group of statements

names
* _identifier_: user defined name; aka 'symbol' https://en.wikipedia.org/wiki/Symbol_table#Example
* _keyword_: reserved and in use; getting shorter https://news.ycombinator.com/item?id=22474850 https://danluu.com/cli-complexity/
* _reserved_: not in use

variables
* _declare_: put var into namespace
* _initialize_: give var initial value
* _assign_: give var subsequent values; `TypeError: 'tuple' object does not support item assignment` supports the definition I've gleaned

operators https://docs.python.org/3/library/stdtypes.html
* _operand_: value used by operator
* _operator_: perform action
* _assignment_: =
* _conditional/ternary_: ?
* _logical/boolean_: and, or, not
* _equality_: ==, != 🗄 `python.md`
* SQL uses `=`
* _identity_: is 🗄 `python.md`
* _comparison_: >, < 📙 Bradshaw [55]
* _membership_: in

arithmatic
* _increment_: `++`
* _infix_: multiplication `*` exponentiation `**` https://treyhunner.com/2018/10/asterisks-in-python-what-they-are-and-how-to-use-them/
* += https://stackoverflow.com/a/7456548

# DESIGN

🗄
* `sociology.md` linguistics
* `system.md` programs / paradigms
📚
* Fowler refactoring
* Martin clean code
* McConnell code complete

systems programming
* languages: C, C++, Rust
* things people write with: dbms, web server, compiler, shell https://drewdevault.com/2021/05/30/Come-build-your-project.html https://drewdevault.com/2021/02/21/On-the-traits-of-good-replacements.html
* fuzzy definition http://willcrichton.net/notes/systems-programming/
* memory management now in favor http://esr.ibiblio.org/?p=7804

metaprogramming
* _metaprogramming_: functions that manipulate existing code e.g. decorators, inspection 📙 Beazley 329
* also synonym for process (build tools, dep mgmt) https://missing.csail.mit.edu/2020/metaprogramming/
* in Ruby (Perrotta) https://news.ycombinator.com/item?id=24935242 

---

> Style and usage matter; sometimes programmers recommend Strunk & White’s The Elements of Style - that’s right, the one about the English language. Its focus on efficient usage resonates with programmers. The idiom of a language is part of its communal identity. - Ford what is code?

> A computer is a clock with benefits. They all work the same, doing second-grade math, one step at a time - Ford what is code?
> Everything ultimately has to get down to things in little boxes pointing to each other. That’s just how things work.  - Ford what is code?
> A programming language is a system for encoding, naming, and organizing algorithms for reuse and application. It’s an algorithm management system. - Ford what is code?
> The true measure of a language isn’t how it uses semicolons; it’s the standard library of each language.
> The Linux kernel is written in C. The software that connects your printer to your computer could be in C. The Web servers that serve up your Web pages are often written in C. It’s also a good language for writing other languages—Python, PHP, and Perl are written in C, as are many others. C is a language you use for building systems; it has the same role in computing that Latin did among Renaissance academics. You won’t often meet a serious practitioner of the digital arts who doesn’t have at least a passing familiarity. The more serious scholars are pretty fluent.
> But there’s another way to interpret all this activity around Python: People love it and want it to work everywhere and do everything. They’ve spent tens of thousands of hours making that possible and then given the fruit of their labor away. That’s a powerful indicator. A huge amount of effort has gone into making Python practical as well as pleasurable to use. There are lots of conferences, frequent code updates, and vibrant mailing lists. You pick a language not just on its technical merits, or its speediness, or the job opportunities it may present, but also on its culture. Python people, generally, are pretty cool.
> But the choice of a main programming language is the most important signaling behavior that a technology company can engage in. Tell me that you program in Java, and I believe you to be either serious or boring. In Ruby, and you are interested in building things quickly. In Clojure, and I think you are smart but wonder if you ship. In Python, and I trust you implicitly. In PHP, and we sigh together. In C++ or C, and I nod humbly. In C#, and I smile and assume we have nothing in common. In Fortran, and I ask to see your security clearance. These languages contain entire civilizations.

https://chriskiehl.com/article/thoughts-after-6-years
more strongly
* Clever code isn't usually good code. Clarity trumps all other concerns.
* So called "best practices" are contextual and not broadly applicable. Blindly following them makes you an idiot
* Designing scalable systems when you don't need to makes you a bad engineer.
* Static analysis is useful
* DRY is about avoiding a specific problem, not an end goal unto itself.
* The word "scalable" has a mystical and stupefying power over the mind of the software engineer. Its mere utterance can whip them into a depraved frenzy. Grim actions have been justified using this word
* Despite being called "engineers," most decision are pure cargo-cult with no backing analysis, data, or numbers
less strongly
* 90% – maybe 93% – of project managers, could probably disappear tomorrow to either no effect or a net gain in efficiency.
changed mind
* After performing over 100 interviews: interviewing is thoroughly broken. I also have no idea how to actually make it better.

> One especially good groove to span is the one between tools and things made with them. For example, programming languages and applications are usually written by different people, and this is responsible for a lot of the worst flaws in programming languages. I think every language should be designed simultaneously with a large application written in it, the way C was with Unix. http://paulgraham.com/marginal.html
> Part of the problem here is social. Language designers like to write fast compilers. That's how they measure their skill. They think of the profiler as an add-on, at best. But in practice a good profiler may do more to improve the speed of actual programs written in the language than a compiler that generates fast code. Here, again, language designers are somewhat out of touch with their users. They do a really good job of solving slightly the wrong problem. - http://paulgraham.com/popular.html
> This is what I’ve started telling people: Use mostly functions, try to make most of them pure. I think that can get people (even new devs) 80% of the benefits (testability, composability, loose coupling, and the ability to reason about code) of more complicated, prescriptive architectures (Hexagonal, Onion, Ports & Adapters, Clean, etc) with a minimal amount of ramp up.- https://news.ycombinator.com/item?id=24915497
> Large organizations have different aims from hackers. They want languages that are (believed to be) suitable for use by large teams of mediocre programmers-- languages with features that, like the speed limiters in U-Haul trucks, prevent fools from doing too much damage. Hackers don't like a language that talks down to them. Hackers just want power. http://www.paulgraham.com/javacover.html
> Computers, operating systems, networks are a hot mess. They're barely manageable, even if you know a decent amount about what you're doing. Nine out of ten software engineers agree: it's a miracle anything works at all. - https://fasterthanli.me/articles/i-want-off-mr-golangs-wild-ride

🗄 `system.md` - 'prematurity'

---

opionated
> So you need to figure out for yourself what kind of team you have, what kind of frameworks you like using, where people can be most productive, so they will stick around through the completion of the project. This is hard. Most places can’t do this. So they go with the lowest common denominator —Java, PHP—because they know that when people leave, they’ll be able to get more of them. - Ford what is code?

speed
> We do not optimize for speed or quality, we optimize our codebase for confidence. For the next person to make changes, For everyone to be able to reason about it, For everyone to be informed enough to ask questions (leave your name next to notes)
> Beware of arguments related to programming speed. All things being equal, faster is better. But all things are never equal. Do you need the kind of speed that lets you get a website up and running quickly? Or the kind that allows you to rotate a few thousand polygons in 3D in real time? Do you need to convert 10,000 PDFs into text per hour? Or 10 million PDFs into text once? These are different problems. - Ford what is code?

community
> The wrong people like it. The programmers I admire most are not, on the whole, captivated by Java. http://www.paulgraham.com/javacover.html
> But there’s another way to interpret all this activity around Python: People love it and want it to work everywhere and do everything. They’ve spent tens of thousands of hours making that possible and then given the fruit of their labor away. That’s a powerful indicator. A huge amount of effort has gone into making Python practical as well as pleasurable to use. There are lots of conferences, frequent code updates, and vibrant mailing lists. You pick a language not just on its technical merits, or its speediness, or the job opportunities it may present, but also on its culture. Python people, generally, are pretty cool. - Ford what is code?
> But the choice of a main programming language is the most important signaling behavior that a technology company can engage in. Tell me that you program in Java, and I believe you to be either serious or boring. In Ruby, and you are interested in building things quickly. In Clojure, and I think you are smart but wonder if you ship. In Python, and I trust you implicitly. In PHP, and we sigh together. In C++ or C, and I nod humbly. In C#, and I smile and assume we have nothing in common. In Fortran, and I ask to see your security clearance. These languages contain entire civilizations. - Ford what is code?

libraries
> 99.5% of programming consists of gluing together calls to library functions. All popular languages are equally good at this. So one can easily spend one's whole career operating in the intersection of popular programming languages. http://paulgraham.com/weird.html
> The true measure of a language isn’t how it uses semicolons; it’s the standard library of each language. - Ford what is code?
> I think a lot of the advances that happen in programming languages in the next fifty years will have to do with library functions. I think future programming languages will have libraries that are as carefully designed as the core language. Programming language design will not be about whether to make your language strongly or weakly typed, or object oriented, or functional, or whatever, but about how to design great libraries. The kind of language designers who like to think about how to design type systems may shudder at this. It's almost like writing applications! Too bad. Languages are for programmers, and libraries are what programmers need. - http://paulgraham.com/popular.html

* development speed vs. execution speed https://bitfieldconsulting.com/golang/rust-vs-go
* Java developers have low pain tolerances https://news.ycombinator.com/item?id=25124513
> Language users do not miss conveniences that they have never had access to in the first place. Those few bi-cultural citizens who function in both Chinese-character and alphabetic worlds are aware of the advantages conferred by the alphabet, but even these people soon get used to the differences, which slip below the level of consciousness, unremarked and unlamented...in virtually every informatic context, from library card catalogs to everyday user’s manuals, the relatively cumbersome Chinese writing system exerts a low-level but constant drag force on productivity 📝 Moser invisible writing
* extensibility is a bad thing (usually) https://drewdevault.com/2020/11/01/What-is-Gemini-anyway.html
* https://www.fredrikholmqvist.com/posts/brooks-wirth-go/

> A programming language is for thinking of programs, not for expressing programs you've already thought of. It should be a pencil, not a pen. [Graham hackers and painters 22]
> Have you ever noticed that when you sit down to write something, half the ideas that end up in it are ones you thought of while writting? The same thing happens with software. Working to implement one idea gives you more ideas. [Graham hackers and painters 68]
> Design and build software, even operating systems, to be tried early, ideally within weeks. Don’t hesitate to throw away the clumsy parts and rebuild them. - Bell Systems Technical Journal https://stratechery.com/2020/the-end-of-os-x

Python
* _insights_: code read more often than written https://www.xkcd.com/353/ have an aesthetic https://www.python.org/dev/peps/pep-0020/ fast enough usually works, even for big things (Instagram, Dropbox, Reddit, Pinterest)
* _widely applicable_: teaching, web dev, sys admin, ML, security, scraping, microcontrollers, industrial automation https://www.pythonpodcast.com/episode-114-industrial-automation-with-jonas-neubert/
* _pain points_: binaries, import system, version management, packaging, browser, native (mobile, desktop), speed (not built for multi-core https://twitter.com/mitsuhiko/status/1091802711908106240)
* _dynamic language trends_: gradual typing (Ruby) speed (PHP https://stitcher.io/blog/php-in-2019)

Golang
* _insights_: composition over inheritance (non-magical, good for maintenance), cleanliness (won't compile if formatting guidelines not met, can't import packages that aren't used, can’t declare variables that aren’t used) speed arbitrage (dev time faster than C, run time faster than dynamic) composition over inheritance https://talks.golang.org/2012/splash.article https://python-patterns.guide/gang-of-four/composition-over-inheritance/
* _pain points_: module system is weird limited to services and CLIs
> Where scripting languages got started as an effective way to write small programs and gradually scaled up, Rust and Go were positioned from the start as ways to reduce defect rates in really large projects. Like, Google’s search service and Facebook’s real-time-chat multiplexer. - http://esr.ibiblio.org/?p=7724
> The single best property of Go is that it is basically non-magical. With very few exceptions, a straight-line reading of Go code leaves no ambiguity about definitions, dependency relationships, or runtime behavior. This makes Go relatively easy to read, which in turn makes it relatively easy to maintain, which is the single highest virtue of industrial programming. - https://peter.bourgon.org/blog/2017/06/09/theory-of-modern-go.html
* Ken Thompson has been right
> I will finally note that Ken Thompson has a history of designs that look like minimal solutions to near problems but turn out to have an amazing quality of openness to the future, the capability to be improved. Unix is like this, of course. It makes me very cautious about supposing that any of the obvious annoyances in Go that look like future-blockers to me (like, say, the lack of generics) actually are. Because for that to be true, I’d have to be smarter than Ken, which is not an easy thing to believe. - http://esr.ibiblio.org/?p=7745
* Ken Thompson has been wrong
> To be clear, I'm not saying that I or anyone else could have done better with the knowledge available in the 70s in terms of making a system that was practically useful at the time that would be elegant today. It's easy to look back and find issues with the benefit of hindsight. What I disagree with are comments from Unix mavens speaking today; comments like McIlroy's, which imply that we just forgot or don't understand the value of simplicity, or Ken Thompson saying that C is as safe a language as any and if we don't want bugs we should just write bug-free code. These kinds of comments imply that there's not much to learn from hindsight; in the 70s, we were building systems as effectively as anyone can today; five decades of collective experience, tens of millions of person-years, have taught us nothing; if we just go back to building systems like the original Unix mavens did, all will be well. I respectfully disagree. https://danluu.com/cli-complexity/#maven

perf
> A good language, as everyone knows, should generate fast code. But in practice I don't think fast code comes primarily from things you do in the design of the language. As Knuth pointed out long ago, speed only matters in certain critical bottlenecks. And as many programmers have observed since, one is very often mistaken about where these bottlenecks are. So, in practice, the way to get fast code is to have a very good profiler, rather than by, say, making the language strongly typed. You don't need to know the type of every argument in every call in the program. You do need to be able to declare the types of arguments in the bottlenecks. And even more, you need to be able to find out where the bottlenecks are. - http://paulgraham.com/popular.html

---

* _cohesion_: like with like stuff related to User in `user.py` stuff for membership in `membership.py`; comes from a book called Structured Design by Larry Constantine [Conery 270]
* _separation of concerns_: synonym for cohesion but applied to app layers (UI, logic, db, auth, logs) and business functions (content mgmt, reporting, membership) [Conery 271]
* duplication beats the wrong abstraction [Conery 275] https://news.ycombinator.com/item?id=23739596

* _things I favor_: feature lean (Go, C) 📍 Wellons https://drewdevault.com/2019/02/18/Generics-arent-ready-for-Go.html
* _generics_: https://drewdevault.com/2019/02/18/Generics-arent-ready-for-Go.html https://news.ycombinator.com/item?id=29705134
* Go designed by austistics, write sloppy code and explore https://www.evanmiller.org/four-days-of-go.html
* [1 line must be written 10 times](https://www.ybrikman.com/writing/2018/08/12/the-10-to-1-rule-of-writing-and-programming/)

> A little duplication is far cheaper than the wrong abstraction. - https://dave.cheney.net/practical-go/presentations/qcon-china.html#_package_design

https://gist.github.com/non/ec48b0a7343db8291b92

prioritize ease of deletion, not ease of extension https://news.ycombinator.com/item?id=23124796
write stupid code https://thorstenball.com/blog/2015/10/22/write-stupid-code/

Graham - Hackers and Painters

> A programming language is for thinking of programs, not for expressing programs you've already thought of. It should be a pencil, not a pen. [22]

> Have you ever noticed that when you sit down to write something, half the ideas that end up in it are ones you thought of while writting? The same thing happens with software. Working to implement one idea gives you more ideas. [68]

languages should get smaller over time https://twitter.com/random_walker/status/1182635589604171776?mc_cid=74bb05ab13&mc_eid=85dafbe485
> Second, C has a tendency to be conservative, changing and growing very slowly. This is a feature, and one that is often undervalued by developers. (In fact, I’d personally like to see a future revision that makes the C language specification smaller and simpler, rather than accumulate more features.) - https://nullprogram.com/blog/2018/11/21/

## functional

📙 Conery

* _functional_: function that operates on other functions https://stackoverflow.com/a/94056

---

* y combinator https://www.youtube.com/watch?v=QuXJ3kXUCiU
* _curry_: break down larger function into smaller and chaining them together 📙 Conery [291,302]
> diff to closure? https://stackoverflow.com/questions/62499789/racket-closure-currying-where-is-the-difference#62500425 🗄 `python.md` partial https://www.youtube.com/watch?v=kZlOy1BY6lY

* https://github.com/hemanth/functional-programming-jargon
* _what makes something functional?_: batch impurity, higher-order functions (decorators, closures, lambdas)
* _pure_: no side effects
* _side effect_: IO, mutation
* _subroutine_: synonym for function https://jeffknupp.com/blog/2013/04/07/improve-your-python-yield-and-generators-explained/
* _functor_: func that iterates over things that are iterable [Conery 307]
* _monad_: functor iterates, monad does logic [Conery 307] wrap control flow https://bytes.yingw787.com/posts/2019/12/06/monads/ https://samgrayson.me/2019-08-06-monads-as-a-programming-pattern/ https://lukeplant.me.uk/blog/posts/understanding-monads-via-python-list-comprehensions/ https://rbtcollins.wordpress.com/2018/08/26/monads-and-python/
* _sink_: https://realpython.com/python-functional-programming/ https://realpython.com/python-reduce-function/ https://github.com/dry-python/returns Land of Lisp epilogue https://docs.python.org/3/howto/functional.html https://kite.com/blog/python/functional-programming https://stackoverflow.com/q/1017621/6813490 https://treyhunner.com/2018/09/stop-writing-lambda-expressions/ https://blog.cleancoder.com/uncle-bob/2014/11/24/FPvsOO.html https://julien.danjou.info/python-and-functional-programming/ https://sumit-ghosh.com/articles/demystifying-decorators-python/ https://jrsinclair.com/articles/2019/what-i-wish-someone-had-explained-about-functional-programming/ https://codewords.recurse.com/issues/one/an-introduction-to-functional-programming http://www.lihaoyi.com/post/WhatsFunctionalProgrammingAllAbout.html https://blog.cleancoder.com/uncle-bob/2017/07/11/PragmaticFunctionalProgramming.html https://docs.python.org/3/howto/functional.html https://github.com/evhub/coconut https://github.com/pytoolz/toolz

## object-oriented

🗄 `system.md` design / DDD
📙 Ramalho fluent python

* _object model_: how objs work in a language 📙 Ramalho [15]
* aka "data model" in Python
* BYO http://aosabook.org/en/500L/a-simple-object-model.html
* _metaobject_: objs that form core of object model 📙 Ramalho [16]
* _attribute_: obj property i.e. field (data) or method (action) https://docs.python.org/dev/tutorial/classes.html
* _attribute reference_: referring to attr https://docs.python.org/dev/tutorial/classes.html#class-objects

inheritance
* _hierarchical_: 1 parent - 1 child
* _multi-level_: 1 grandparent - 1 parent - 1 child
* _multiple_: n parents - 1 child
* aka interfaces in Java, mixins in Python
* _polymorphism_: https://confuzeus.com/hub/django-web-framework/model-polymorphism/ https://news.ycombinator.com/item?id=27658706
* _diamond problem_: https://en.wikipedia.org/wiki/Multiple_inheritance#The_diamond_problem Python solves w/ MRO https://stackoverflow.com/a/44535084/6813490
* _Liskov_: every instance of a subclass (in this case, my extension of Thread) needs to remain a valid instance of the superclass
* _abstract class_: not instantiated; TwoDimensionalShape(Circle, Square, Triangle)
* _Law of Demeter_: don't reach through one object to get to another [Conery 278]

opinions
* creates confusion
> In 2003, Jane Street began a rewrite of its core trading systems in Java. The rewrite was eventually abandoned, in part because the resulting code was too difficult to read and reason about...we built up a nest of classes that left people scratching their heads when they wanted to understand just what piece of code was actually being invoked when a given method was called. https://queue.acm.org/detail.cfm?id=2038036
> The price is that the resulting code is bloated with protocols and full of duplication. This is not too high a price for big companies, because their software is probably going to be bloated and full of duplication anyway. http://www.paulgraham.com/noop.html

---

* quadratic complexity
* _delegation_: composition by another name https://www.thedigitalcatonline.com/blog/2020/08/17/delegation-composition-and-inheritance-in-object-oriented-programming/#delegation-in-oop
* https://www.thedigitalcatonline.com/blog/2020/08/17/delegation-composition-and-inheritance-in-object-oriented-programming/
* https://jesseduffield.com/beginners-guide-to-abstraction/
* https://news.ycombinator.com/item?id=8420060

* _information hiding_: obj as black box against which you can ask for stuff but you don't know how it's going on inside [Connolly database systems 25.3.1 814]
* _override_: replace method inherited from parent
* _overload_: same method name, different sig (i.e. diff params)
* in Python https://martinheinz.dev/blog/50
* _history_: 1970s Smalltalk https://news.ycombinator.com/item?id=29890205 1990s Java https://twobithistory.org/2019/01/31/simula.html https://medium.com/javascript-scene/the-forgotten-history-of-oop-88d71b9b2d9f https://www.hillelwayne.com/post/alan-kay/ https://www.youtube.com/watch?v=QyJZzq0v7Z4

__static methods__
* _static_: belongs to class, not an individual instance
* something that won't change across instances 📍 example
* code organization https://stackoverflow.com/a/14085311/6813490
* bad for testing? https://stackoverflow.com/a/2671938/6813490

opinions
* tell, don't ask [Conery 276]
* unlearn OOP https://dpc.pw/the-faster-you-unlearn-oop-the-better-for-you-and-your-software
* Hickey https://www.youtube.com/watch?v=oytL881p-nQ

method chaining https://www.youtube.com/watch?v=BY34Fe-2xgk
* used in SQL query builders [2:45]
```python
class Player:
    def __init__(self, sh_per=0.40):
        self.points = 0
        self.fatigue = 0
        self.shooting_per = sh_per
    
    def shoot(self):
        self.points += 2.0 * self.shooting_per
        self.fatigue += 1
        return self

    def stats(self):
        print(f"pts {self.points} fatigue {self.fatigue}")
```

## typing

🗄 `python.md` typing
🔗 https://en.wikipedia.org/wiki/Type_system

* _type inference_: figure out type based on context https://calpaterson.com/mypy-hints.html
* _duck typing_: obj of type if it has properties/methods of that type (vs. nominative)
* _nominative typing_: obj type explicitly declared https://en.wikipedia.org/wiki/Nominal_type_system

---

https://www.destroyallsoftware.com/compendium/types?share_key=baf6b67369843fa2

* gradual typing: type hints/annotations in code checked by static analysis tooling, not compiler
* _definitions_: strong/weak less rigorously defined than static/dynamic [Smallshire 1 @ 5.4]
* _sink_: https://danluu.com/empirical-pl/ https://www.cs.uaf.edu/users/chappell/public_html/class/2018_spr/cs331/docs/types_primer.html https://eli.thegreenplace.net/2006/11/25/a-taxonomy-of-typing-systems vocab https://cdsmith.wordpress.com/2011/01/09/an-old-article-i-wrote/ https://danluu.com/empirical-pl/

|   	    | static   	| dynamic   	    |
|---	    |---	    |---	            |
| strong   	| C++      	| Python, Ruby   	|
| weak  	|   	    | JS, Perl   	    |

* _static_: specify type in code (resolved during compilation)
* _dynamic_: don't specify type in code (resolved during runtime) ❓ 'dynamic' synonym for duck typing?
* _weak_: will perform type conversion (e.g. JS) 
* _strong_: won't perform type conversion `42 + 'hi'` throws `TypeError` (only time this happens in Python is `if` statements)

__opinions__

* implicit https://news.ycombinator.com/item?id=26671136
https://news.ycombinator.com/item?id=24839697

> Type checking catches bugs that unit testing does not, often much faster and with less code overhead than unit testing requires. It has surprised me how much of my unit tests were de facto implementing a type system halfheartedly as opposed to testing behavior of those types. - https://threadreaderapp.com/thread/1141836825838800896.html more on typing as a analog to unit tests https://www.jorgemanrubia.com/2019/06/22/on-ruby-and-type-checkers/

> Research has shown that Franklin's remark about giving up liberty to purchase safety is actually about type systems. - https://twitter.com/MarijnJH/status/570833749065265152

turns into metadata addiction

> And Haskell, OCaml and their ilk are part of a 45-year-old static-typing movement within academia to try to force people to model everything. Programmers hate that. These languages will never, ever enjoy any substantial commercial success, for the exact same reason the Semantic Web is a failure. You can't force people to provide metadata for everything they do. They'll hate you. The type system is 'wrong' whenever it cannot match the intended computational model. Every time want to use multiple inheritance or mixins in Java's type system, Java is 'wrong', because it can't do what you want. You have to take the most natural design and corrupt it to fit Java's view of the world. I think the general answer to this is: when in doubt, don't model it. Just get the code written, make forward progress. Don't let yourself get bogged down with the details of modeling a helper class that you're creating for documentation purposes. http://steve-yegge.blogspot.com/2008/02/portrait-of-n00b.html

# LANGUAGES

> [a programming language is] an algorithm management system - Ford what is code?
> We can see that Brooks' 1986 claim that we've basically captured all the productivity gains high-level languages can provide isn't too different from an assembly language programmer saying the same thing in 1955, thinking that assembly is as good as any language can be. https://danluu.com/essential-complexity/#summary

* _C++_: https://ccc.codes/ https://github.com/green7ea/cpp-compilation http://esr.ibiblio.org/?p=7724
* _Haskell_: https://haskellbook.com/
* _PHP_: Laravel great for solo devs https://news.ycombinator.com/item?id=30259097
* _Nim_: https://nim-lang.org/ https://github.com/Pebaz/nimporter

Julia
* https://increment.com/programming-languages/goldilocks-language-history-of-julia/
* https://danluu.com/julialang/
* https://www.evanmiller.org/why-im-betting-on-julia.html
* https://news.ycombinator.com/item?id=27884165
* Jupyter notebooks https://github.com/fonsp/Pluto.jl https://news.ycombinator.com/item?id=31321620

Lua
* for binaries https://news.ycombinator.com/item?id=10974870
* for embedded https://news.ycombinator.com/item?id=3534746
* NeoVim
* multiple compilers https://news.ycombinator.com/item?id=23686297
* not backwards compatibile https://news.ycombinator.com/item?id=3535382
* no stdlib https://news.ycombinator.com/item?id=3535382
* Fennel https://www.mattroelle.com/fennel-the-practical-lisp

R
* _tidyverse_: stdlib https://www.tidyverse.org/index.html
* https://github.com/sfirke/janitor
* Pandas-esque
> Terseness here is a huge advantage as well because in many data analysis workflows you are rerunning that same 10 line snippet over and over, making small changes, adjusting to eventually visualize the thing you're looking for perfectly. Having all of that in the same small block is ideal. https://news.ycombinator.com/item?id=30764505

Rust https://rftgu.rs/
* vs. Golang https://news.ycombinator.com/item?id=31205072
* doesn't have a spec https://drewdevault.com/2019/03/25/Rust-is-not-a-good-C-replacement.html
* big learning curve https://news.ycombinator.com/item?id=30627667
> Despite my infamous distaste for Rust, long-time readers will know that where I have distaste for Rust, I have passionate scorn for C++. I’m quite glad to see Rust taking it on, and I hope very much that it succeeds in this respect. https://drewdevault.com/2021/02/21/On-the-traits-of-good-replacements.html
* syntax https://lucumr.pocoo.org/2015/5/27/rust-for-pythonistas/ https://fasterthanli.me/blog/2020/a-half-hour-to-learn-rust/
* used for: CPU intensive, not API https://news.ycombinator.com/item?id=25798008
* governance problems https://news.ycombinator.com/item?id=28513130
* what people love: packaging, DX https://stackoverflow.blog/2020/06/05/why-the-developers-who-use-rust-love-it-so-much parallelization https://news.ycombinator.com/item?id=26443768 CLI (jless) https://news.ycombinator.com/item?id=30273940 correctness
> [invariant violation] At point A, there's some assumption, and way over there at point B, that assumption is violated... Type systems prevent some invariant violations. Because that works, there are ongoing attempts to extend type systems to prevent still more invariant violations. That creates another layer of confusing abstraction. Some invariants are not well represented as types, and trying makes for a bad fit. What you're really trying to do is to substitute manual specification of attributes for global analysis. The Rust borrow checker is an invariant enforcer. It explicitly does automatic global analysis, and reports explicitly that what's going on at point B is inconsistent with what point A needs. This is real progress in programming language design, and is Rust's main contribution. https://news.ycombinator.com/item?id=29996240

Zig
* overview https://www.thoughtworks.com/radar/languages-and-frameworks?blipid=202203010
* tutorial https://gist.github.com/ityonemo/769532c2017ed9143f3571e5ac104e50
* BYO ls https://stackoverflow.com/questions/13554150/implementing-the-ls-al-command-in-c
* getting popular https://macwright.com/2020/08/01/recently.html
* https://news.ycombinator.com/item?id=29702607
* seems way easier than Rust https://scattered-thoughts.net/writing/assorted-thoughts-on-zig-and-rust/ https://kevinlynagh.com/rust-zig/
* smart users https://github.com/jamii

## assembly

🔗 https://github.com/hackclub/some-assembly-required
📚
* Petzold code (24)
* Nisan nand2tetris (4, 6)

* _assembly_: shorthand for whatever binary the CPU understands 📙 `evans-linux.pdf` 1
* _learning_: 📍 finish second chapter of Manga Microprocessors 🗄 Duntemann https://news.ycombinator.com/item?id=7143585 Latacora CTF https://news.ycombinator.com/item?id=7145479 🗄 Bryant https://news.ycombinator.com/item?id=7143866 microcontrollers https://news.ycombinator.com/item?id=7147009
https://wizardzines.com/comics/assembly/
* most assembly scoped to particular machine architecture; assembly used to be what OS were written in until Unix [LPI 1.1]
* macOS https://news.ycombinator.com/item?id=7144020
* _HLA (high-level assembly)_: just a Randall Hyde thing https://news.ycombinator.com/item?id=7143409
* https://news.ycombinator.com/item?id=26311722

## C lang

📙 Matthews dive https://diveintosystems.org/ http://fabiensanglard.net/c/index.php
📹 https://www.youtube.com/c/JacobSorber/videos
> The Linux kernel is written in C. The software that connects your printer to your computer could be in C. The Web servers that serve up your Web pages are often written in C. It’s also a good language for writing other languages - Python, PHP, and Perl are written in C, as are many others. C is a language you use for building systems; it has the same role in computing that Latin did among Renaissance academics. - Ford what is code?

stdlib
* _libc_: POSIX spec for os stdlib; used by higher-levels languages for everything from networking to memory management https://wizardzines.com/comics/libc/
* _glibc_: most common impl of libc https://stackoverflow.com/a/11373143
* _musl_: used by Alpine https://www.musl-libc.org/ https://news.ycombinator.com/item?id=23819500 https://www.etalabs.net/compare_libcs.html cleaner? https://drewdevault.com/2020/09/25/A-story-of-two-libcs.html
* things people don't like and replacements https://news.ycombinator.com/item?id=25125034

projects
* Python extension https://realpython.com/build-python-c-extension-module/
* db https://cstack.github.io/db_tutorial/
* cmus https://github.com/cmus
* virtual machine https://justinmeiners.github.io/lc3-vm/
* text editor https://viewsourcecode.org/snaptoken/kilo/01.setup.html
* Lisp http://www.buildyourownlisp.com/contents

design
> C has a tendency to be conservative, changing and growing very slowly https://nullprogram.com/blog/2018/11/21/
> The C language is old and boring. It is a well-known and well-understood language. https://sqlite.org/whyc.html
> When programming in C you do not stand on a path, but a plane of decision, and C dares you to decide what to do. http://www.buildyourownlisp.com/chapter1_introduction
> Libraries written in C are callable from any programming language. https://sqlite.org/whyc.html
* https://saagarjha.com/blog/2020/05/10/why-we-at-famous-company-switched-to-hyped-technology/ https://eev.ee/blog/2016/12/01/lets-stop-copying-c/ https://nullprogram.com/tags/c/

history
* _1972_: created https://www.bell-labs.com/usr/dmr/www/chist.html
* _1978_: K&R spec
* _1980_: prominence http://esr.ibiblio.org/?p=7711
* _1989_: c89
* _90s-present_: used for firmware and kernels but new stuff now in other languages http://esr.ibiblio.org/?p=7711
* c99, c11, c17 https://drewdevault.com/2020/11/01/What-is-Gemini-anyway.html https://news.ycombinator.com/item?id=24361469

----

start here
* https://gribblelab.org/CBootCamp @ https://gribblelab.org/CBootCamp/3_Basic_Types_Operators_And_Expressions.html
* Hacking page 21
* https://www.enlightenment.org/docs/c/start
* https://realpython.com/c-for-python-programmers/
* example code: Redis, SQlite https://news.ycombinator.com/item?id=30753428

misc
* sysroot, undefined behavior (UB) https://news.ycombinator.com/item?id=30488979
* _gdb_: debugger https://www.gnu.org/software/gdb/ https://github.com/cs01/gdbgui can be used on more than C https://golang.org/doc/gdb influential in debugger design https://www.npmjs.com/package/trepanjs https://rubygems.org/gems/trepanning
* Postgres codebase is supposed to be a good guide https://news.ycombinator.com/item?id=20556336
* `#define`: constants https://www.youtube.com/watch?v=hsmGp3cp_50 0:50

under the hood
* _ABI_: https://en.wikipedia.org/wiki/Application_binary_interface https://news.ycombinator.com/item?id=24140848 https://gankra.github.io/blah/c-isnt-a-language/
* _abstract machine_: C's version of a virtual machine https://words.steveklabnik.com/should-you-learn-c-to-learn-how-the-computer-works
* _bitfield_: https://danluu.com/algorithms-interviews/
* _compilation_: https://jvns.ca/blog/2019/10/28/sqlite-is-really-easy-to-compile/
* _garbage collection_: (kinda) possible https://stackoverflow.com/a/5009966/6813490
* _undefined behavior_: when an error happens but it's not thrown i.e. `TypeError` in Python might be mean the compiler just chugging along in C https://blog.regehr.org/archives/213 https://news.ycombinator.com/item?id=24363573
* call Python from C http://eradman.com/posts/extending-c-python.html

## Java

* version mgmt: sdkman https://www.youtube.com/watch?v=rouaKVAH3iM
* 🎗 emailed self books on Maven and Spring Boot
* HTTP client https://github.com/square/okhttp
* dev env https://news.ycombinator.com/item?id=30841581
* relearn https://maxmautner.com/2019/09/12/java-primer-for-python-developers.html
* Scala https://news.ycombinator.com/item?id=28479697
* concurrency: https://return.co.de/blog/articles/programming-languages/
* exceptions: Object > Throwable > Error, Exception; checked (compile time) vs. unchecked (runtime)
* generics: prevent type errors in Collections (bc Collections can contain any obj type e.g. str, int, et al.)
* governance https://headcrashing.wordpress.com/2019/05/03/negotiations-failed-how-oracle-killed-java-ee/ https://docs.google.com/document/d/1nFGazvrCvHMZJgFstlbzoHjpAVwv5DEdnaBr_5pKuHo/preview
* GUI: AWT -> FX -> Swing
* imports: can't alias imports, so if you have 2 classes w/ same name, pick one and instead of importing, refer to using fully-qualified name https://stackoverflow.com/a/35686734/6813490
* primitives: everything that's not an object
* _JNDI_: API to lookup on fs or db
* naming: `DefaultJmsListenerContainerFactoryConfigurer` https://spring.io/guides/gs/messaging-jms/
* testing: beware of EasyMock and PowerMock https://return.co.de/blog/articles/java-development-fast/
* run from shell
```sh
# ❗️ "Class JavaLaunchHelper is implemented in both" is [Java on Mac bug](https://stackoverflow.com/a/43003231/6813490)
# from $CWD https://stackoverflow.com/a/3692235/6813490
javac Hello.java
java -cp . Hello

# from package root i.e. `.com` https://stackoverflow.com/a/3081700/6813490
java -cp . com.zachvalenta.Main
```

packages
* package naming convention to create globally unique namespace
* full class name includes the package name
* technically no correlation btw package name and file structure but IDE will complain, which is why we get comically deep directory nesting
* _classpath_: Java's answer to $PATH i.e. where it looks for `.class` files https://stackoverflow.com/a/2396513/6813490

Hibernate
* _DTO/DAO_ https://stackoverflow.com/a/35079306/6813490
* _JPA_: spec for ORM https://stackoverflow.com/a/11881732/6813490
* _ORM_: Hibernate (impl of JPA) JDBC (connect, query w/ SQL) https://www.jooq.org
* pull from db and map onto the `@Entitiy` class
* `validate`: validates that entities compatible against db (checks presence of tables, columns, id generators) https://stackoverflow.com/a/44479455/6813490
* [default value for column](https://www.daveperrett.com/articles/2007/12/05/default-values-with-hibernate-annotations/)
* `none`: do nothing; same effect as elision from `app.props`
* `validate`: [validate entities against DDL](https://stackoverflow.com/q/43965089/6813490)
* `create`: run DDL based on entities when app boots
* `create-drop`: " " + then rm on shutdown
* `update`: update schema according to entities (but won't rm columns)
❗️ `update` not for PROD https://stackoverflow.com/a/221422/6813490 + https://stackoverflow.com/a/21113195/6813490 + https://stackoverflow.com/a/42147995/6813490
* create table
```java
@Entity
@Table(name = "ZV_TEST_TABLE")
public class ZVTestTable {
    @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    private long id;
    private String foocol;
    private String barcol;
}
```

JVM
* _Java_: language + JDK
* _JDK_: JRE + compiler; `/usr/libexec/java_home`
* _JRE_: JVM + libs (Collections, IO)
* _JVM_: src to bytecode, env to run byte; handles IO, threading; [written in C](https://stackoverflow.com/a/1220931)
* _classloader_: pull `.class` files into JVM
* workaround for JVM cold start https://medium.com/teads-engineering/jvm-and-cache-warm-up-strategy-for-high-traffic-services-4b5016f8b565
* keeps getting faster https://stackoverflow.blog/2020/07/30/java-at-25-features-that-made-an-impact-and-a-look-to-the-future

Maven
* better than Gradle: https://return.co.de/blog/articles/java-development-fast/ https://blog.philipphauer.de/moving-back-from-gradle-to-maven/ but Gradle uses Groovy instead of XML, back in the day there was Ant
* _bill of materials_: define parent POM, all lower transitive dependencies (child dependencies [test, web, Jackson] and their children) will all be compatible)
* build: `package`
* fix all your problems: `clean install`
* skip tests: `-DskipTests=true`
* rebuild w/out deps update: `-o`
* `target`: where compiled code goes
* _plugin_: kinda like a class
* _goal_: kinda like a method on a class
* _phase_: series of goals strung together e.g. `mvn package` runs all goals up to and incl. `package`; `install` (installs to local `~/.m2`) `deploy` same as install except pushes to internal repo

Spring
* _Spring_: next gen EE
* _Spring Boot_ : Spring (MVC) + OOB config
* _wiring_: use IDE to make Maven project, parent POM to `spring-boot-starter-parent` https://www.youtube.com/watch?v=bDtZvYAT5Sc
* _aspect-oriented_: afaik encapsulation by another name; separate logging from business logic 📙 Ramalho 16
* _bean_: obj
* _boot_: init Spring context (looks around for `@Components`), starts Tomcat, runs app https://www.baeldung.com/running-setup-logic-on-startup-in-spring
* _container_: manage beans i.e. create, config, connect, garbage collection
* _dependencies_: https://docs.spring.io/spring-boot/docs/1.4.2.RELEASE/reference/htmlsingle/#appendix-dependency-versions
* _history_: 2002 Rod Johnson publishes framework, turns into SpringSource 2003 Dell acquires VMWare 2009 VMWare acquires SpringSource 20013 Dell and GE form Pivotal
* `@Bean`: init obj and keep track of it https://stackoverflow.com/a/34174782/6813490
* `@Configuration`: seems similar to `@Bean`
* `@Autowire`: use obj already init elsewhere (or from some 3rd-party lib)
* `@Entity`: tells JPA to map class to table https://stackoverflow.com/a/29333628/6813490
* `@Value`: pull in V from `.properties` into class

## Lisp

📙 SICP https://wizardforcel.gitbooks.io/sicp-in-python/content/ https://mitpress.mit.edu/sites/default/files/sicp/index.html https://www.youtube.com/playlist?list=PLE18841CABEA24090 http://www.sicpdistilled.com/ https://xuanji.appspot.com/isicp/ https://corecursive.com/039-hal-abelson-sicp/ https://news.ycombinator.com/item?id=24428907 https://thorstenball.com/blog/2016/11/30/why-i-wrote-a-book-about-interpreters/  https://news.ycombinator.com/item?id=30016323

> At one point, I decided I should learn Lisp or Haskell, probably because of something Paul Graham wrote. I couldn't find a Lisp textbook in the library, but I found a Haskell textbook. After I worked through the exercises, I had no idea how to accomplish anything practical. But I did learn about list comprehensions and got in the habit of using higher-order functions. https://danluu.com/learning-to-program/

Lisps https://stackoverflow.com/questions/47482349/what-characterizes-a-lisp-dialect
* Fennel https://www.mattroelle.com/fennel-the-practical-lisp
* _Clojure_: https://blog.cleancoder.com/uncle-bob/2019/08/22/WhyClojure.html https://tonsky.me/blog/utils/ Joy of Clojure better than Clojure for the Brave and True? http://ahungry.com/blog/2018-12-26-Clojure-is-Capable.html https://news.ycombinator.com/item?id=20844978 check out this book, Dan Luu recommended https://twitter.com/ctford/status/1345798531119009792
* _Common Lisp_: less Lisp-y, really fast compiler https://notes.eatonphil.com/starting-a-minimal-common-lisp-project.html https://ebzzry.io/en/script-lisp/ http://stevelosh.com/blog/2018/08/a-road-to-common-lisp/ http://paulgraham.com/popular.html https://news.ycombinator.com/item?id=32723784
* _Racket_: based off Scheme, async database https://notes.eatonphil.com/walking-through-a-basic-racket-web-service.html https://news.ycombinator.com/item?id=7823337 https://news.ycombinator.com/item?id=19952714 https://news.ycombinator.com/item?id=23132621 https://news.ycombinator.com/item?id=8206038 https://news.ycombinator.com/item?id=13881535 https://news.ycombinator.com/item?id=32723784
* _Scheme_: lotta different Scheme compilers and Scheme programs are not compatible across different compilers bc the language spec is so minimal (50 pages compared to 650 for Java) https://hardmath123.github.io/perchance-to-scheme.html 

language
* s-expressions https://news.ycombinator.com/item?id=5654398 https://notes.eatonphil.com/compiler-basics-lisp-to-assembly.html
* no loops https://www.lvguowei.me/post/sicp-goodness-looping/
* prefix notation: operator comes first https://www.braveclojure.com/getting-started/

misc
* declarative? [Karwin 2]
* _history_: self-perpetuating failure https://news.ycombinator.com/item?id=13143282 Lisp was more awesome in a world w/out Java, Python?
* _written in Lisp_: ITA, Emacs
* _sink_: https://twobithistory.org/2018/10/14/lisp.html https://beautifulracket.com/appendix/why-racket-why-lisp.html http://jakob.space/blog/thoughts-on-lisps.html http://www.paulgraham.com/rootsoflisp.html https://treenotation.org/ https://www.youtube.com/watch?v=1r5GkhoN-Zc https://github.com/syncsynchalt/axiomatic-lisp

# MEMORY

🔍 https://softwareengineering.stackexchange.com/questions/tagged/memory
🗄
* `architecture.md` memory
* `python.md` memory

memeory management https://stackoverflow.com/a/3434252
* _unmanaged code_: language w/ no memory management e.g. C, C++; sometimes used to mean "compiles directly to machine code" by people who do not understand that C has an abstract machine
* _managed code_: language w/ memory management (Java); dynamic languages not typically described as such, more of a marketing term for enterprise languages
* _garbage collection_: scheduled memory management; yes (Python, Java) no (Rust 'borrow checker') no-unless-you-hack-real-hard (C, C++)
* memory leak https://www.glean.com/blog/how-we-analyzed-and-fixed-a-golang-memory-leak

interning
* _intern_: reuse i.e. only storing one version of obj
* prevent creation of obj with same value and type https://python-reference.readthedocs.io/en/latest/docs/functions/intern.html#remarks
* handled by compiler

## argument passing 

🗄 stack - in-place, out-of-place

https://mathspp.com/blog/pydonts/pass-by-value-reference-and-assignment
terms 🗄 pointers
* _pass by reference_: function operates on passed obj https://realpython.com/python-pass-by-reference/#defining-pass-by-reference
> seems to be used interchangeably w/ in-place https://realpython.com/python-pass-by-reference/#best-practice-use-dictionaries-and-lists
* _pass by value_: function operates on values of passed obj by copying to new obj https://www.interviewcake.com/question/python3/reverse-words https://neilalexander.dev/2021/08/29/go-pass-by-value.html
* _pass by assignment_: Python's approach; aka 'pass by object reference' https://realpython.com/python-pass-by-reference/#passing-arguments-in-python https://robertheaton.com/2014/02/09/pythons-pass-by-object-reference-as-explained-by-philip-k-dick/

pass by reference https://realpython.com/python-pass-by-reference/#using-pass-by-reference-constructs
* used to save memory when obj are large (data sci)
* used for counters
```c#
// C# allows actuall pass by reference
incrementer(ref int counter){
    counter++;
}
int counter = 0;
incrementer(ref counter);  // counter = 1
incrementer(ref counter);  // counter = 2
```
```python
# Python can give you interface of counter but not actually pass by reference i.e. still creates new obj https://realpython.com/python-pass-by-reference/#replicating-pass-by-reference-with-python
def incrementer(num):
    return num + 1

counter = 0
id(counter)  # 4304845280
counter = incrementer(counter)
id(counter)  # 4304845312
```

## pointers

* _pointer_: memory address https://nullprogram.com/blog/2019/06/30/ https://boredzo.org/pointers/#definition

---

* https://boredzo.org/pointers/ https://www.ralfj.de/blog/2020/12/14/provenance.html

* _pointer value_: value at memory address
* _reference_: synonym for memory address https://stackoverflow.com/a/36208432 or obj at mem address https://realpython.com/pointers-in-python/#names-in-python
* _dereference_: derive pointer value from pointer
* _reference_: derive pointer from pointer value
```go
// https://tour.golang.org/moretypes/1
hitchhiker := 42  // 42
p = &hitchhiker // 0x414020 - reference
*p // 42 -> dereference
```
* used for saving memory https://stackoverflow.com/a/850850
* not even agreement on how difficult the topic is or, if it is difficult, why it's difficult (which probably means it is intrinsically difficult) https://stackoverflow.com/q/5727
* "FOO_LANGUAGE doesn't have pointers" = language doesn't expose memory allocation to end user? language doesn't intern? https://realpython.com/pointers-in-python/#understanding-variables
```python
# name: does intern
a = 13
b = a
a is b  # True
```
```c
// variable: doesn't intern i.e. value copied to new mem address
int x = 42;  // 0x7ffee4c114f8
int y = x;  // 0x7ffee4c114f4
```

## stacks

* _stack frame_: instance of function execution
* vars, args, metadata (location in call stack, return address)
* _call stack_: all frames in state of execution 📙 Bhargava 3.42
* aka traceback, stack trace https://realpython.com/python-debugging-pdb/#python-caller-id
* _stack overflow_: too many frames on stack and process runs out of memory https://developer.mozilla.org/en-US/docs/Glossary/Call_Stack

* _stack_: mem for stack frame var https://danielmiessler.com/study/difference-stack-heap-based-memory/
* auto deallocation on func completion
* faster to access than heap (at least in Java) https://www.baeldung.com/java-stack-heap https://blog.robertelder.org/computer-science-for-engineers/
* _heap_: memory used for manual de/allocation https://danielmiessler.com/study/difference-stack-heap-based-memory/
* _garbage collection_: deallocate mem in heap 📙 Conery 216

place 🗄 `algos.md` complexity
* _out-of-place_: mutates copy of data https://www.interviewcake.com/concept/python3/in-place
* _in-place_: mutates original data https://en.wikipedia.org/wiki/In-place_algorithm
* i.e. doesn't create additional obj for purpose of data manipulation, does it within stack frame
* generally a bad idea https://twitter.com/raymondh/status/1055478808793546752 https://stackoverflow.com/a/1637838 https://www.interviewcake.com/concept/python3/in-place
* aka 'destuctive'
* funny example from unit tests that requires you to swap elements https://www.interviewcake.com/question/python3/reverse-string-in-place

---

* ❓ relationship to space complexity https://www.interviewcake.com/concept/python3/in-place https://en.wikipedia.org/wiki/In-place_algorithm#Examples
```python
def in_place(qd):
    for ind, el in enumerate(qd):  # just mutates original
        qd[ind] *= el

def out_of_place(qd):
    new_qd = list()  # creates new obj for mutation
    for ind, el in enumerate(qd):
        new_qd[ind] *= el
```

# ZA

history https://increment.com/programming-languages/language-history/
* _1957_: Fortran (IBM); still the best for math https://news.ycombinator.com/item?id=14498904 Python better? https://cerfacs.fr/coop/fortran-vs-python
* _1958_: Lisp (MIT)
* _1959_: Cobol; process transactions
* _1972_: C (Bell Labs) Smalltalk (Xerox Parc) 
* _1985_: C++ (Bell Labs)
* _1990_: Python
* _1995_: Java (Sun) JS (Netscape) Ruby (Matz) https://twobithistory.org/2017/11/19/the-ruby-story.html

language server 🗄 `vim.md`
* _language server_: provides editor with code completion, syntax highlighting
* talks to editor via LSP (language server protocol) https://en.wikipedia.org/wiki/Language_Server_Protocol 📙 Neil modern 127
* options: jedi, vanilla MS (OSS) https://github.com/microsoft/python-language-server Pylance (not OSS) https://github.com/microsoft/pylance-release/issues/4

za
* _DSL_: abstraction layer https://tonsky.me/blog/dsl/ https://eloquentjavascript.net/03_functions.html https://news.ycombinator.com/item?id=22375721
* _static analysis_: run rules against non-running code; aka code quality (CQ); autofmt (black, prettier) lint (flake8) security (https://github.com/returntocorp/semgrep)
* _standard library (stdlib)_: algos, datetime, networking https://drewdevault.com/2021/03/19/A-new-systems-language.html
> The base state of programming is gluing together library calls. Since glue code can be written in any language, most programmers' language preferences are really library preferences. - Graham https://twitter.com/paulg/status/1373926244673323008

---

* math happens in the CPU, in language interpreters, and in libraries https://macwright.com/2020/02/14/math-keeps-changing.html
* Knuth 'Art of Computer Programming' are math books https://news.ycombinator.com/item?id=19976957&
* _string interpolation_: combine string literal and placeholders https://en.wikipedia.org/wiki/String_interpolation
* probabilistic https://mrandri19.github.io/2022/01/12/a-PPL-in-70-lines-of-python.html
* Elixir https://news.ycombinator.com/item?id=28482580
* visual https://news.ycombinator.com/item?id=27928772
* non-English languages: Italian https://news.ycombinator.com/item?id=24330089 https://en.wikipedia.org/wiki/Non-English-based_programming_languages atypical languages in general https://esoteric.codes/
* _sink_: https://blog.wesleyac.com/posts/language-todos https://opencredo.com/java-go-back/ https://news.ycombinator.com/item?id=14521894 http://peter.bourgon.org/blog/2017/06/09/theory-of-modern-go.html
* checklist https://news.ycombinator.com/item?id=21057335
* programming languages not in English
* _escape_: treat char in non-literal manner e.g. `\d` as a single digit in regex vs. the char `d` https://docs.python.org/3/reference/lexical_analysis.html?highlight=string%20literal#string-and-bytes-literals

learn a few languages well
> Based on internet comments and advice, I had the idea learning more languages would teach me how to be a good programmer so I worked through introductory books on Python and Ruby. As far as I can tell, this taught me basically nothing useful and I would have been much better off learning about a specific area (like algorithms or networking) than learning lots of languages. https://danluu.com/learning-to-program/

* _null_: indicates absence of value (n.b. obj ref cannot be said to 'equal' null) [Beaulieu 2.29] https://www.lucidchart.com/techblog/2015/08/31/the-worst-mistake-of-computer-science/
* _generics_: e.g. reverse array of any type https://blog.golang.org/why-generics https://drewdevault.com/2019/02/18/Generics-arent-ready-for-Go.html https://news.ycombinator.com/item?id=29702607
* _debuggers_ https://eli.thegreenplace.net/2011/01/23/how-debuggers-work-part-1 https://eli.thegreenplace.net/2011/01/27/how-debuggers-work-part-2-breakpoints https://eli.thegreenplace.net/2011/02/07/how-debuggers-work-part-3-debugging-information https://scattered-thoughts.net/writing/looking-for-debugger-2/
* keep a language small https://medium.com/@erights/the-tragedy-of-the-common-lisp-why-large-languages-explode-4e83096239b9

> “So much of art is discovery, and you can’t discover anything if you can’t see what you’re doing” - Victor, ‘Inventing on Principle'
* bring your own client (editor, browser, RSS) https://www.geoffreylitt.com/2021/03/05/bring-your-own-client.html

when you really love your favorite language 💜
> My favorite programming language is C. It’s fast, simple, and compiles very quickly. Unlike many other languages, it’s quite reasonable for an individual to have a comprehensive understanding of the entire language. C is my default choice unless something else is particularly better suited (Python, shell script, etc.). There’s also a special place in my heart for Emacs Lisp, a venerable goofball language that’s so much fun to discuss. https://nullprogram.com/about/

## control flow

* _branching factor_: degree of nesting in control flow 📙 Kleppmann 81 https://fivethirtyeight.com/features/what-if-trump-loses-and-wont-leave/
* _cyclomatic complexity_: number of linear paths through a problem i.e. how many if-else https://github.com/PyCQA/mccabe
> diff btw branching factor and cyclomatic complexity?

conditionals
* case statemtent, goto, if/else (invented by McCarthy http://www.paulgraham.com/diff.html)
* _guard clause_: seems synonymous w/ 'conditional' https://en.wikipedia.org/wiki/Guard_%28computer_science%29 https://refactoring.com/catalog/replaceNestedConditionalWithGuardClauses.html
* don't nest https://pythonbytes.fm/episodes/show/131/python-3-has-issues-over-on-github

loops
* batched vs. naive = if dealing with large number of iterations, do write operation every n iterations https://avi.im/blag/2021/fast-sqlite-inserts/
* types: for, while, do-while (same as `while` except executes at least once)
* `continue`: goto next iteration
* `break`: exit

## functions

semantics https://realpython.com/python-pass-by-reference/#defining-pass-by-reference
* _function_: returns single obj https://www.youtube.com/watch?v=EnSu9hHGq5o 14:30
* aka callable https://towardsdatascience.com/functools-the-power-of-higher-order-functions-in-python-8e6e61c6e4e4
* aka subroutine
> That process of going character by character can be wrapped up into a routine - also called a function, a method, a subroutine, or component. (Little in computing has a single, reliable name, which means everyone is always arguing over semantics.) - Ford what is code?
* _generator_: returns stream of objs https://www.youtube.com/watch?v=EnSu9hHGq5o 14:30
* _argument_: value passed to function
* _parameter_: spec for arg (number, order, type)

types
* _factory_: function that returns another function
* e.g. constructor w/ some defaults https://realpython.com/factory-method-python/
* _first-class_: doesn't need to be attached to obj 
* _higher-order_: can be passed around, assigned to var, used as args to another function, returned from function, take other function as arg
* _lambda_: anonymous function; syntactic sugar for a normal function definition
* _eval()_: take string and evaluate as if expression from language

evaluation https://en.wikipedia.org/wiki/Evaluation_strategy
* _eager_: eval expression during assignment
* _lazy_: don't eval until necessary 🗄 `django.md` db
* _thunk_: way to do lazy evaluation https://en.wikipedia.org/wiki/Thunk
