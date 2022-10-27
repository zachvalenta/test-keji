# TODO

## 参考

📜 
* https://vimhelp.org/usr_toc.txt.html https://www.vim.org/docs.php
* help: `:help vimrc-intro` `:h packages` https://vimtricks.substack.com/p/vimtricks-help-powerup 
* notation 📙 Neil practical xx
🔍 https://vi.stackexchange.com/
📚
* Neil modern vim
* Neil practical vim
* Robbins learning vim

## current

## queue

replace VSC
* color: bullets, braces
> newer version of Noctis doesn't change color after bullet, look at their changelog
* search/nav: goto file/tag, grep + preview
* syntax: code block syntax for Markdown https://vimtricks.com/p/highlight-syntax-inside-markdown/
* visual: ✅ Git gutter ✅ statusline ❌ tagbar -> ctags

## done

* _22_: built-in pkg mgmt
* _20_: VS Code (Markdown extensions break, install 1.41)
* _19_: VS Code, Vim (Neil practical vim 1.1-3, 2.7-9, 3.13-15, 4.20.22, 5.27.28, 8.47-53, 9.56-57 10.60-62)
* _18_: IntelliJ, PyCharm
* _17_: Eclipse
* _15_: Sublime

# TEXT

semantics
* _operator_: verb
* _motion_: mv w/in buffer 📙 Neil practical 113, 135
* _jump_: mv btw buffers 📙 Neil practical 135
* _text object_: pattern (paren pair, HTML tags) 📙 Neil practical 8.128

---

vocabulary
* _syntax_: operator + count + motion; order can change e.g. `3dd` for delete 3 lines [VT 2.6]
* _minimap_: sidebar that shows compressed version of buffer https://nova.app/
* _change_: anything from any mode that modifies text in document [PV 2.8]
* _macro_: save series of commands as single cmd https://hacker-tools.github.io/editors/ https://www.youtube.com/watch?v=futay9NjOac 📙 Neil practical ch. 11
* _word_: char, num, underscore [Neil pv 8.119]
* _WORD_: word but incl. delimiters [Neil pv 8.119]

substitute 📙 Neil practical ch. 14
```sh
# basic
:%s/this/that

# things you have to escape
:%s/\'/\"  # quotes
:%s/\ /\-  # white space
```
* all lines: `:%` [PV 5.28]
* last line: `:$`
* https://vimtricks.com/p/tag/replace/ https://vimtricks.substack.com/p/vimtrick-count-occurrences
* https://news.ycombinator.com/item?id=26285372
* current line_: `.` e.g. `:.s/\ /-/g` replace all spaces on line with hyphen https://stackoverflow.com/a/46181576/6813490
* https://github.com/osyo-manga/vim-over

* block cursor, line cursor (for insert mode) https://www.youtube.com/watch?v=FcQjTXLrVUU
* open URL under cursor https://vimtricks.com/p/open-url-under-cursor/
* highlight lines https://vimtricks.com/p/highlight-specific-lines/
* run cmd on every line https://vimtricks.com/p/operate-on-every-line/
* once you're in insert mode, stay there until you finish full edit so it's repeatable https://vimtricks.com/p/insert-mode-edit-mappings/
* comments https://vimtricks.com/p/commenting-code/ https://github.com/preservim/nerdcommenter https://github.com/tpope/vim-commentary https://www.semicolonandsons.com/episode/IDE-like-refactors-snippets-tests-hover-docs-commenting-and-git 4:00
* hidden char https://vimtricks.com/p/display-hidden-characters/
* snippets https://www.youtube.com/watch?v=Co4S_uJYb1o https://vimtricks.com/p/automated-file-templates/ https://www.youtube.com/watch?v=PJiOYNMOQ8M&lc=UgguwtLM8AsVcXgCoAEC https://www.youtube.com/watch?v=XA2WjJbmmoM 38:20 https://www.semicolonandsons.com/episode/IDE-like-refactors-snippets-tests-hover-docs-commenting-and-git 2:15 https://github.com/SirVer/ultisnips
* folding https://realpython.com/vim-and-python-a-match-made-in-heaven/#code-folding http://vimcasts.org/episodes/archive/
* mouse support `set mouse+=a`
* export visual as html https://stefanoborini.com/export-vim-text-with-colors-to-html/
* datetime: https://vimtricks.substack.com/p/insert-the-current-date-or-time
* design: available everywhere and modal (melodies not chords) [Neil pv xx] but Vimscript is meh and destructive tasks are easy
> The most important idea in Vim is that Vim’s interface itself is a programming language. Keystrokes (with mnemonic names) are commands, and these commands compose. https://missing.csail.mit.edu/2020/editors/
* new line: treated differently than other text editors https://stackoverflow.com/questions/15639511/vim-show-newline-at-the-end-of-file
* spell check: `:set spell/nospell` https://vimtricks.substack.com/p/vimtrick-spell-checking-in-vim http://vimcasts.org/episodes/archive/ https://www.youtube.com/watch?v=44pNDuRO77g
* remote editing https://vimtricks.substack.com/p/vimtrick-edit-files-remotely
* toggle relative line numbers https://vimtricks.substack.com/p/vimtrick-toggle-line-number-mode

* _leader_: create custom mappings [PV 8.122] https://stackoverflow.com/a/23503958 people typically map it to `,` https://news.ycombinator.com/item?id=24287951
* _line number mode_: https://vimtricks.substack.com/p/vimtrick-toggle-line-number-mode
* _mapping_: search https://vimtricks.substack.com/p/vimtrick-search-your-mappings
* _session_: https://jvns.ca/blog/2017/09/10/vim-sessions/ https://vimtricks.com/p/saving-session-state/ 📙 Neil modern ch. 6 https://rutar.org/writing/vim-session-management-an-introduction-to-fish/
* text expansion / abbreviations https://vimtricks.substack.com/p/vimtrick-type-less-with-abbreviations

