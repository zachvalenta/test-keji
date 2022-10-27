# 看板

## 参考

🔍
* https://www.commandlinefu.com
* https://explainshell.com/
📚
* Evans shell
* Shotts linux command line
* Stutz cookbook

## current

## next

* Conery final chapter
* fzf
* tmux

## done

* _22_: Fira Mono for iTerm font/icons, try starship, try/fail vi mode for readline, organize utils
* _21_: line editor, fzf for bash history https://hacker-tools.github.io/lectures/
* _20_: broot
* _19_: exa, symlink dotfiles, try out utils (z, fish, tig, fzf, ranger, ripgrep)
* _18_: scripts (`fne`, `qing`, `ding`, `qiu`, `jb`)

# BASH

📙 Shotts command line
🔗
* https://github.com/dylanaraps/pure-bash-bible
* http://aosabook.org/en/bash.html
* https://github.com/anordal/shellharden/blob/master/how_to_do_things_safely_in_bash.md
* https://leanpub.com/learnbashthehardway
* https://wizardzines.com/zines/bite-size-bash/

as HLA
* downsides: not great for scripting other than universality (which is great); crappy syntax, hard to test, limited data structures https://medium.com/capital-one-developers/bashing-the-bash-replacing-shell-scripts-with-python-d8d201bc0989 doesn't do autosuggestion, syntax highlighting https://danyspin97.org/blog/colorize-your-cli/
> The opposite of "it's like riding a bike" is "it's like programming in bash". A phrase which means that no matter how many times you do something, you will have to re-learn it every single time. https://twitter.com/JakeWharton/status/1334177665356587008
* mischief https://news.ycombinator.com/item?id=18902830
* `reset`: bail out when things go crazy [Linux Cookbook 2.3.5]
* template https://news.ycombinator.com/item?id=25428621
* linting: https://github.com/koalaman/shellcheck https://github.com/anordal/shellharden https://www.youtube.com/watch?v=28Ygo05cLmo
* testing https://github.com/sstephenson/bats https://github.com/amoffat/sh https://blog.esciencecenter.nl/testing-shell-commands-from-python-2a2ec87ebf71 https://github.com/bach-sh/bach

history https://catonmat.net/the-definitive-guide-to-bash-command-line-history
* search: `ctrl r`
* scroll all items that match query: `ctrl r` (again)
* cancel search: `ctrl c`
* scroll previous: `ctrl p`
* scroll next: `ctrl n`
> same when you're in search mode
* event designator: `history | rg cd` then go to event w/ `!<event_num>`
> it can be helpful to stick something like `#useful` or `# description` on the end of a command you expect to need again https://news.ycombinator.com/item?id=13888269

snippets
```sh
# new line
echo -e "foo bar \n"
echo -en "\n"

# debug mode https://github.com/Idnan/bash-guide#4-debugging
#!/usr/bin/env bash - x

# strict mode http://redsymbol.net/articles/unofficial-bash-strict-mode/
set -euo pipefail
IFS=$'\n\t'

# directory depth (~/Desktop/zvmac/materials/za) https://unix.stackexchange.com/a/369458/331460
$ find yuyan -type d | wc -l  # 15
$ find business -type d | wc -l  # 1

# generate random string https://unix.stackexchange.com/a/230710/331460
```

dates
* https://github.com/jarun/pdd
* backup w/ timestamp: `touch "$(date +%Y%m%d_%H%M%S).bak"` https://unix.stackexchange.com/a/96383/331460
* _touch_: make new file or update timestamp
* create dir with current date
```sh
today="$(date +'%Y-%m')"
hour_min="$(date +'%H-%M-%S')"
\cd $HOME/Documents
dir="my-dir-$today-$hour_min"
mkdir "$dir"
```

---

where to put shell scripts
* `/usr/local/bin` [Linux Cookbook A.3.4]
* `~/bin`
* `fooDir` --> `~/bin`

* _shebang line_: pick which interpreter will run script
```sh
# BASH
#!/usr/bin/env bash

# Python
#!/usr/bin/env python3 ### $PATH
#!/usr/bin/python3.6 ##### absolute path
```

capitalization https://stackoverflow.com/a/673940/6813490
* uppercase: env var
* lowercase: everything else

## args

```sh
# get previous arg https://www.youtube.com/watch?v=vt-IvdFP5ZA
$_

# positional
$ cmd arg1 arg2 # $0 = cmd, $1 = arg1, $2 = arg2, $@ = all args

$#  # number
$@  # all e.g. for file in "{$files[@]}"

# none
if [ $# -eq 0 ]; then

# equality
if [ "$var" = "$var" ]; then

# empty string: -z (true if empty) -n (true if not empty) https://stackoverflow.com/a/18096739
if [ -z "$var" ]; then

# integer https://stackoverflow.com/a/28898213
if [[ "$var" =~ ^-?[0-9]+[.,]?[0-9]*$ ]]
```

## control flow

📜 https://ss64.com/bash/if.html

* file operators: exists `-e` is a regular file not dir `-f` https://ss64.com/bash/syntax-file-operators.html

```sh
###
# ITERATION
###

my_array=(item1 item2 item3)

# for
for FILE in *; do echo $FILE; done  # files in dir https://www.digitalocean.com/community/tutorials/workflow-loop-through-files-in-a-directory
for var in "$@"  # all args
for var in "${arr[@]}"  # all arr el
do
    git add "$var"
done

# while
while [ -z "$ur_var" ]; do
    thing
done

# until
until [ -z "$ur_var" ]; do
    thing
done

###
# CONDITIONALS
###

# if
if [ -z "$ur_var" ]; then
    echo "hey"
else
    echo "hi"
fi

# if else
if [ -z "$ur_var" ]; then
    echo "hey"
else
    echo "hi"
fi

# if elif else
if [ ]; then
    echo "hey"
elif [ ]
then
    echo "hi"
else
    echo "hello"
fi

###
# BOOLEAN OPERATORS
###

A && B # if A then B
A ; B # A then B (regardless of A exit code)
A || B # if not A then B
A & B # A and B simultaneously
```

## execute

* _eval_: use str as cmd https://www.youtube.com/watch?v=0A4Kjr8ThJA 1:45
```sh
x="date"
echo $x  # date
eval $x  # Tue Feb 22 18:33:49 EST 2022

# use to set multiple exports at once
eval "$(brew shellenv)"
```