* whitespace: flag https://realpython.com/vim-and-python-a-match-made-in-heaven/#flagging-unnecessary-whitespace trim https://vimtricks.substack.com/p/vimtrick-trim-trailing-whitespace tabs, spaces http://vimcasts.org/episodes/archive/
* text wrap http://vimcasts.org/episodes/archive/ format line length https://www.youtube.com/watch?v=a3yhIOelUCY
* show newline, invisible char http://vimcasts.org/episodes/show-invisibles/
* lists: quickfix, args https://vimtricks.substack.com/p/vimtrick-copy-from-quickfix-to-the 📙 Neil modern ch. 4

## normal

* run on every line https://www.getrevue.co/profile/vim_tricks/issues/operate-on-every-line-1181574
* `g_` mv to last normal char in line (vs. new line) https://stackoverflow.com/a/105734
* _case_: lower `gu` upper `gU` https://vimtricks.com/p/change-character-case/

📙 Neil practical 2.12
🔗 `:h motion.txt`
> clean these up

rf
* bubbling http://vimcasts.org/episodes/bubbling-text/ https://www.youtube.com/watch?v=gNyNm5DsQ88
* region selection https://vimtricks.substack.com/p/vimtrick-region-expanding
🎗 all motion are either inclusive or exclusive [`:h exclusive`]
jump to matching bracket: `%` show matching while in insert https://vimtricks.substack.com/p/vimtrick-highlight-matching-bracket
jump to next method `]m` https://vimtricks.substack.com/p/vimtrick-jump-to-next-method
* jump to top/btm of section `()`

## motions

* wrap: `gw`  https://vimtricks.substack.com/p/vimtrick-tidy-paragraphs
https://github.com/easymotion/vim-easymotion

 📍 operate until https://vimtricks.substack.com/p/vimtrick-operate-until-pattern

char
* _find by_: `t` (incl) `f` (ex); `;` (next) `,` (previous); for current line, cap for backwards
* _matching_: `%`
* _left/right_: `h/l`
* _left/right - insert_: `i/a` ('append')

file
* _start/end_: `gg/G`
* _goto_: `<num>G`
* _up/down_: `k/j`
* _start/end_: `0/$`
* _start/end - non-blank_: `^/g_`
* _start/end - insert_: `I/A`

https://stackoverflow.com/a/2281755/6813490
* current line - nudge: `ctrl e/y` https://vimtricks.substack.com/p/vimtrick-nudge-current-line-up-or
* current line - jump: `H` (top) `M` (mid) `L` (bottom)
* page (reposition): `zt` (top) `zz` (center) `zb` (bottom) https://vimtricks.substack.com/p/vimtrick-reposition-the-current-line config to keep cursor vertically centered https://vim.fandom.com/wiki/Keep_your_cursor_centered_vertically_on_the_screen
* page - half: `CTRL d/u`
* page - whole: `CTRL b/f`

word
* _forward to start_: `w`
* _forward to end_: `e` ('append')
* _back to start_: `b`
* _back to end_: `ge`

## operators

* _case_: `u` (lower) `U` (cap) -> think this is different than 'undo' bc need to select something first
* _change_: `c` (cut + insert mode) `cc` (line) `C` (to line end)
* _delete (cut)_ : `d` (operator pending)  `dd` (line) `D` (line end) `s` (char under cursor + insert)
* _dot_: `.` [PV 1.2] rewards repeatable changes [PV 2.9]
* _indent_: https://vimtricks.substack.com/p/vimtrick-indenting-code
* _open_: `O` (at current) `o` (below current VT 6.1)
* _put (paste)_: `P` (before) `p` (after); will swap if pasting over text highlighted in visual mode [PV 10.62] `CTRL r <register>` (put from register while inside insert mode) [PV 3.15]
* _redo_: `CTRL r`
* _replace_: `r` (char) `R` (word)
* _undo - individual_: `u` (single) `U` (line) `ctrl u` (stay in insert mode) https://vimtricks.com/p/undo-from-insert-mode/ https://news.ycombinator.com/item?id=18901621 https://vimtricks.substack.com/p/vimtrick-time-travel-in-vim
* _yank (copy)_: `y` (+ motion) `yy`/`Y` (line) https://vimtricks.com/p/copy-from-above-or-below/
yank by line number without moving https://vimtricks.com/p/copying-and-pasting-lines/

## registers

* _register_: container that holds text [Neil pv 10.62]
* _system register_: used by os
* aka clipboard 📙 Neil pv 10.62
* avoid overwrite https://www.youtube.com/watch?v=JU8g1-j2jd8
* _unnamed register_: not addressable by char/num https://vimtricks.com/p/pasting-multiple-times/

* list registers `:reg`
* address register `"<reg>`
* system register `"+` (`*` on macOS) https://realpython.com/vim-and-python-a-match-made-in-heaven/#system-clipboard

actions https://vimtricks.com/p/pasting-multiple-times/
* yank: copies text to both unnamed register and 0 register
* paste: copies text pasted over into unnamed register but doesn't touch 0 register

When I copy text with y, Vim puts it in the unnamed register and the 0 register. Both those registers contain the same thing.
When I paste over with p, Vim puts what I pasted over into the unnamed register but the 0 register still contains my original yanked text.
That means that if I paste with p, I’ll get the last thing I pasted over but if I paste with "0p, then I’ll paste with the last yanked text. Which is exactly what we want!

---

registers http://vimcasts.org/episodes/archive/

changelist http://vimcasts.org/episodes/archive/
* undolist https://vi.stackexchange.com/a/26309
* list of recent edits; per buffer [9.57]
* _changelist - p/n_: `g;`/`g,`
* view all  https://vimtricks.substack.com/p/vimtrick-jump-between-changes

jumplist http://vimcasts.org/episodes/archive/ https://www.getrevue.co/profile/vim_tricks/issues/the-vim-jump-list-1401966
* list of recent jumps (move btw files, long-range motions) [PV 9.56] per window [PV 9.57]
* _jumplist - list_: `:jumps`
* _jumplist - p/n_: `<C-o>/<C-i>`
> for some reason if you want to go back to where you were before searching `ctrl o` works https://www.cyberciti.biz/faq/unix-linux-vim-go-back-to-last-cursor-position/

https://vimtricks.com/p/improving-usage-of-registers/
* _VS Code Vim_: using default register across windows https://github.com/VSCodeVim/Vim/issues/4197
* _put (paste)_: `P` (before) `p` (after); will swap if pasting over text highlighted in visual mode [PV 10.62] `CTRL r <register>` (put from register while inside insert mode) [PV 3.15]
* 📝 there are a few registers whose values (current file, last searched text) are read-only [PV 10.62]
* can paste from system register into Vim as well https://vimtricks.substack.com/p/vimtrick-the-clipboard-register
* https://vimtricks.substack.com/p/vimtricks-command-mode-paste
* https://vimtricks.com/p/pasting-multiple-times/
* https://vimtricks.substack.com/p/vimtricks-avoid-paste-formatting
* https://vimtricks.com/p/go-to-next-match-and-select/
* [PV 10.61]

# UTILS

* YAML https://martinheinz.dev/blog/75

## code completion

🗄
* `language.md` language server
* `shell.md` tab completion

* YouCompleteMe https://realpython.com/vim-and-python-a-match-made-in-heaven/#auto-complete 
* https://www.youtube.com/watch?v=XA2WjJbmmoM 24:30
* https://github.com/neoclide/coc.nvim https://www.youtube.com/watch?v=gnupOrSEikQ
* 📙 Neil practical ch. 19 find virtualenv https://realpython.com/vim-and-python-a-match-made-in-heaven/#virtualenv-support 
* https://stackoverflow.com/questions/7138039/vim-autocomplete-for-python https://stackoverflow.com/questions/905005/python-and-intellisense https://www.youtube.com/watch?v=2f8h45YR494 https://www.youtube.com/watch?v=2f8h45YR494 https://www.semicolonandsons.com/episode/vim-autocomplete-overview https://vimtricks.com/p/autocomplete-word-for-word/ https://www.youtube.com/watch?v=ZzyY_9SMfeY https://pmihaylov.com/vim-for-go-development/
* autocorrect/spellcheck thesaurus, dictionary 📙 Neil practical ch. 20 https://www.youtube.com/watch?v=3TX3kV3TICU https://github.com/preservim/vim-lexical https://github.com/preservim/vim-litecorrect https://github.com/preservim/vim-wordy grammar https://www.youtube.com/watch?v=tIvdLeeW6pM https://github.com/caderek/gramma https://github.com/languagetool-org/languagetool
* linting https://github.com/errata-ai/vale

## color

* VS Code theme https://github.com/liviuschera/noctis 🗄 `sw/vim/vs-code-colorscheme.png`
* Markdown scoping 🗄 `education.md` note-taking
```md
# CHILD
## GRANDCHILD
great grandchild
* _item_: foo
* sub-item 1
* sub-item 2
* _item_: bar
```

colorthemes (gruvbox)
* gruvbox https://github.com/morhetz/gruvbox https://www.youtube.com/watch?v=h509rn2xIyU
* material
* vividchalk https://github.com/tpope/vim-vividchalk

---

* find Noctis color file
* BYO https://github.com/tpope/vim-vividchalk/tree/master/colors
https://rigel.netlify.app/
Markdown 
* vertical align Markdown tables https://vimtricks.com/p/vertical-alignment/ https://www.youtube.com/watch?v=XdDUGAePASA tabular http://vimcasts.org/episodes/aligning-text-with-tabular-vim/
* full setup https://www.swamphogg.com/2015/vim-setup/ https://vimvalley.com/replacing-scrivener-with-emacs-and-vim/

color
* bullets https://stackoverflow.com/questions/28665317/how-can-i-customize-comment-marker-in-vim https://stackoverflow.com/questions/10686792/how-to-color-specified-text-in-vim
* syntax file https://arnaudr.io/2020/08/17/modify-vim-syntax-files-for-your-taste/ https://vim.fandom.com/wiki/Creating_your_own_syntax_files
* keyword file, `keywordAs` https://vi.stackexchange.com/questions/34556/using-a-vim-syntax-file-i-would-like-some-keywords-such-as-to-be-colored
* colorscheme https://vi.stackexchange.com/questions/2782/how-can-i-create-my-own-colorscheme https://gist.github.com/romainl/5cd2f4ec222805f49eca https://github.com/flazz/vim-colorschemes https://stackoverflow.com/questions/7331940/how-to-get-the-list-of-all-installed-color-schemes-in-vim 📙 Robbins 195
* `.vim/colors` https://github.com/tomasr/molokai  https://www.freecodecamp.org/news/vimrc-configuration-guide-customize-your-vim-editor/
* DIY https://alvinalexander.com/linux/vi-vim-editor-color-scheme-syntax/
* pkgs https://github.com/kaicataldo/material.vim https://github.com/preservim/vim-thematic https://github.com/nanotech/jellybeans.vim
* "writing mode" e.g. iA Writer https://github.com/preservim/vim-pencil https://github.com/preservim/vim-colors-pencil
* change fmt on insert mode
```conf
# https://vim.fandom.com/wiki/Avoid_the_escape_key
# https://www.youtube.com/watch?v=9FECnDJShMk
:inoremap kj <Esc> 
:cnoremap kj <Esc>
# https://sanctum.geek.nz/arabesque/vim-anti-patterns/
inoremap jj <Esc>
```