```sh
# check if command exists
if ! type -f fswatch >/dev/null ; then
  echo "fswatch not installed: install with `brew install fswatch`" >&2
  exit 2
fi
```
* sudo https://bsago.me/tech-notes/sudo-with-aliases-in-fish
* keep script from consuming too many resources: `nice myscript`
* add location: `./myscript` doesn't need to be on $PATH
* as a cmd: `myscript` (script need shebang and perm to exec)
* using bash: `bash myscript` (doesn't need shebang or perm to exec, can debug this way using `bash -x myscript`)
```sh
$ foo
-bash: zv/bin/foo: Permission denied
$ l
-rw-r--r-- foo # no perm

$ bash foo
hi zjv # can still exec w/ `bash`
```

---

```sh
# 📍 'Automate' appendix B

# as .py
`python script.py`
# with shebang
`./script.py`  # apparently this only works if file is executable, where `bash script.sh` always works
```

* _source_: export variable to environment within current shell; syntax-wise either `source` or `.` https://stackoverflow.com/a/16619261

📍 re: `suan` https://stackoverflow.com/questions/874452/change-the-current-directory-from-a-bash-script

* __call script directly__: `<script>`
* __dot command__: . `<script>`
* __dot + forward slash__: . `<script>`
* __sh command__: sh `<script>` 
* __bash command__: bash `<script>`

[source vs. execute](https://superuser.com/a/795838)

* put on $PATH
* make executable `chmod u+x script.sh`
* if bash, remove `.sh` (`script.sh` ➡️ `script`) and call (`script`)
* if python, keep `.py` and call (`script.py`)

📝 get tab completion from terminal if put on $PATH

__dot command__: `. fooScript.sh`

```sh
# diff btw `source` and `./` 
# ➡️ https://stackoverflow.com/a/9640736/6813490

# use `exit`
🈚️ ☞☞☞ ./git-hooks/test_zv.sh

# use `return`
🈚️ ☞☞☞ source git-hooks/test_zv.sh
```

❓ diff btw this and all the other ways 😄
❓ why does Python script require `./script.py`

```sh
code
<script>
. <script>
./ <script>
sh <script> 
bash <script>
```

## exit codes

codes
* _0_: success 
* _1_: err 
* _2_: "misuse of shell built-ins" (e.g. "no such file" err) https://askubuntu.com/a/892605 
* _?_: var for last cmd's exit code e.g. `echo "hi"; echo $?  #0` https://askubuntu.com/a/892607
* _127_: you use a command in your script that the shell doesn't know about
* _130_: termination via CTRL c
* _137_: script faile (128) and then received sig kill (9) from OOM killer https://stackoverflow.com/a/1041309

---

* cleanup on exit https://github.com/Idnan/bash-guide#exit-traps
* are less clear than you think https://news.ycombinator.com/item?id=24267155
* get exit code of last command: `$?` https://www.freecodecamp.org/news/docker-exec-how-to-run-a-command-inside-a-docker-image-or-container/
* `exit`: close shell
* `return`: exit script
* _sink_: http://www.tldp.org/LDP/abs/html/exitcodes.html https://en.wikipedia.org/wiki/Exit_status#Shell_and_scripts https://bencane.com/2014/09/02/understanding-exit-codes-and-how-to-use-them-in-bash-scripts/
```sh
~/Desktop/zvmac/materials/sw/algos/algos (master *)$ rg austen  # no results
~/Desktop/zvmac/materials/sw/algos/algos (master *)$ echo "$?"  # 1
```

## $PATH

* change precedence: https://apple.stackexchange.com/a/49961
* _default_: `/bin`, `usr/bin`
* _global_: `/etc/paths`
* _user_: `.bash_profile`
* `$PATH`: list of directories that the shell should search when looking for programs corresponding to commands entered by the user [LPI 2.7]

## strings

```sh
alice="hi, alice"
echo "${alice}"  # contents
echo "${#alice}" # length

# slice https://unix.stackexchange.com/a/47372
alice="alice"
nickName="$(echo "$alice" | cut -c3-)"
echo "$nickName"
```

---

* [remove char from front of string](https://unix.stackexchange.com/a/194938)
* [remove char from end of string](https://unix.stackexchange.com/a/399397)
* [store command in string and then run](https://stackoverflow.com/a/2355242/6813490)

## variables

* braces https://www.youtube.com/watch?v=FzBdcKkvUg8
* https://jvns.ca/blog/2017/03/26/bash-quirks/ https://zwischenzugs.com/2018/01/06/ten-things-i-wish-id-known-about-bash/ https://www.hackerrank.com/domains/shell/bash
* [store command in string and then run](https://stackoverflow.com/a/2355242/6813490)
* [plus command substitution](http://www.compciv.org/topics/bash/variables-and-substitution/)

```sh
# assign
# AFAIK can't have spaces between var, equal operator, and value
str="alice"
arr=("one" "two" "three")

# ref
echo "$alice"

# expand/concatenate
echo "hi, ${alice}. look at these random numbers: ${randomNum}"
```

📝 use quotes around variables (if contains spaces, is empty &c. everything will break 😑)
📝 always quote your variables

https://stackoverflow.com/a/673940/6813490

# INTERFACES

🔗 https://unixsheikh.com/articles/the-terminal-the-console-and-the-shell-what-are-they.html

❓
* _teletype_: https://the.exa.website/introduction
* _subshell_: ? https://github.com/Canop/broot/issues/115#issuecomment-573183294
* _tty_: ?

exec
* _shell_: cmd interpreter https://stackoverflow.com/a/44388115
* origins in VT-100 terminal https://josephg.com/blog/databases-have-failed-the-web/

IO
* _command line_: IO for shell
* _line editor_: editing for command line https://en.wikipedia.org/wiki/Line_editor
* ++ autocomplete, history substitution https://danyspin97.org/blog/colorize-your-cli/
> Some versions of the Python interpreter support editing of the current input line and history substitution, similar to facilities found in the Korn shell and the GNU Bash shell. This is implemented using the GNU Readline library, which supports various styles of editing. https://docs.python.org/3/tutorial/interactive.html

UI
* _terminal emulator_: shell GUI
* i.e. command line + viewport (previous cmd, output)
* get current terminal `echo $TERM_PROGRAM` https://github.com/dylanaraps/neofetch/wiki/Terminal-and-Terminal-Font-detection
* handles font, colors https://hacker-tools.github.io/command-line/ https://wizardzines.com/comics/terminals/
* "emulator" bc original terminals were hw connected to mainframe https://news.ycombinator.com/item?id=23320090
* _multiplexer_: window manager + session mgmt for terminal 📙 Hogan x
* multiplexers w/out sessions e.g. dvtm
* sessions w/out window mgmt e.g. abduco https://www.youtube.com/watch?v=GbZFwpmr230 0:45

## graphical

window mgmt
* _window manager_: windows in non-overlapping frames (tiling), switch btw apps using hotkeys https://hacker-tools.github.io/os-customization/ https://askubuntu.com/a/20435
* aka tiling https://www.youtube.com/watch?v=j1I63wGcvU4
* Windows https://news.ycombinator.com/item?id=33168263
* AlwaysOnTop https://www.youtube.com/watch?v=6IxRlaTWsoQ
* aka screen manager  https://missing.csail.mit.edu/2019/os-customization/
* xmonad: https://jvns.ca/blog/2020/01/05/paperwm/ https://kevinlynagh.com/newsletter/2020_04_keyboards_rethinking_desktops/ https://news.ycombinator.com/item?id=30402358
* i3: tiling + hotkeys https://www.youtube.com/watch?v=bdumjiHabhQ 3:30
* Slate: https://github.com/jigish/slate
* tiling for macOS https://magnet.crowdcafe.com/ https://news.ycombinator.com/item?id=22852157 https://faun.pub/yabai-macos-tile-window-manager-833ce1be396a?gi=132df1bca0e1

za
* _window system_: one level down from window manager?
* X11, X Window System https://github.com/sharkdp/pastel#get-a-list-of-all-x11--css-color-names https://xmonad.org/ https://github.com/sharkdp/pastel#get-a-list-of-all-x11--css-color-names
* KDE/Gnome ride on top of https://en.wikipedia.org/wiki/X_Window_System Wayland https://en.wikipedia.org/wiki/Wayland_(display_server_protocol) https://www.youtube.com/watch?v=lm2aireP-wc https://www.youtube.com/watch?v=jFxwPJpUwl0
* textual https://news.ycombinator.com/item?id=24243521 https://drewdevault.com/2019/03/11/Sway-1.0-released.html
* _desktop environment_: how apps/folders look
* Gnome https://wiki.gnome.org/ https://jvns.ca/blog/2020/01/05/paperwm/ https://news.ycombinator.com/item?id=24491091 https://blog.edfloreshz.dev/articles/linux/system76/rust-based-desktop-environment/

## line editor

* _readline_: line editor
* impl https://github.com/chzyer/readline
* view keybindings: `bind -P` https://catonmat.net/bash-vi-editing-mode-cheat-sheet
* set mode: `set -o <emacs/vi>`
* exec previous cmd: `!!` https://bsago.me/tech-notes/a-replacement-for-!!-in-fish

* _vi_: doesn't support text obj e.g. `cw` works but `ciw` doesn't https://vi.stackexchange.com/a/9876 https://catonmat.net/bash-vi-editing-mode-cheat-sheet
* scroll history: `j/k`

---

* autocomplete https://fig.io/

to read before you take another swing at using vi mode
* https://twobithistory.org/2019/08/22/readline.html
* https://thoughtbot.com/upcase/videos/readline
* config https://missing.csail.mit.edu/2020/editors/
* problem #1: would allow single motion and then go into insert mode
* problem #2: scroll history; can use emacs commands in vi mode as workaround https://stackoverflow.com/q/42951222
> both of these worked at first

bindings
* readline https://stackoverflow.com/questions/35046794/where-can-i-view-all-my-custom-keybindings-in-bash
* https://bsago.me/tech-notes/insert-text-with-fish-keybindings
* https://stackoverflow.com/questions/10870468/whats-the-usage-of-bind-in-bash
* https://www.computerhope.com/unix/bash/bind.htm

emacs https://catonmat.net/bash-emacs-editing-mode-cheat-sheet
* scroll history: `CTRL n/p`
* _repeat previous command_: `!!`
* _goto - word - forward_: alt b
* _goto - word - forward_: alt f
* _goto - line - end_: ctrl e
* _goto - line - start_: ctrl a
* _rm - word - back_: ctrl w
* _rm - word - forward_: alt d
* _rm to - line - end_: ctrl k
* _rm to - line - start_: ctrl u

completion
* _tab completion_: aka autocomplete, expansion https://python-poetry.org/docs/ https://www.freecodecamp.org/news/fzf-a-command-line-fuzzy-finder-missing-demo-a7de312403ff/ 
* uses `complete` https://tuzz.tech/blog/how-bash-completion-works
```sh
$ complete -W "red green blue yellow purple pink orange" color
$ color <TAB><TAB>
# blue    green   orange  pink    purple  red     yellow
$ color p<TAB><TAB>
# pink    purple
```
* `ctrl e` tab complete from bash history
```sh
# tig.log
> Bash completion has been installed to: /usr/local/etc/bash_completion.d
```

## multiplex (tmux)

📙 Hogan @ 3
📜 https://github.com/tmux/tmux
🔗 https://thoughtbot.com/upcase/tmux

* install via Homebrew

---

* Neovim https://rutar.org/writing/from-vim-and-tmux-to-neovim/
* one session per project e.g. t3, data eng, baseline (desktop/cmus/yin) https://www.youtube.com/watch?v=hbs7tuwpgZA 1:45
* guided tour https://www.youtube.com/watch?v=sSOfr2MtRU8 @ 5:00
* persist sessions through restart https://github.com/tmux-plugins/tmux-resurrect https://www.youtube.com/watch?v=sMbuGf2g7gc
* n windows w/in single session of terminal emulator https://linuxize.com/post/getting-started-with-tmux/
* switch btw sessions w/ fzf https://news.ycombinator.com/item?id=22857615
* vim https://github.com/christoomey/vim-tmux-navigator https://www.youtube.com/watch?v=gnupOrSEikQ
* config, pane count https://www.youtube.com/watch?v=FTklH6z0LWA
* https://willvaughn.org/articles/the-tmux-manual-review/
* https://vimtricks.com/p/quickly-access-project-notes/
* _why switch from iTerm?_ named sessions https://www.youtube.com/watch?v=hbs7tuwpgZA 7:50 temp full screen of panes [ibid 6:35]
* _config_: more ergonomic binding for prefix https://thoughtbot.com/upcase/videos/tmux-introduction https://thoughtbot.com/upcase/videos/tmux-configuration
* _workflow_: session per Git project https://www.youtube.com/watch?v=hbs7tuwpgZA https://thoughtbot.com/upcase/videos/tmux-introduction one pane for Vim and another for running tests
* copy, paste https://thoughtbot.com/upcase/videos/tmux-navigation
* _normal navigation cmds (page up, et al.)_: prefix [ then q to exit
* _leader_: synonym for hotkey?

vocabulary
* _pane_: portion of window running process https://thoughtbot.com/upcase/videos/tmux-introduction 类似 Vim split (and you could also have a window be a single pane of a Vim instance within which you use Vim splits) https://www.youtube.com/watch?v=hbs7tuwpgZA 3:58 https://thoughtbot.com/upcase/videos/tmux-vim-integration
* _window_: terminal space to be divided up
* _session_: collection of n windows https://www.youtube.com/watch?v=hbs7tuwpgZA 3:30

cmd
* _start_: `tmux`
* _stop_: `exit`
* _prefix to all cmd_: `ctrl b`
* _list all cmd_: `?`

pane https://thoughtbot.com/upcase/videos/tmux-introduction
* _horizontal split_: prefix %
* _vertical split_: prefix "
* _toggle splits_: prefix o
* _switch splits by direction_: prefix arrow

session
* _create named_: `tmux new-session -s <name>`
* _save_: tmux-resurrect (apparently you'd otherwise lose on shutdown) https://www.youtube.com/watch?v=hbs7tuwpgZA 9:50
* _detach_: run in background; `prefix d` or `tmux detach-session` https://thoughtbot.com/upcase/videos/tmux-introduction
* _list_: `tmux ls`
* _attach_: bring to foreground; `tmux a <num>` or `tmux attach -t <name>`; can use `choose-tree` as well https://thoughtbot.com/upcase/videos/tmux-navigation

## shell

* TUI for bash https://github.com/charmbracelet/gum
* design https://www.micahlerner.com/2021/07/14/unix-shell-programming-the-next-50-years.html 🗣 Dan Luu
* get current shell: `echo $SHELL` https://stackoverflow.com/a/3327022/6813490
* switch shell: `<shell>` https://fishshell.com/docs/current/tutorial.html#tut_getting_started
* return to default shell: `exit`

zsh
> autocomplete
* _zsh_: bash superset
* `.zprofile`: `.bash_profile` https://apple.stackexchange.com/q/388622
* `.zshrc`: put `PS1` here https://unix.stackexchange.com/q/71253
* silence warning not to use bash `export BASH_SILENCE_DEPRECATION_WARNING=1` https://elisabethirgens.github.io/notes/2020/02/bye-bash/
* comes installed on macOS https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH https://nil.wallyjones.com/what-shell-am-i-using/
* frameworks: ohmyzsh, pretzo https://hacker-tools.github.io/command-line/
* autocomplete https://github.com/zsh-users/zsh-autosuggestions
* scripting language not portable https://news.ycombinator.com/item?id=18778681
* trailing percent sign thing https://unix.stackexchange.com/a/167600

fish
> autocomplete nice but have to rewrite profile
* https://bsago.me/tech-notes
* install: brew; uninstall https://fishshell.com/docs/current/faq.html#faq-uninstalling
* autocomplete using history
> I can just type part of a command, hit arrow-up and look through only the relevant results https://news.ycombinator.com/item?id=27992073
* aliases
> aliases (which are called abbreviations) are actually expanded after typing, so the full command appears in your history. You can also edit the full command before running it https://news.ycombinator.com/item?id=27992073
* accept autosuggestion: `CTRL f` https://stackoverflow.com/a/58382167/6813490
* autocomplete https://www.benkuhn.net/autocomplete/ https://ianthehenry.com/posts/sd-my-script-directory/ https://news.ycombinator.com/item?id=18777113 
* pgcli inspired by fish https://news.ycombinator.com/item?id=15912028
* might have to rewrite profile https://news.ycombinator.com/item?id=15913251 https://superuser.com/questions/446925/re-use-profile-for-fish
* `!!` doesn't run last cmd https://news.ycombinator.com/item?id=15943070
* scripting language not portable https://news.ycombinator.com/item?id=18778681 https://news.ycombinator.com/item?id=15911216
* can't run bash scripts = just switch back to bash https://news.ycombinator.com/item?id=18777141 https://jvns.ca/blog/2017/04/23/the-fish-shell-is-awesome/
* there's a Vi mode but apparently doesn't work well https://stackoverflow.com/questions/28444740/how-to-use-vi-mode-in-fish-shell https://news.ycombinator.com/item?id=18778048
* more design thoughts https://news.ycombinator.com/item?id=23957325

xonsh
* https://news.ycombinator.com/item?id=30302955
* https://github.com/hauntsaninja/pyp
* need to rewrite profile https://xon.sh/xonshrc.html https://xon.sh/bash_to_xsh.html
* bad w/ virtualenvs https://xon.sh/python_virtual_environments.html

others https://github.com/oilshell/oil/wiki/Alternative-Shells
* crush https://news.ycombinator.com/item?id=24079001
* elvish https://news.ycombinator.com/item?id=18778681
* nushell: https://www.nushell.sh/
* oil: https://news.ycombinator.com/item?id=24079001
* WSL: run Linux programs on Windows https://www.youtube.com/watch?v=idW-an99TAM https://blog.jessfraz.com/post/windows-for-linux-nerds/
* BYO https://www.destroyallsoftware.com/screencasts/catalog
* _Powershell_: supports some Bash commands but no arguments https://yehudakatz.com/2019/04/24/powershell-lets-get-started
* good at working with structured text like CSV https://news.ycombinator.com/item?id=28306401

## terminal (iTerm)

🗄 sourcing
🔗 https://anarc.at/blog/2018-04-12-terminal-emulators-1/

iTerm 📜 https://iterm2.com/documentation.html
* restore tabs https://superuser.com/a/755924
* select tab: keys > nav > tab https://stackoverflow.com/a/59303000
* font: load to Font Book, then update per profile
* alternatives: xTerm, Hyper, kitty https://sw.kovidgoyal.net/kitty/ https://www.youtube.com/watch?v=1XkRfJbcVAo Warp https://news.ycombinator.com/item?id=30921231
* create config: general > preferences > load from folder https://stackoverflow.com/a/25122646 (`com.googlecode.iterm2.plist`)
* hand ALT: preferences > profiles > keys > left option as esc+ https://stackoverflow.com/a/345949
* hotkey: keys > hotkey > show/hide all windows (`ALT SPACE`)
* fullscreen: `CMD ENTER`
* _arrangement_: group of windows
* save default: `CMD SHIFT s`
* use default: arrangements > set default, general > startup
* _split_: window
* create: keys > keybindings > split w/ default
* nav: keys > nav > shortcut to chooose split pane > CMD number
* fullscreen: `CMD SPACE ENTER`
* colortheme https://rigel.netlify.app/#terminal

hotkey
* _hotkey_: keypress handled by listening program even if another program is active
* https://news.ycombinator.com/item?id=31625407
* killer feature https://news.ycombinator.com/item?id=17924264 https://news.ycombinator.com/item?id=22853277
* AutoHotKey https://www.hillelwayne.com/post/ahk/
* Karabiner https://missing.csail.mit.edu/2019/os-customization/ https://news.ycombinator.com/item?id=30876934
* Alfred https://www.alfredapp.com/
* snap https://rectangleapp.com/

music icon screwup
* can't do icons for music files https://gitlab.com/gnachman/iterm2/-/issues/7570
* workaround #1: check file extension every time you run ls e.g. `fd -d 1 -e md`
* workaround #2: every time you go to music dir, source alternate profile that will overwrite `l` with no icons

prompt
* things I want: Git branch, Python version, venv
* Git: https://www.youtube.com/watch?v=wku-1nJR_oA https://github.com/zachvalenta/dotfiles/commit/cc4117a72c7b1d80f0ec58021530727435a2e4af https://raw.githubusercontent.com/git/git/master/contrib/completion/git-prompt.sh https://stackoverflow.com/questions/31252573/get-current-directory-without-full-path-in-fish-shell
* _pure_: zsh only https://github.com/sindresorhus/pure
* _powerlevel10k_: https://github.com/romkatv/powerlevel10k
* _powerline_: statusline and prompt for Vim and used by zsh https://github.com/powerline/powerline
* can install via pip https://pypi.org/project/powerline-status/ https://github.com/wesbos/Cobalt2-iterm
* _starship_: https://starship.rs/
* downside: slower than powerline-shell, Git status looks worse
* upside: support for pyenv, Poetry https://starship.rs/config/#package-version
* install `brew install starship` or `sh -c "$(curl -fsSL https://starship.rs/install.sh)"`
* update `sh -c "$(curl -fsSL https://starship.rs/install.sh)"`
* uninstall `sh -c 'rm "$(command -v 'starship')"'`
* venv https://github.com/starship/starship/issues/1529
* won't get Python version if you're using an alias https://github.com/starship/starship/issues/632
* _powerline-shell_: powerline but works on bash and zsh (w/out ohmyzsh) https://github.com/b-ryan/powerline-shell
* conf: `~/.config/powerline-shell/config.json`
* requires powerline for fonts? https://powerline.readthedocs.io/en/latest/installation/osx.html
* no Poetry support https://github.com/b-ryan/powerline-shell/issues/507
* https://github.com/b-ryan/powerline-shell#generic-segments

---

* terminal theme w/ gruvbox https://www.youtube.com/watch?v=h509rn2xIyU
* emoji https://darrenburns.net/posts/emoji-in-the-terminal/
* scripting https://cgamesplay.com/post/2020/11/25/iterm-plugins/ https://github.com/kamranahmedse/itomate
* _conf - save_: general > preferences > load from custom folder > pick folder you want them saved in https://stackoverflow.com/a/25122646/6813490
* _error debug_: https://gitlab.com/gnachman/iterm2/issues/7517
* _goto pane_: preferences > keys > navigation shortcuts > switch to split panes
* _locate cursor_ | CMD /
* _open default_: general > startup > default window arrangement
* _open profile_: window > restore window arrangement https://medium.com/@jessesrsmith/five-tips-for-iterm-91db83cf4d4e
* _split_: preferences > keys > add
* _status bar_: profile > session > configure status bar
* how to open custom arrangement in new window w/ keyboard shortcut? https://gitlab.com/gnachman/iterm2/issues/5739 https://github.com/gnachman/iTerm2 https://stackoverflow.com/questions/tagged/iterm2 https://stackoverflow.com/a/29464585/6813490 https://apple.stackexchange.com/a/25084
> I would like to open an arrangement in a new window **after** starting up iTerm.
> I bolded 'after' bc I already have configured iTerm to open a specific arrangements of profiles (start `cmus`, cd into my `code` directory, etc.) **on startup**. Which is awesome and a huge time-saver.
> When jumping back into a project, however, I often need to arrange a bunch of windows (start a dev server in one window

# USERLAND

🗄
* `applications.md` utils
* `db.md` utils
* `git.md` utils
* `linux.md` dev env

* _coreutils_: ls, rm, cat, et al. https://en.wikipedia.org/wiki/List_of_GNU_Core_Utilities_commands
* aka userland https://bitfieldconsulting.com/golang/scripting
* rewrite in Rust https://news.ycombinator.com/item?id=26396798 https://jvns.ca/blog/2022/04/12/a-list-of-new-ish--command-line-tools/ https://github.com/ibraheemdev/modern-Unix aka "modern UNIX" https://www.thoughtworks.com/radar/tools/modern-unix-commands

autojump
* _autojump_: jump to recently visited dir https://missing.csail.mit.edu/2020/shell-tools/
* what I use: lots of alias in `.bash_profile`
* options: https://github.com/rupa/z https://github.com/wting/autojump https://github.com/clvv/fasd https://github.com/ajeetdsouza/zoxide
* BYO https://news.ycombinator.com/item?id=22853119

monitoring
* directory size: du, ncdu https://github.com/bootandy/dust `du -sh -- * | sort -r` https://unix.stackexchange.com/a/185777 https://github.com/muesli/duf
* disk space: view of mounts; `df -h`; colorize https://danyspin97.org/blog/colorize-your-cli/
* memory: free (UNIX) top (macos) gotop https://github.com/xxxserxxx/gotop/issues/50 ytop https://github.com/cjbassi/ytop
* network: https://github.com/imsnif/bandwhich

za
* _asciicinema_: terminal recording https://darrenburns.net/posts/tools/ https://github.com/nbedos/termtosvg https://github.com/cytopia/ffscreencast
* _bc_: do math on stdin https://missing.csail.mit.edu/2020/data-wrangling/
* _imgcat_: render img in terminal https://news.ycombinator.com/item?id=23319272
* _gotty_: term as web app https://github.com/yudai/gotty
* _neofetch_: system info
* _scc_: code stats https://github.com/XAMPPRocky/tokei
* _tldr_: cheatsheets https://github.com/tldr-pages/tldr/tree/master/pages https://github.com/dbrgn/tealdeer https://github.com/chubin/cheat.sh
* _whereis_: search for executables in system db https://github.com/Idnan/bash-guide#c-whereis
* _which_: search for executables on path https://github.com/Idnan/bash-guide#d-which

## awk

📙
* Kernighan awk
* Shotts command line

* _awk_: process columnar data
* avoid by parsing stdout to JSON then using JSON query tool e.g jq https://github.com/kellyjonbrazil/jc https://www.thoughtworks.com/radar/tools?blipid=202203056

recipes https://kadekillary.work/post/cli-4-ds/ https://neowaylabs.github.io/programming/unix-shell-for-data-scientists/
* get $PWD from path: `awk -F"/" '{print $NF}'` https://stackoverflow.com/a/17921589
* get last word in line https://stackoverflow.com/a/16617037
* sum series of numbers https://stackoverflow.com/a/28926450
```sh
# use awk 'control file' against input file
awk -f my_script.awk /etc/ntp.conf
# set delimiter
ifconfig foo | awk -F":" '/HWaddr/{print toupper($3 $4)}'
```
```aw
# BEGIN block (processed once) = clarify output, set delimiter ('file separator'), 
BEGIN { FS=":" ; print "username"}

{ print $1}# UNNAMED block = prints for each line 
mt ps | awk '{print $1}' # https://askubuntu.com/a/161803

# END block (processed once) = clarify output
END { print "TOTAL USERS: " NR}  # NR = num rows
```

versions
* `awk -W version` -> doesn't work on macOS
* _mawk_: used on Ubuntu, Debian
* _gawk_: other distros (on macOS also)

---

* https://github.com/thewhitetulip/awk-anti-textbook/
* https://en.wikipedia.org/wiki/The_AWK_Programming_Language
* https://blog.jpalardy.com/posts/why-learn-awk/ 
* https://gregable.com/2010/09/why-you-should-know-just-little-awk.html
* http://www.grymoire.com/Unix/Awk.html
* https://blog.jpalardy.com/posts/why-learn-awk/
* https://gregable.com/2010/09/why-you-should-know-just-little-awk.html

## CLI design

🗄
* `information.md` serialization
* `python.md` CLI

impl language
* C: ✅ fast ❌ development speed
* Nim: ✅ distribution ❌ maturity https://ssalewski.de/nimprogramming.html
* Python: ✅ exploratory ❌ distribution
* Go: ✅ distribution, fast startup https://news.ycombinator.com/item?id=23319684 ❌ stdlib lib lib not good
* Rust: ✅ speed, Clap library https://news.ycombinator.com/item?id=23320411 better for cross platform https://cuchi.me/posts/go-vs-rust ❌ language itself

input https://news.ycombinator.com/item?id=31293032
* https://nullprogram.com/blog/2020/08/01/
* _flag_: hyphen e.g. `cmd --from here --to there`
* letter (`-h`) word (`--help`) https://www.youtube.com/watch?v=FOQHGz__OLs
* _arg_: no hypen `cmd here there`; less clear than flags bc have to remember which is src and which is target https://medium.com/@jdxcode/12-factor-cli-apps-dd3c227a0e46

## file explorer (broot)

📜 https://dystroy.org/broot/ https://github.com/Canop/broot

conf https://dystroy.org/broot/conf_file/
* fs on personal `~/Library/Preferences/org.dystroy.broot`
* fs on work machines `~/.config/broot/conf.toml`
* default file now `conf.hjson` but can rm and use `conf.toml`
* broot will run exec on ALT ENTER
* mv focus to preview pane https://github.com/Canop/broot/issues/480 https://dystroy.org/broot/#preview-files

install
* shell function adds line to bash profile https://github.com/Canop/broot/issues/115
* Homebrew version might lag https://github.com/Canop/broot/issues/123
* reinstall: `broot --install`
* keybindings: preview file `alt p` close preview `alt q` quit `ctrl w` open file `alt enter` https://github.com/Canop/broot/issues/86#issuecomment-573197384
* ❓ how to turn file preview on by default? https://www.freecodecamp.org/news/fzf-a-command-line-fuzzy-finder-missing-demo-a7de312403ff/
* set Vim as editor https://missing.csail.mit.edu/2020/editors/

file explorers
* _file explorer_: TUI for file system e.g. Finder (mv, rm, preview)
* aka file browser, file manager
* alternatives: vifm https://www.youtube.com/watch?v=RGOsE3UWqhI https://www.youtube.com/watch?v=6eyFXcyosu8 lf https://www.youtube.com/c/BrodieRobertson/search?query=lf nnn https://github.com/jarun/nnn fff https://github.com/dylanaraps/fff/issues/135 

## file goto (fzf)

📜 https://github.com/junegunn/fzf
> fzf is just a Unix filter https://www.freecodecamp.org/news/fzf-a-command-line-fuzzy-finder-missing-demo-a7de312403ff/

uses https://www.freecodecamp.org/news/fzf-a-command-line-fuzzy-finder-missing-demo-a7de312403ff
* file preview/open
> can replace broot
* autojump
> can replace aliases

---

* setup using vim, bat, rg, fzf https://www.youtube.com/watch?v=aLMepxvUj4s
> you should finish Vim config and plugin mgmt and Neovim before doing this
* find all files containing text w/ rg, fzf for filter, bat for preview matches https://stackoverflow.com/questions/61740910/how-do-i-fuzzy-find-all-files-containing-specific-text-using-ripgrep-and-fzf-and
* seems like more documentation on how to do this within Vim https://sidneyliebrand.medium.com/how-fzf-and-ripgrep-improved-my-workflow-61c7ca212861 https://www.youtube.com/watch?v=fP_ckZ30gbs https://www.youtube.com/watch?v=loNdGAnKEf8
```sh
# https://www.linuxuprising.com/2021/03/a-quick-introduction-to-fzf-interactive.html
fzf --preview 'bat --style=numbers --color=always --line-range :500 {}'
```
* config https://www.freecodecamp.org/news/fzf-a-command-line-fuzzy-finder-missing-demo-a7de312403ff/
* select git branches https://seb.jambor.dev/posts/improving-shell-workflows-with-fzf
* can be used to replace broot file preview https://www.youtube.com/watch?v=aLMepxvUj4s
* alternatives: https://github.com/mptre/pick https://github.com/facebook/PathPicker https://github.com/lotabout/skim
* uses `find` under the hood https://github.com/junegunn/fzf/issues/1625#issuecomment-507674106
* as broot alternative (cd to dir of file) https://github.com/junegunn/fzf/wiki/Examples#changing-directory https://mike.place/2017/fzf-fd/
```sh
# cdf - cd into the directory of the selected file, suggested by @harelba and @dimonomid:
cdf() {
   local file
   local dir
   file=$(fzf +m -q "$1") && dir=$(dirname "$file") && cd "$dir"
}
```
* https://seb.jambor.dev/posts/improving-shell-workflows-with-fzf/
* can use to cd w/ `alt c` although broot does better here https://www.freecodecamp.org/news/fzf-a-command-line-fuzzy-finder-missing-demo-a7de312403ff/
* can use for tab completion w/ `<cmd>**` https://www.freecodecamp.org/news/fzf-a-command-line-fuzzy-finder-missing-demo-a7de312403ff/ cant figure out yet how to ignore hidden dir in music-usb https://github.com/junegunn/fzf.vim/issues/453#issuecomment-526791474
* ignore files https://github.com/junegunn/fzf/issues/1625#issuecomment-507674106
* _alternatives_: dmenu https://eli.thegreenplace.net/2018/command-line-autocomplete-for-go-documentation/
* `--preview` unable to use the preview command despite following installation instructions https://github.com/junegunn/fzf#using-homebrew-or-linuxbrew https://github.com/junegunn/fzf/issues/1743 📍 https://github.com/junegunn/fzf/issues/1743#issuecomment-593052202
* _keybindings_: Emacs; ctrl j/k to scroll https://github.com/junegunn/fzf/issues/1716#issuecomment-542756200 but just type a few more char https://github.com/junegunn/fzf/issues/1716#issuecomment-542784884 more scroll bindings https://github.com/junegunn/fzf.vim/issues/211#issuecomment-497943378 https://github.com/junegunn/fzf.vim/issues/358#issuecomment-296737223 https://github.com/junegunn/fzf/blob/master/CHANGELOG.md#0152
* _Vim_: 🗄 `fzf.log`

## file list (exa)

📜 https://github.com/ogham/exa https://the.exa.website/

exa
* conf https://the.exa.website/docs/environment-variables
* no Git in grid view https://github.com/ogham/exa/issues/927
* grid-details aka long grid https://the.exa.website/features/long-view#long-grid
* long view without metadata https://the.exa.website/features/grid-view
* icons nerd font https://the.exa.website/features/icons

ls
* colorize https://danyspin97.org/blog/colorize-your-cli/
* https://github.com/Yash-Handa/logo-ls
* list number of dir/files in $CWD/subs: `tree | tail -1`
> so tree gives some output stats that exa's tree mode doesn't?

---

* exa will list `.gitignore` files with marker
```sh
.rw-r--r--@  459 zv_mac 14 Feb 12:02 -I accounts.md
.rw-r--r--@ 1.2k zv_mac 16 Feb 08:48 N- company.md
.rw-r--r--@ 4.8k zv_mac 16 Feb 08:49 N- eng.md
.rw-r--r--@ 2.5k zv_mac 16 Feb 07:57 N- onboarding.md
.rw-r--r--@ 9.4k zv_mac 16 Feb 09:28 N- payments.md
```
* `LS_COLORS`: var that controls output of ls, tree https://github.com/sharkdp/vivid
* no color https://news.ycombinator.com/item?id=30483417
* vivid https://github.com/sharkdp/vivid
use vivid with exa_colors https://github.com/mimame/.dotfiles/blob/b097b3dba50dc4ed7ff26886678392aa6926bed7/zsh/.zshrc#L152
🎗 `exa` already handles a bunch of filetypes for you https://the.exa.website/features/colours
* `exa` w/ `.gitignore`: smart enough to ignore everything in `.gitignore` if it's in the root directory, but `exa --tree` won't, so you have to add `.DS_Store` et al. via `exa -I`   https://github.com/ogham/exa/issues/136 https://github.com/ogham/exa/issues/408
256 color codes https://github.com/trapd00r/LS_COLORS https://github.com/search?q=exa_colors&type=Code https://www.howtogeek.com/307899/how-to-change-the-colors-of-directories-and-files-in-the-ls-command/

rf your bash profile https://github.com/search?q=exa_colors&type=Code
* color symlinks (or just use default purple)
* show .gitignored env files
* background - white: `export LS_COLORS="*.py=38;5;114;47"`
* foreground - pink: `38;5;213`
* foreground - coral: `38;5;114`

`fd`: doesn't need but could use exa if you wanted to https://github.com/sharkdp/fd/issues/222
`ls`: exa - color config https://the.exa.website/docs/colour-themes
`tree`: 1) use vivid https://github.com/sharkdp/vivid/issues/25 2) use exa's tree functionality https://the.exa.website/features/tree-view + exa color config https://the.exa.website/docs/colour-themes 
* tree can rm files as well https://codesolid.com/what-are-those-pyc-files-in-a-python-project/
```python
pyclean () {
        find . -type f -name "*.py[co]" -delete
        find . -type d -name "__pycache__" -delete
}
```

color output: `tput` https://stackoverflow.com/a/20983251/6813490

## file search (fd)

📜 https://github.com/sharkdp/fd

* snippets
```sh
-E <exclude>
-HI  # include hidden/.gitignore https://github.com/sharkdp/fd#fd-does-not-find-my-file
-d <depth>

wc -l <file>  # lines in file
ls | wc -l    # files in dir
# world count from all files in subdirectory (use scc for lines)
fd -t f | xargs bat | wc -w
# world count from all files in specified subdirectory
fd . "dir1/" "dir2/" -t f | xargs bat | wc -w
fd . "sw/" "za/" -t f | xargs bat | wc -w  # 226693

# https://missing.csail.mit.edu/2020/shell-tools/
# Delete all files with .tmp extension
find . -name '*.tmp' -exec rm {} \;
# Find all PNG files and convert them to JPG
find . -name '*.png' -exec convert {} {}.jpg \;
```

alternatives
* https://github.com/kashav/fsql
* fselect https://github.com/jhspetersson/fselect
```sh
# ordering
fselect path from /tmp order by size desc, name
# music
fselect duration, path from /home/user/music where genre = Rap and bitrate = 320 and mp3_year lt 2000  
fselect path, mime from /home/user where is_audio = 1
```

## file watch

* https://news.ycombinator.com/item?id=30736518
* entr https://github.com/eradman/entr https://jvns.ca/blog/2020/06/28/entr/ https://github.com/eradman/entr/issues/45 http://eradman.com/posts/repeatable-workspaces.html
* https://github.com/gorakhargosh/watchdog
* https://facebook.github.io/watchman/ https://adamj.eu/tech/2021/01/20/efficient-reloading-in-djangos-runserver-with-watchman
* https://github.com/watchexec/watchexec
* https://github.com/emcrisostomo/fswatch https://slack.engineering/development-environments-at-slack/
* https://vsoch.github.io/watchme/getting-started/
* https://github.com/cespare/reflex
* https://github.com/cortesi/modd
* https://github.com/wtetsu/gaze

## jobs (cron)

🗄 `distributed.md` TQ

nohup
* _nohup_: separates process and terminal https://unix.stackexchange.com/a/148698
* keeps process alive after terminal that started process is killed https://hacker-tools.github.io/remote-machines/
* appends to `nohup.out`
```sh
# keep alive https://github.com/Idnan/bash-guide#d-nohup
nohup <cmd>
# keep alive + run in background
nohup <cmd> &
```

---

* https://www.youtube.com/watch?v=AHAAA7zfT7Q
* _bg_: put job in background
* _fg_: put background job into foreground https://hacker-tools.github.io/shell/
* _&_: run in background
* _nq_: queuing commands https://github.com/leahneukirchen/nq
```sh
# build targets without occupying the terminal
$ nq make clean
$ nq make depends
$ nq make all
$ fq  # look at output without stopping the build
```

* https://www.twilio.com/blog/2017/04/wedding-at-scale-how-i-used-twilio-python-and-google-to-automate-my-wedding.html
* https://github.com/SkullTech/drymail
* https://github.com/caronc/apprise
* https://github.com/fonoster/fonos
* https://hacker-tools.github.io/automation/
* Python https://github.com/agronholm/apscheduler
* _anacron_: runs certain time after system start i.e. better for personal machine; 1 time/day
* _launchd_: macOS equivalent https://blog.bejarano.io/fixing-cron-jobs-in-mojave.html
* _batch_: runs when server load drops below specific level
* _Autosys_: tool for coordinating cron jobs; first heard about this 2017.11
* _monitoring_: https://github.com/healthchecks/healthchecks

* _cron_: expects specific time i.e. better for server; n times/day; `/etc/crontab` for system, `~/crontab` for user
* `crontab -e`: create crontab
* `crontab -l`: see active entries

* syntax https://www.youtube.com/watch?v=QZJ1drMQz1A&t=895s https://crontab.guru/
```sh
# 1-min(0-59) 2-hour 3-day(month) 4-month 5-day(week)
5 * * * *  # 5th minute of every hour, every day of month, every month, every day of week
```

## munge

🗄 `sql.md` munge

* _cut_: rm columns https://blog.balthazar-rouberol.com/text-processing-in-the-shell#cut https://kadekillary.work/post/cli-4-ds/ https://github.com/theryangeary/choose https://github.com/ibraheemdev/modern-unix
```sh
```
* _sort_: sort lines https://github.com/Idnan/bash-guide#j-sort https://kadekillary.work/post/cli-4-ds/ https://blog.balthazar-rouberol.com/text-processing-in-the-shell#sort
```sh
```
* _shuf_: https://neowaylabs.github.io/programming/unix-shell-for-data-scientists/
* _uniq_: rm dupes https://github.com/Idnan/bash-guide#l-uniq https://kadekillary.work/post/cli-4-ds/ https://blog.balthazar-rouberol.com/text-processing-in-the-shell#uniq
```sh
```

grouping
* _join_: SQL join on files https://kadekillary.work/post/cli-4-ds/
* _paste_: merge sorted files https://kadekillary.work/post/cli-4-ds/ https://blog.balthazar-rouberol.com/text-processing-in-the-shell#paste
```
```
* _split_: split file into chunks https://kadekillary.work/post/cli-4-ds/ https://tech.marksblogg.com/importing-data-from-s3-into-redshift.html

## pager (bat)

📜 https://github.com/sharkdp/bat

```sh
# specify stdin language
yaml2json .travis.yml | json_pp | bat -l json
# multiple
bat src/*.rs
```

---

* _pager_: print file
* cat https://twobithistory.org/2018/11/12/cat.html
* bat https://github.com/sharkdp/bat
* less https://danyspin97.org/blog/colorize-your-cli/
* https://github.com/sharkdp/bat#man https://danyspin97.org/blog/colorize-your-cli/ https://askubuntu.com/a/623996 🗄 `linux.md` man pages

* _create theme_: https://github.com/sharkdp/bat#adding-new-themes https://github.com/sharkdp/bat/blob/d65ae517dd868008ce72b37e30604e5480554571/.gitmodules
* _make default pager_: bp - `export MANPAGER=bat` https://askubuntu.com/a/679058
* doesn't deal w/ binary https://github.com/sharkdp/bat/issues/150 https://github.com/sharkdp/bat/issues/248
* can open multiple files 🗄 xargs
```sh
bat --line-range 227:236 $NOTES_DIR/sw/za/algos.md
```

## output

* _fold_: https://blog.balthazar-rouberol.com/text-processing-in-the-shell#fold
* _fmt_: fmt stdout https://github.com/Idnan/bash-guide#f-fmt

* stdout, stderr
```sh
# stderr to file
cmd &> file.log

# capture cmd output
OUTPUT="$(ls -1)"
echo "${OUTPUT}"

# redirect stderr to stdout
2>&1  # `&` marks `1` as a file descriptor vs. a file name https://stackoverflow.com/a/818284
```

## stream edit (sd)

🗄 `vim.md` argdo

* _sed_: stream editor = filter/transform text
* rm newline `sed "s/\r$//" file.txt > out.txt`
* _tr_: string edit e.g. case, add newline https://github.com/Idnan/bash-guide#k-tr https://shapeshed.com/unix-tr/ https://blog.balthazar-rouberol.com/text-processing-in-the-shell#tr

https://blog.balthazar-rouberol.com/text-processing-in-the-shell#sed
* sed = 看板 + now/next/done (what's the point of paging everything in queue?) https://stackoverflow.com/a/4824742
* https://jvns.ca/blog/2018/05/11/batch-editing-files-with-ed/

---

https://kadekillary.work/post/cli-4-ds/
* sd https://github.com/chmln/sd

🔗 https://www.digitalocean.com/community/tutorials/the-basics-of-using-the-sed-stream-editor-to-manipulate-text-in-linux
https://github.com/tanrax/maza-ad-blocking macOS version

* all but last line `sed \$d` https://stackoverflow.com/a/18127797/6813490
* _input_: reads (stdin, file) line by line
* _output_: to stdout by default
* syntax
```sh
sed <options> <commands> <input>
sed '' BSD  # no cmd i.e. just send to stdout
```
* print range: `sed -n '1,5p' bsd.txt` (specific) `sed -n '1,5p' bsd.txt` (relative)
* macOS version is BSD, which doesn't work with any further examples from article https://unix.stackexchange.com/a/13716/331460

## text search (ripgrep)

📜 https://github.com/BurntSushi/ripgrep/blob/master/GUIDE.md#basics

rg
* `-s` case-sensitive 🗄 `.bash_profile` mq
* `U` multiline-mode, necessary for regex 🗄 `.bash_profile` mq
* conf: set fs in profile `RIPGREP_CONFIG_PATH` https://github.com/BurntSushi/ripgrep/blob/master/GUIDE.md#configuration-file
```sh
# syntax
<query> <args> <dir>
# search hidden files
--hidden
# files with matches
<query> --files-with-matches
# see what files will be searched
<query> --files <dir>

###
# FILTER / GLOB https://github.com/BurntSushi/ripgrep/blob/master/GUIDE.md#manual-filtering-globs
# n.b. use single quotes on globs
# -uuu turn off automatic filtering https://github.com/BurntSushi/ripgrep/blob/master/GUIDE.md#automatic-filtering
###

# file types
--type-list  # get file types
<query> -g '*.py'  # only file type
<query> -g '!*.toml'  # exclude file type

# globbing
rg toil -g '*-tracking*'
rg bpython -g [Mm]akefile

# dir
<query> -g 'src/*'  # only incl single dir
<query> -g 'src/*' ; <query> -g 'src/*' # only incl multiple dir
<query> -g '!jay/*'  # exclude dir
```

---

* assign colors to matches https://github.com/arsham/blush
* metasearcher: files, file contents, email, Git (message, contents) https://simonwillison.net/2020/Nov/14/personal-data-warehouses/ 23:45 https://datasette.substack.com/p/dogsheep-personal-analytics-with
* pfdgrep apparently this is faster? https://github.com/phiresky/ripgrep-all)

grep
* colorize https://danyspin97.org/blog/colorize-your-cli/
* snippets
```sh
# version 📝 Linux uses GNU, Mac uses FreeBSD
grep --version

# find tab char https://stackoverflow.com/a/5694596
grep $'\t' <file>

# '<regex>' <file> 📝 good idea to use quotes here
grep 'user' /etc/passwd

# case insensitive. line numbers
grep -in 'first' foo.txt

# all files in directory
grep -r 'query' *
grep -ir sean 2019 * # from `logs`

# alias
grep --color=auto

# show lines __b__efore and __a__fter -> https://stackoverflow.com/a/9083/6813490
grep -B 3 -A 2 foo README.txt

# multiple queries --> https://unix.stackexchange.com/a/37316/331460
grep -E 'PROJECTS|venv' ~/.bash_profile

# line begins w/ query
grep '^user' /etc/passwd

# view single function def from `.bash_profile`
declare -f <name>

# view all function def
declare -f

# view all function names (regex = line starts with lower case characters)
declare -f | grep '^[a-z]'

# https://superuser.com/a/595699/728972
tree -if | grep <query>
```

# ZA

file/dir diff
* _vimdiff_: `vim -d <file1> <file2>` https://stackoverflow.com/a/113328/6813490
* wraps Vim's diff mode for use in other tools, notably Git's mergetool https://vi.stackexchange.com/a/626 https://www.youtube.com/watch?v=kFVjoIish0E
* _diff_: https://danyspin97.org/blog/colorize-your-cli/ diffing trees https://github.com/trailofbits/graphtage
* BeyondCompare https://scootersoftware.com/ https://news.ycombinator.com/item?id=22850711
* _difftastic_: diff + syntax https://github.com/Wilfred/difftastic

file name editing
* file manager (nnn, ranger, et al.)
* vimv https://news.ycombinator.com/item?id=13890944 https://github.com/thameera/vimv
* visidata https://www.visidata.org/blog/2020/ten/
* `fne` (bulk, dry run, default for youtube-dl)

globbing
* filename completion (vs. regex i.e. search text https://www.linuxjournal.com/content/globbing-and-regex-so-similar-so-different) [LPI 25] 
* aka wildcards
* `*`: anything 
* `?`: single char 
* `[]`: range; case-sensitive `cp [a-f]*.png` `rm 02[3-7].mp3`

redirects
* `>`: overwrite file
* `>>`: append to file https://askubuntu.com/a/731237
* `<`: use file as input; `sqlite3 local.db < schema.sql`; ❓ can also be used to test file existence? https://stackoverflow.com/a/50108745/6813490 other approaches https://stackoverflow.com/q/638975

cp
* dir: `cp -r <dir> <path/to>`
* dir but exclude `.git`_: `cmd --exclude=.git <source> <target>` https://stackoverflow.com/a/3672584
* dir contents: `cp -r <dir>/ <path/to>`

---

* live log view `tail -f foo.log`

check file exists `test -f ~/.netrc && echo "~/.netrc already exists"`
* copy output to clipboard : `<cmd> | pbcopy`
* copy file to clipboard: `pbcopy < ~/.ssh/id_rsa.pub`
* _ffmpeg_: video encoding, file format conversion https://www.youtube.com/watch?v=MPV7JXTWPWI
* get file duration https://www.youtube.com/watch?v=s6DXMf_yj64
* _rm_: `~/.Trash`; alternatives https://github.com/nivekuil/rip try this w/ newer version https://github.com/arsenetar/send2trash/issues https://github.com/arsenetar/send2trash/issues/56 https://hacker-tools.github.io/command-line/
* _which_: full path https://nil.wallyjones.com/what-shell-am-i-using/
* _xargs_: construct list of args for cmd (bc some cmds only take args, not stdin) https://thorstenball.com/blog/2012/10/24/command-line-ride/ https://www.oilshell.org/blog/2021/08/xargs.html
```sh
LOGS_DIR/20 $ fd tracking | tail -n 3 | xargs bat  # open 3 most recent tracking files
ls | sort -f | head -1 | xargs open  # kaiff - open first file in directory; used to open Youtube talks downloaded as pods
fd tracking | xargs rg music  # from logs/20 -> get tracking info for music
```

wild ideas
* Python from command line https://github.com/hauntsaninja/pyp https://github.com/python-mario/mario 
* pkg mgmt https://github.com/bpkg/bpkg 
* Bash as C# https://github.com/niieani/bash-oo-framework

* `LC_COLLATE`: determine sort order https://unix.stackexchange.com/q/75341/331460
* `head`: 类似 SQL `limit` e.g. `ls <query> | head -4` or `kaiff` (`ls | sort -f | head -1 | xargs open`) https://stackoverflow.com/a/14510257/6813490
* _alternatives_: Python, Perl, TCL https://news.ycombinator.com/item?id=23360338
* _$PWD_: output for `pwd`

* _declarative UNIX_: https://github.com/tfeldmann/organize 
* `export`: propagates variable to child processes [LPI 34] https://unix.stackexchange.com/a/209581/331460
* `file <file>`: info on encoding, if executable
* _free_: disk space `df` memory https://apple.stackexchange.com/q/4286/328389 or `duf` https://github.com/ibraheemdev/modern-unix
* `ls`: a (hidden files) l (perms) F (file type) S (size) t (sort on write timestamp); if there's a tenth character in the column `@` it’s something to do w/ ACL (access control list) on the file https://linux-audit.com/plus-sign-ls-output/
* `rm`: -i (prompt before each deletion) -R (answer yes to all prompts) -rf (knock out everything)
* test runner: https://chrismorgan.info/blog/make-and-git-dhttps://scootersoftware.com/iff-test-harness/ https://news.ycombinator.com/item?id=23268911
* df: free disk space
* free: free memory (`top` on macOS)
* [w](https://rachelbythebay.com/w/2018/03/26/w/)
* completion script https://iridakos.com/tutorials/2018/03/01/bash-programmable-completion-tutorial.html + https://github.com/pindexis/marker
* `.bashrc`: https://en.wikipedia.org/wiki/Run_commands
* `$EDITOR`: how os knows what to use to open text files https://github.com/dylanaraps/fff/issues/30#issuecomment-451484118 https://unix.stackexchange.com/a/251055/331460
* _tree_: ignore multiple https://unix.stackexchange.com/a/47806/331460 https://superuser.com/questions/772567/how-to-get-tree-a-to-ignore-git-directories
* unzip `.zip`: `unzip <file>`
* [rm binary data from text file](https://unix.stackexchange.com/a/353420/331460) + [view binary data in text file](https://unix.stackexchange.com/a/353421/331460)
* [live preview](https://github.com/akavel/up)
* [file extensions don't matter to program execution](https://askubuntu.com/a/764126)

## env var

* reference: `echo $SHELL`
* list: `env`
* rm: `unset <var>`
* set temporarily to run cmd: `DEBUG=true npm start`
* `envsubst`: sub env var into fmt strings https://nickjanetakis.com/blog/using-envsubst-to-merge-environment-variables-into-config-files
```sh
foo.sh  # echo $LOGNAME 
./foo.sh           # stdout: $LOGNAME
envsubst < foo.sh  # stdout: zach
```
* _direnv_: load env var based on dir https://jamey.thesharps.us/2019/05/29/per-project-postgres/ https://github.com/direnv/direnv

* macOS execution order: `.bash_profile`, `.bash_login`, `.profile`
* https://unix.stackexchange.com/a/106606/331460
* https://github.com/thoughtbot/til/blob/master/bash/bash_profile_vs_bashrc.md
🗄 `broot.log`

## profiles

🗄 `system.md` application config

* https://shreevatsa.wordpress.com/2008/03/30/zshbash-startup-files-loading-order-bashrc-zshrc-etc/

sourcing
* zsh automatically sources `.zprofile` and `.zshrc`
* bash automatically sources `.bash_profile`
* silence warning not to use bash `export BASH_SILENCE_DEPRECATION_WARNING=1` https://elisabethirgens.github.io/notes/2020/02/bye-bash/
* bash on zsh MacOS iTerm: profiles > command: (`bash`, `source ~/.bash_profile`)

shell types
* _interactive_: normal
* _non-interactive_: process spawned when script run 📙 LPI 2.2 https://unix.stackexchange.com/questions/43385/what-do-you-mean-by-interactive-shell/43389#43389 
* _login_: reads profiles and env var 
* _non-login_: cron jobs https://unix.stackexchange.com/questions/38175/difference-between-login-shell-and-non-login-shell/46856#46856 https://www.quora.com/What-are-the-differences-between-a-login-shell-and-a-non-login-shell/answer/Rod-Nussbaumer-1?srid=ebCJ

dotfiles
* prefer programs that store config as text
* keep under version control and symlink into place with script https://hacker-tools.github.io/dotfiles/ advanced mgmt https://github.com/twpayne/chezmoi https://news.ycombinator.com/item?id=32632533
> There are two basic approaches: version your entire home directory or symbolically link your dotfiles into place from a stand-alone repository. The first approach is straightforward but has a number of issues that make it a poor choice. https://nullprogram.com/blog/2012/06/23/
* install script https://www.youtube.com/watch?v=hXU54axdjJc https://alexpearce.me/2016/02/managing-dotfiles-with-stow/

---

* _system_: `/etc/profile` `/etc/bashrc` https://bencane.com/2013/09/16/understanding-a-little-more-about-etcprofile-and-etcbashrc/
* _login_: `~/.bash_profile` 
* _non-login_: `~/.bashrc` https://unix.stackexchange.com/a/3469/331460

alias
* _alias_: evaluated when shell loads profile
* use unaliased cmd: `\cd` https://stackoverflow.com/a/11056541
* view from cmd line w/ `type <alias>` https://www.youtube.com/watch?v=aLMepxvUj4s 4:15