* `:set <val>/<noval>`: toggle boolean on/off
* _modeline_: config options at top of file read by Vim only; typically for one-off where you don't want to update Vim config for that file type
> unsure why this still shows up in vimrc [https://www.youtube.com/watch?v=XA2WjJbmmoM 5:30 PV xxv]
* _examples_: https://github.com/tpope/vim-sensible https://grahamlyons.com/article/why-my-development-environment-is-the-best https://github.com/romainl/idiomatic-vimrc https://www.youtube.com/watch?v=hw5YsoX242Y
* Python https://realpython.com/vim-and-python-a-match-made-in-heaven/#syntax-checkinghighlighting
* syntax: https://github.com/vim-syntastic/syntastic columns for Python https://vimtricks.substack.com/p/vimtrick-column-highlighting Python indentation https://realpython.com/vim-and-python-a-match-made-in-heaven/#python-indentation

## config

📙
* Neil modern ch. 7
* Neil practical appendix

```sh
# autocmd: hook 📙 Neil practical 306 https://www.youtube.com/watch?v=nwCqb074qZE
# e.g. on Bufread, set scrolloff
# use to set file type e.g. you want Python syntax highlighting for .txt files https://www.youtube.com/watch?v=hrbV5WGxxdY
:autocmd BufRead /Users/zach/Desktop/zvmac/notes/sw/za/industry.md set scrolloff=999
```

set from shell
* set conf: `:set <val>`
* view values diff than default: `:set`
* find out where value was set: `:verbose set <value>`
* view available settings: `:options`
* no conf: `vim -u NONE` [PV xxiv]
* specific conf: `vim -u path/to/conf` [PV xxiv]
* disable vi compatability: `vim -N`; since Vim 8 this is the default but people typically still specific in config via `nocompatible`
* hiddne https://vimtricks.com/p/what-is-set-hidden/

files
* `~/.vimrc`: most common; initialization commands
* update on the fly http://vimcasts.org/episodes/updating-your-vimrc-file-on-the-fly/
* lint http://vimcasts.org/episodes/neovim-checkhealth/
* `MYVIMRC`: load from alternate location https://stackoverflow.com/a/4618301
* `~/.vim/`: plugins, color schemes, language-specific conf -> https://github.com/mrnugget/vimconfig
* `~/.gvimrc`: graphics settings (font, window size)
* hierarchy: `vim --version`
* config per project https://vimtricks.com/p/local-vimrc-files/
* config per file type https://vimtricks.com/p/per-file-type-configs/

## ctags

📍
* _tag_: scope-defining keywords in your programming language https://www.youtube.com/watch?v=XA2WjJbmmoM 3:50
* _ctags_: index of tags https://en.wikipedia.org/wiki/Ctags https://www.youtube.com/watch?v=JWD1Fpdd4Pc&t=338s 7:30 🗄 `db.md` index

---

* comby, sourcegraph https://comby.dev/ https://www.thoughtworks.com/radar/tools?blipid=202110077
* https://news.ycombinator.com/item?id=30819579
* https://www.semicolonandsons.com/episode/Fluent-File-Navigation
* https://www.youtube.com/watch?v=4f3AENLrdYo 
* https://www.youtube.com/watch?v=XA2WjJbmmoM 16:15
* https://www.youtube.com/watch?v=MP-FxMl0frk
* https://thoughtbot.com/upcase/navigating-ruby-files-with-vim
* https://thoughtbot.com/upcase/vim
* https://vimtricks.substack.com/p/vimtrick-open-file-to-line
* https://vimtricks.substack.com/p/vimtrick-open-to-a-pattern
* https://github.blog/2021-12-09-introducing-stack-graphs/

## file explorer (vifm)

🗄 `shell.md` file explorer

* CoC: https://www.youtube.com/watch?v=0kNYR40EcGM
* fern: https://www.youtube.com/watch?v=YpzIhRoZ-tk
* NerdTree: 

netrw
* https://www.youtube.com/watch?v=nDGhjk4Eqbc https://vimtricks.substack.com/p/vimtrick-filesystem-exploration http://vimcasts.org/episodes/the-file-explorer/ https://www.youtube.com/watch?v=XA2WjJbmmoM 34:30
* create files https://vimtricks.com/p/creating-files-and-directories/
* _file - fuzzy_: `:b <name>` https://drewdevault.com/2020/12/12/Shell-literacy.html https://github.com/ctrlpvim/ctrlp.vim https://www.youtube.com/watch?v=gnupOrSEikQ
* _file - previous_: `:bp`
* _file - open_: `:e path/to/file` (from within Vim)
* _file - list_: `:e .`
* _directory - set_: `:cd path/to/dir` (allows us to open files using relative paths)
* _directory - print_: `:pwd`

## file goto (fzf)

🗄 `shell.md` file goto
📙 Neil modern ch. 3

* https://www.youtube.com/watch?v=XA2WjJbmmoM 06:45
* https://github.com/ctrlpvim/ctrlp.vim
* https://github.com/mileszs/ack.vim
* `:vimgrep` http://vimcasts.org/episodes/archive/
* https://www.freecodecamp.org/news/fzf-a-command-line-fuzzy-finder-missing-demo-a7de312403ff/
* https://www.youtube.com/watch?v=kFNFlbiIeJM
* https://github.com/wincent/command-t
* https://github.com/wincent/ferret

## packaging

🔍 https://vimawesome.com/
📙
* Neil modern ch. 2
* Neil practical appendix

* _plugin_: Vimscript pkg loaded when Vim starts
* can impl using other languages e.g. Python https://www.youtube.com/watch?v=vMAeYp8mX_M
* scope: global, filetype (aka 'ftplugin' https://www.swamphogg.com/2015/vim-setup/ https://thoughtbot.com/upcase/videos/intro-to-dotfiles)

mgmt
* _vim-plug_: easy uninstall/rollback
* _minpac_: built-in for Vim 8/Neovim but everyone still using vim-plug https://rigel.netlify.com/#vim https://www.reddit.com/r/vim/comments/6x64oh/vim_8_any_reason_to_use_the_buildin_package/ https://github.com/k-takata/minpac https://danielmiessler.com/blog/vim-configuration-update-2019-version 
* _pathogen_: Tim Pope says to just use built-in
* _built-in_: just `git clone` to file location https://vimtricks.substack.com/p/vimtrick-plugin-installation
* default read pkg from `~/.vim/pack/*/start`
* can avoid `start` dir by specifying what to load in `.vimrc` with `:packadd plugin-name`
```sh
# or just pack/vendor/start for everything
├── $HOME/.vim/pack
│   └── color
│   └──── start
│   └────── pkg1
│   └────── pkg2
│   └── git
│   └──── start
│   └────── pkg3
│   └────── pkg4
```

statusline (lightline)
* _statusline_: prompt for window https://github.com/vim-airline/vim-airline 📙 Neil modern 133
* BYO https://jdhao.github.io/2019/11/03/vim_custom_statusline
* pkgs https://github.com/itchyny/lightline.vim https://github.com/vim-airline/vim-airline https://github.com/powerline/powerline

visual
* 🎗 eventually pull `colors` in here
* ✅ Git gutter https://github.com/airblade/vim-gitgutter
* 📍 tagbar: https://github.com/preservim/tagbar
> needs ctags impl https://github.com/universal-ctags/ctags https://www.youtube.com/watch?v=s0Bimr1079A

za
* autoclose/autopair for backticks and quotes https://github.com/tpope/vim-surround https://www.youtube.com/watch?v=_hbvvBgXlBo
* csv https://github.com/chrisbra/csv.vim
* undo https://github.com/sjl/gundo.vim

## search / nav

🗄 `shell.md` filter, nav
📙
* Neil modern ch. 3
* Neil practical ch. 16/18

how I current use VSC
* fuzzy search file: CMD p
* fuzzy search header - file: CMD r
* fuzzy search header - global: CMD t
* search: CMD CTRL f
* reopen previous buffer: CMD SHIFT t

open file at
* _mark_: bookmark w/in file https://vimtricks.com/p/bookmark-frequent-locations/
* section: `vim +/'## profile'`
* tag https://www.youtube.com/watch?v=pt36X1OJRG4 2:20
* line number https://www.youtube.com/watch?v=pt36X1OJRG4 2:45 https://stackoverflow.com/q/39232615/6813490 https://www.cyberciti.biz/faq/linux-unix-command-open-file-linenumber-function/ last line: `alias qu='vim "+normal G$" ~/Desktop/music-queue.md'` https://edunham.net/2015/01/29/vim_open_file_with_cursor_at_the_end.html https://www.youtube.com/watch?v=kAAGEx8deM8
* string https://www.youtube.com/watch?v=pt36X1OJRG4 3:15

---

* non-greedy https://www.getrevue.co/profile/vim_tricks/issues/non-greedy-regex-in-vim-1106742
* https://github.com/preservim/vim-markdown
❓ Vim emulation seems to default to smart-case like ripgrep but Vim itself no
https://vimtricks.com/p/navigating-around-the-screen/

search 📙 Neil practical ch. 13
*  https://vimtricks.substack.com/p/vimtrick-search-project-for-current
* previous search: `/` `ctrl p` https://vi.stackexchange.com/a/10340
* _start_: `/` [PV 10.51]
* _n/p_: `n`/`N`
* _under cursor - n/p_: `*`/`#`
* _smartcase_: only case sensitive if query contains caps; ignore with `\query\C` https://stackoverflow.com/a/2287449
* clear highlight https://vimtricks.com/p/clear-search-highlight/

* file manager https://github.com/scrooloose/nerdtree fern https://www.youtube.com/watch?v=oFc2kr734rs https://www.youtube.com/watch?v=dL2J0TtdCRk
* bat + fsf for preview https://www.youtube.com/watch?v=zbguTldYkCw 3:30

# ZA

version
* use Homebrew https://www.vim.org/download.php
* M1 macs come with Vim installed
* `vim --version`

modes
* _normal_: motions
* _insert_: actually writing
* _command line_: anything preceded by `:` 📙 Neil practical 5.27
* _operator-pending_: 📙 Neil practical 2.12
* _visual_: https://www.getrevue.co/profile/vim_tricks/issues/edit-multiple-lines-at-once-1221503 📙 Neil practical 8.52
* `V` (linewise) `v` (characterwise) indent (viz + `< / >`) surround (highlight + `S` + char https://stackoverflow.com/a/50687836/6813490) `o` restart selection https://vimtricks.substack.com/p/vimtrick-editing-visual-selections

history
* stone age: no screen = teletype
* 1969: ed https://begriffs.com/posts/2019-07-19-history-use-vim.html
* 1976: screens = ex, Vi, Emacs https://lwn.net/Articles/832429/ https://two-wrongs.com/why-you-should-buy-into-the-emacs-platform https://two-wrongs.com/on-escape-meta-alt-control-shift-emacs.html https://github.com/hlissner/doom-emacs
* 1991: Vim https://twobithistory.org/2018/08/05/where-vim-came-from.html https://begriffs.com/posts/2019-07-19-history-use-vim.html
* 2006: Vim 7.0
* 2013: Vim 8.0 [PV 5.27]

Neovim 📙 Neil modern
> Bram's comparison is Vi, Neovim teams' comparison is VS Code. https://news.ycombinator.com/item?id=31936725
* design: Lua for scripting, run tasks async https://www.lucasfcosta.com/2019/02/10/terminal-guide-2019.html
* libraries https://www.youtube.com/c/ChrisAtMachine/videos
* distros: https://github.com/SpaceVim/SpaceVim

## command line

📙 Neil practice ch. 5

* scroll cmd history: `: + arrow`
* search: `:<start_of_cmd> + arrow` https://vim.fandom.com/wiki/Using_command-line_history
* open stdin: `cmd | vim -` e.g. `\ls | vim -` for file editing https://vim.fandom.com/wiki/Bulk_rename_files_with_Vim
* can run terminal emulator inside buffer http://vimcasts.org/episodes/neovim-terminal/ 📙 Neil modern ch. 5, 130

---

* http://vimcasts.org/episodes/refining-search-patterns-with-the-command-line-window/
* argdo https://www.youtube.com/watch?v=futay9NjOac http://vimcasts.org/episodes/archive/
https://www.semicolonandsons.com/episode/Vim's-Versatile-CLI

* execute over a range of lines, aka ex cmds [PV 5.intro]
* enter: `:` or `/` [PV 5.intro]
* exit: `esc`
* view history https://vimtricks.substack.com/p/vimtrick-view-your-history-from-command
* quit and discard: `:q!`
* https://vimtricks.com/p/operate-across-files-by-name/

* _substitute_: `:%s/<old>/<new>` [PV 5.58] repeat https://vimtricks.substack.com/p/vimtrick-repeat-the-last-substitution across files https://vimtricks.substack.com/p/vimtrick-replace-across-files
* _global_: `:%s/<old>/<new>/g` [PV 5.58]
can also use to delete lines https://vimtricks.substack.com/p/vimtrick-remove-lines-matching-pattern

## splits

📙 Neil practice ch. 6-7

* vs. tabs https://www.youtube.com/watch?v=ZlyiNuxlkJY
* size https://vimtricks.com/p/splitting-to-a-specific-size/
* maximize https://vimtricks.com/p/maximize-the-current-split/
* split all files in dir https://vimtricks.substack.com/p/vimtrick-open-all-files-in-a-directory
* equalize https://vimtricks.substack.com/p/vimtrick-equalize-your-splits
* split to a line https://vimtricks.substack.com/p/vimtrick-split-to-a-line
* https://vimtricks.substack.com/p/vimtrick-moving-splits
* https://vimtricks.substack.com/p/vimtrick-change-split-orientation
```.vimrc
"split navigation
nnoremap <C-J> <C-W><C-J>
nnoremap <C-K> <C-W><C-K>
nnoremap <C-L> <C-W><C-L>
nnoremap <C-H> <C-W><C-H>
```

## windows

📍 http://vimcasts.org/episodes/archive/

* _file_: on disk
* _buffer_: file in memory 📙 Neil practical 6.84
* _viewport_: what's in view 📙 Neil practical 6.92 https://developer.mozilla.org/en-US/docs/Web/CSS/Viewport_concepts https://vimtricks.com/p/navigating-around-the-screen/
* _window_: viewport onto buffer 📙 Neil practical 6.92

tabs
* _tab_: 
* use tabs to encapsulate diff types of files e.g. business logic vs. immediate files https://www.youtube.com/watch?v=hbs7tuwpgZA 5:00

# 💀

## PyCharm

* _find action (god command)_: CMD SHIFT a
* _problems_: sometimes doesn't display *any* directories properly and you need to close IDE and blow away `.idea` dir and restart IDE, ignore dir in search is flaky
* _keymap schemes_: macOS (what the keymap reference PDF shows) OS-agnostic (what you'd be used to if you use other JetBrains IDEs)
* _sink_: https://github.com/JetBrains/awesome-pycharm https://www.youtube.com/playlist?list=PLQ176FUIyIUZ1mwB-uImQE-gmkwzjNLjP
* _settings - global_ | CMD ,
* _settings - project_ | CMD ;
* _editor font_: preferences > editor > font
* _default dir to open projects_: appearance > system settings
* _editor config_: `code style`
* [change file association](https://intellij-support.jetbrains.com/hc/en-us/community/posts/206237949-Change-file-association-manually)
* [turn off spell check](https://stackoverflow.com/a/2298724/6813490)
* visual guide for line length: `preferences > code style`
* ignore PEP8 error code in Pycharm: `preferences > inspections > Python > PEP8 > 'ignore errors` > add 'E5' (for line length)
* [show current file being edited in project window](https://stackoverflow.com/a/36738303/6813490)
* spaces instead of tabs: `editor > code style > Python` uncheck `use tab character` --> then do 'reformat code' in file to go from [tabs to spaces](https://stackoverflow.com/a/11816221/6813490)
* ['speed search'](https://www.jetbrains.com/help/phpstorm/speed-search-in-the-tool-windows.html) i.e. fuzzy search once inside project window
* exclude file (from inspections, code completion): [project structure](https://www.jetbrains.com/help/pycharm/excluding-files-from-projects.html)
* need `localhost` in `etc/hosts` to use console https://stackoverflow.com/a/41345334/6813490
* config interpreter to venv: `pref > project > interpreter > venv/bin/python_interpreter` ['Django Fundamentals']
* settings: `~/Library/Preferences/<PyCharmEdition>`
* launcher script: open dir/file from CLI; 'Tools | Create Command-Line Launcher'
* [can be discrepancy btw PyCharm and terminal](https://stackoverflow.com/q/31348711/6813490) about whether your imports are done correctly; potential resolution [here](https://stackoverflow.com/a/21241988/6813490)

editor
* _line_: CMD l (`main menu > navigate`)
* _tab - by number_: CMD # (GoToTabs plugin)
* _tab - scroll ('select next tab')_ : `CMD ALT arrow`
* _method - search_: ALT m https://stackoverflow.com/a/3992371/6813490
* _method - next/previous_: CMD SHIFT arrow
* _un/fold - single_: CMD +/-
* _un/fold -  all_: CMD SHIFT +/-

project
* _project - close_: CMD SHIFT w
* _project - open_: CMD SHIFT o
* _project - open recent_: CMD ALT o
* _pane - split_: CMD ALT s https://vimtricks.com/p/close-all-other-splits/ https://vimtricks.com/p/open-file-in-a-split/ https://vimtricks.com/p/open-vim-and-split-files/ https://vimtricks.com/p/navigating-splits/
* _pane - switch ('splitter')_: CMD ALT j/k
* _function - declaration_: CMD b
* _function - usage_: CMD u
* _search - class_: CMD n
* _search - text ('find in path')_: CMD SHIFT f

windows
* show current editor file in sidebar via 'Autoscroll from source' in project window settings
* _windows + recent files_ | CMD e
* _editor_: ESC (when in other windows)
* _project_: ALT 1
* _shell - Bash_: ALT 2
* _shell - Python_: ALT 3 (close w/ ALT w)
* _find_: ALT 4
* _structure_: ALT 8
* _TODO_: ALT 9

edit
* _code completion_: SHIFT RETURN
* _quick fix_: ALT RETURN
* _comment_: CMD /
* _line - cut_:  CMD x
* _line - move_ | CMD arrows
* _refactor_ | CMD SHIFT r
* _select - next occurence_: 📍
* _select - all occurences_: 📍
* _undo/redo_ | CMD z / CMD SHIFT z

## VSC

🔗 UI https://code.visualstudio.com/docs/getstarted/userinterface

* outline view: sort by postition, follow cursor
* _workspace_: dir that VS Code knows about; create `code <dir>`

downsides
* update perils https://github.com/microsoft/vscode/issues/142451
* search randomly breaks
* versions (1.41 broke Markdown extensions, seems unsustainable to run older)
* outline view too verbose
* still bloated (console, terminal, version control)
* GUI
* MS product https://news.ycombinator.com/item?id=28812486

misc
* upsides: completion, Vim emulation, less memory usage and better community than Sublime w/ less bloat than PyCharm, same editor for notes and code, merge requests, Markdown formatting (outline for inline code w/ 1.41 is nice), respect gitignore on file search
* views: command pallete, editor, sidebar
* remote development: think this requires src on remote itself vs. Pycharm (which afaik you edit locally and autodeploys to remote on save and runs interpreter there) https://code.visualstudio.com/docs/remote/remote-overview have to repoint `python.venvPath` (settings.json) and `git.path` (ssh settings)
* on path `ln -s /Applications/Visual\ Studio\ Code.app/Contents/Resources/app/bin/code /usr/local/bin/vsc`

extensions
* previous breaks from Markdown extensions https://github.com/mdickin/vscode-markdown-shortcuts/issues/60 https://github.com/mdickin/vscode-markdown-shortcuts/issues/59 https://github.com/yzhang-gh/vscode-markdown/issues/578
* freeze: `alias vscfr="ls ~/.vscode/extensions/ > $DOTFILES_DIR/vsc-pkg.txt"`
* rollback version https://stackoverflow.com/questions/42626065/vs-code-rollback-extension-install-specific-extension-version
* Makefile: ecosystem could use one just for goto https://github.com/microsoft/vscode/issues/47098 outline support https://github.com/microsoft/vscode/issues/81069 there's another extension that tries to run Makefile targets, mine just provides goto symbol and outline support (with prereqs) https://marketplace.visualstudio.com/items?itemName=technosophos.vscode-make&ssr=false
* Markdown: auto-close, bold/italic (independent of cursor location in word)

config
* _file locations_: config home `~/Library/Application Support/Code/User/` conf `settings.json` keys `keybindings.json` snippets `/snippets` https://stackoverflow.com/a/45910856
* exclude dir from search `search.exclude` https://stackoverflow.com/a/33418660/6813490
* file explorer outline follow cursor, sort by position, levels of nesting https://github.com/Microsoft/vscode/issues/54941 https://github.com/Microsoft/vscode/issues/58095
* relative line number for Vim https://github.com/VSCodeVim/Vim/issues/423
* workaround for VSC Docker extension popup https://github.com/Microsoft/vscode-docker/issues/150#issuecomment-462079524
* clickable URLs https://github.com/Microsoft/vscode/issues/68333
* Markdown: autoclose for backticks and quotes https://github.com/Microsoft/vscode/issues/38352 bold w/ double underscore https://github.com/mdickin/vscode-markdown-shortcuts/issues/57 https://github.com/mdickin/vscode-markdown-shortcuts/issues/58
* open tabs to far right https://stackoverflow.com/a/46865080
* open links w/ keybinding https://github.com/microsoft/vscode/issues/68333
```json
{
    "key": "cmd+alt+enter",
    "command": "editor.action.openLink"
}
```
* finding Python envs https://github.com/microsoft/vscode-python/issues/8372 stuck on recently used w/ Poetry https://github.com/microsoft/vscode-python/issues/9826
* _code completion and virtual environment_:  does it really work? or just using globally installed pkg? https://realpython.com/python-development-visual-studio-code/ manually set https://code.visualstudio.com/docs/getstarted/settings#_settings-file-locations https://code.visualstudio.com/docs/python/environments#_manually-specify-an-interpreter https://stackoverflow.com/questions/40377654/how-to-create-and-init-vscode-in-vscode

Markdown Shortcuts
* stars: 50
* italics break for VSC version 1.41 https://github.com/mdickin/vscode-markdown-shortcuts/issues/60 https://github.com/mdickin/vscode-markdown-shortcuts/issues/59 workaround https://github.com/mdickin/vscode-markdown-shortcuts/issues/60#issuecomment-656971750
* slow maintenance cycle https://github.com/mdickin/vscode-markdown-shortcuts/issues/57 
* use double underscore for bold https://github.com/mdickin/vscode-markdown-shortcuts/issues/49 
* bold depends on highlighting word first https://github.com/mdickin/vscode-markdown-shortcuts/issues/58

Markdown All in One
* stars: 1.2k
* todo: latest version w/ VSC 1.41, shortcuts/settings for bold (might need PR to add user setting for bold indicator)
* bindings: bold/italic `cmd b/i` check `alt c`
* slow for 1k+ LOC files https://github.com/yzhang-gh/vscode-markdown/issues/578
* only allows config of italics, not bold https://github.com/yzhang-gh/vscode-markdown/search?q=markdown.extension.italic.indicator&unscoped_q=markdown.extension.italic.indicator https://github.com/yzhang-gh/vscode-markdown/issues/571 https://github.com/yzhang-gh/vscode-markdown/issues/325
```json
// Markdown All in One - only for italics
"markdown.extension.italic.indicator": "_",
// Markdown Shortcuts - for bold as well
"markdownShortcuts.bold.marker": "__",
```

reinstall
* rm old using App Cleaner
* install
* disable plugins you only use occasionally
* outline view: follow cursor, sort by position
* color theme
* symlink to `dotfiles`
```sh
# path/to/Code/User
ln -sf "/Users/zach/Desktop/zvmac/materials/sw/os/za/dotfiles/settings.json" "/Users/zach/Library/Application Support/Code/User/settings.json"
ln -sf "/Users/zach/Desktop/zvmac/materials/sw/os/za/dotfiles/keybindings.json" "/Users/zach/Library/Application Support/Code/User/keybindings.json"

# path/to/Code/User/snippets
ln -sf "/Users/zach/Desktop/zvmac/materials/sw/os/za/dotfiles/markdown.json" "/Users/zach/Library/Application Support/Code/User/snippets/markdown.json"
```

install specific version
* uninstall using App Cleaner
* grab specific version
* unzip and move to `/Applications`
* open then quickly close so you can ⤵️ https://github.com/microsoft/vscode/issues/87215
* symlink from `settings.json`, `keybindings.json`, and snippets https://stackoverflow.com/a/49347158/6813490
* uninstall didn't seem to affect `~/.vscode/extensions`, fresh install just picked them up, enabled by default
* 1.41: broke Markdown extensions
* 1.46: pinned tabs https://code.visualstudio.com/updates/v1_46#_pin-tabs more flexible layouts https://code.visualstudio.com/updates/v1_46#_flexible-layout

workspaces
* https://code.visualstudio.com/docs/editor/multi-root-workspaces 
* _workspace_: container for n projects from n directories https://stackoverflow.com/a/50185038/6813490 
* `<dir>.code-workspace`: ❓ not sure how this works; doesn't seem to tell VS Code "here are paths to dir inside workspace"
* _create_: file > 'save workspace as'
* _add to_: file > 'add folder to workspace'
* _open_: select `.workspace` file in project root
* _switch_: 'open recent' from cmd pallete

keybindings
* tab: previous `gT` next `gt` (w/ Vim extension) https://stackoverflow.com/a/51407314
* goto symbol https://code.visualstudio.com/updates/v1_44#_workbench
* _clear file history_: command pallete + `clear editor history`
* _command palette (god command)_: `cmd shift p`
* _extensions_: `cmd shift x`
* _file explorer_: `cmd shift e`
* _function - declaration/definition_: cmd palette -> 'definition'
* _function - usage/reference_: cmd palette -> 'reference'
* Markdown preview: `cmd shift v`
* _outline view_: rm imports/vars/classes and leave only functions https://github.com/microsoft/vscode/issues/84380 https://github.com/zfeher/dotfiles/blob/66f3c1cb0d7a502adb5d4ee6d90493af3fab6c49/vscode/User/settings.json
* _pane - split_: `CMD \`
* _pane - switch ('splitter')_: `CMD ALT <arrow>`
* _search workspace_: `CMD SHIFT f` if you accidentally pull this off the activity bar [the leftmost section] you can drag back on https://stackoverflow.com/a/50065112/6813490
* _sidebar - show_: `cmd b`
* _tab - by number_: `{ "key": "cmd+1", "command": "workbench.action.openEditorAtIndex1" }`
* _tab - close others_: `cmd alt t`
* _un/fold_: cmd palette
