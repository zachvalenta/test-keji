# TODO

## 参考

📙 Chacon pro git https://git-scm.com/book/en/v2 @ ch. 3
📜 https://git-scm.com/docs `help <cmd>`
🎨 https://onlywei.github.io/explain-git-with-d3

## current

## queue

* rf for workflow

submodules so you can share dev notes btw personal/work machines 🗄 `psychology.md` note-taking
> need to clean up `industry.md`
> rn just using gist as marker, if gist has file contents = work machine head of notes repo
* _submodules_: `.gitmodules` separate Git repo w/in main repo for pulling dependencies
* https://longair.net/blog/2010/06/02/git-submodules-explained/ https://github.com/sharkdp/bat/blob/master/.gitmodules https://www.youtube.com/watch?v=8Z4Cmhji_FQ https://www.youtube.com/watch?v=ZYq3NJnO08U https://www.youtube.com/watch?v=iv7WwDgyb0U https://www.youtube.com/watch?v=De8Bc1VxcGQ
```sh
├── docs # module
├────── org
│   └── accounts.md  # .gitignore
│   └── architecture.md
│   └── company.md
│   └── onboarding.md
│   └── todo.md
├────── piao
│   └────── 299.md
│   └────── 427.md
├────── sw  # submodule
│   └────── js.md
│   └────── python.md
│   └────── sql.md
```
* double projects to Gitlab

## done

* _21_: prepopulate commit msg
* _20_: stash commands, 📙 Chacon ch 1-2, Gitlab as secondary remote for notes, auth for BNY (Gitlab token types, server protocols and set up, lots of debugging)
* _19_: hooks (pre-commit) branches (another pass at merge squash rebase) tooling (GitUp, Tig)
* _18_: PR workflow
* _17_: desultory corporate usage, tutorial w/ Roberto

# PLUMBING

🙂 punk rock https://xkcd.com/1597/

* _snapshot_: files at particular time e.g. a commit https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository
* `checkout`: will move rm changes to file in working tree e.g. if file is updated and staged, then updated again, checkout will only rm most recently updates i.e. changes in staging area won't be affected
* _reference_: human-readable name acting as point to commit SHA-1

---

plumbing - clean up notas history
* https://www.leshenko.net/p/ugit
* https://smusamashah.github.io/explain-git-in-simple-words http://www-cs-students.stanford.edu/~blynn/gitmagic/ https://thoughtbot.com/upcase/mastering-git https://news.ycombinator.com/item?id=22200222 https://betterexplained.com/articles/aha-moments-when-learning-git/ https://rachelcarmena.github.io/2018/12/12/how-to-teach-git.html design http://aosabook.org/en/git.html graph theory http://think-like-a-git.net/ write your own https://wyag.thb.lt/ https://benhoyt.com/writings/pygit/ Recurse Center article https://codewords.recurse.com/issues/two/git-from-the-inside-out Stanford https://www.kenneth-truyers.net/2016/10/13/git-nosql-database/ https://thoughtbot.com/upcase/mastering-git https://zwischenzugs.com/2018/05/14/beyond-punk-rock-git-in-eleven-steps/
* Perrota https://app.pluralsight.com/library/courses/how-git-works/table-of-contents https://www.pluralsight.com/courses/master-git
> do w/ his ML course
## states

file state https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository
* _untracked_: anything that wasn't in the last snapshot and not currently in the staging area i.e. files that Git doesn't know about
* _unmodified_: not updated since last commit
* _modified_: updated since last commit
* _staged_: to be incl in next commit, after which it will return to unmodified

sections https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F
* _working directory_: modified; aka 'working tree'; 'clean' = empty = no modified files
* _index/staging area_: staged; file changes marked for save in next commit
* _repository_: committed; `.git`

## design history

VCS history https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control
* _version control_: stores content and tracks changes to content https://medium.com/@willhayjr/the-architecture-and-history-of-git-a-distributed-version-control-system-62b17dd37742
* _first generation_: SCCS
* _second generation_: 2000 - centralized - CVS, SVN/Subversion, Perforce, Bitkeeper https://twobithistory.org/2018/07/07/cvs.html
* _third generation_: 2005 - distributed - Git (dominance such Stack Overflow dev survery no longer asks about VCS and people even use as a client to other VCS https://git-scm.com/book/en/v2/Git-and-Other-Systems-Git-as-a-Client) alternatives (FB uses Mercurial http://aosabook.org/en/mercurial.html SQLite uses Fossil)
* Git for everything https://news.ycombinator.com/item?id=30522175

Git
* _distributed_: less network latency than centralized https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control full version of repo history https://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository
* _reversible_: Git database onlys adds data so it's hard to do something that's not reversible https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F
* _no server_: no predefined client/server relationship among repos i.e. Github acts as a server but could be just another client https://zwischenzugs.com/2018/05/14/beyond-punk-rock-git-in-eleven-steps/
* _doesn't handle large repos or large file sizes_: meant for text https://superuser.com/q/13376 hence VFS (virtual fs) for Git https://pythonbytes.fm/episodes/show/53/getting-started-with-devpi-and-git-virtual-fs https://medium.com/@mattklein123/monorepos-please-dont-e9a279be011b https://medium.com/@adamhjk/monorepo-please-do-3657e08a4b70 https://medium.com/opendoor-labs/our-python-monorepo-d34028f2b6fa https://css-tricks.com/from-a-single-repo-to-multi-repos-to-monorepo-to-multi-monorepo/ git lfs https://stackoverflow.com/a/38313259 can now handle binary? https://tech.marksblogg.com/git-track-changes-in-media-office-documents.html
```sh
db/query-sandbox  $ git push -u origin main
Writing objects: 100% (17/17), 40.31 MiB | 596.00 KiB/s, done.
Total 17 (delta 0), reused 0 (delta 0), pack-reused 0
remote: warning: GH001: Large files detected. You may want to try Git Large File Storage - https://git-lfs.github.com.
remote: warning: See http://git.io/iEPt8g for more information.
remote: warning: File data/housing.csv is 66.34 MB; this is larger than GitHub's recommended maximum file size of 50.00 MB
```

linkable libraries 🗄 `python.md` Git
* reference impl of Git doesn't include i.e. can only as an executable, not as lib https://medium.com/@willhayjr/the-architecture-and-history-of-git-a-distributed-version-control-system-62b17dd37742 
* reimplementations include e.g. `libgit2` (C) which is used by other language implementations e.g. pygit2 (Python) https://github.com/gitpython-developers/GitPython/issues/240 Rugged (Ruby) https://git-scm.com/book/en/v2/Appendix-B%3A-Embedding-Git-in-your-Applications-Libgit2

## db of hashes

* _Git_: fs db of objects impl as DAG
* _object_: hash https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F
* _blob_: hash of file contents
* _tree_: blob + metadata (file name, permissions)
* _commit_: tree + more metadata (msgs, committer, author) + parent commit
* _branch_: reference to a commit; stored in `.git/ref/head`
* _HEAD_: most recent commit of current branch; `.git/ref/head/<current_branch>`
* compressed https://git-scm.com/book/en/v2/Getting-Started-What-is-Git%3F

# PORCELAIN

📜 cmd https://git-scm.com/book/en/v2/Appendix-C%3A-Git-Commands-Setup-and-Config

* _add - chunks_: `add -p`

## branch

🛠 curate https://github.com/matt-harvey/git_curate

list
* all on remote: `branch -a`

rm
* local - merged: `branch -d <br>`
* local - unmerged: `branch -D <br>`
* remote: `push origin --delete <br>`

---

default
* _default branch_: branch against which PRs are raised https://docs.github.com/en/github/administering-a-repository/changing-the-default-branch
* typically main/master but can be anything https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup `sw/git/master-to-main-personal-site.md`
* set: `branch -M <name>`

* use current branch name in commit msg https://stackoverflow.com/a/2111099 `branch=$(git branch | sed -n -e 's/^\* \(.*\)/\1/p')`
* get current branch: `git rev-parse --abbrev-ref HEAD` https://stackoverflow.com/a/6245587

strategies
* _Gitflow_: https://news.ycombinator.com/item 
* _trunk based_: https://trunkbaseddevelopment.com/ https://dev.to/alediaferia/git-tips-for-trunk-based-development-1i1g
* Linux kernel and other email-based workflows https://stackoverflow.com/a/23108169/6813490 https://drewdevault.com/2020/08/27/Microsoft-plays-their-hand.html

---

* _everything on branch not on other branch_: `git cherry -v develop mybranch` https://stackoverflow.com/a/24668421 to master `git cherry -v master`
* _checkout previous_: `git checkout -`
* _switch to different commit on same branch_: `checkout <hash>`
* switch back: `checkout <urbranch>`
* split branch into repo https://stackoverflow.com/questions/40340194/git-how-to-split-a-branch-in-its-own-repository
* pull in branch name for script https://stackoverflow.com/a/2111099/6813490
* _sink_: https://learngitbranching.js.org/

## commit

🗄 undo

delete git push origin HEAD --force https://stackoverflow.com/questions/1338728/how-do-i-delete-a-commit-from-a-branch
* prepare message beforehand https://stackoverflow.com/a/20447988/6813490
* mv most recent msg: `commit --amend`; actually replaces with entirely new commit https://git-scm.com/book/en/v2/Git-Basics-Undoing-Things
* mv n msgs: `rebase -i HEAD~commit_count` then replace `pick` w/ `reword` https://stackoverflow.com/a/7070976

message
* msg components: subject, description
* _COMMIT EDITMSG_: tmp file storing commit msg
* fmt: subject 50 col, desc 72 col https://drewdevault.com/2019/02/25/Using-git-with-discipline.html
* `shortlog` should tell a story https://news.ycombinator.com/item?id=22518813
* labels: func/test/dx/dep; lowers cognitive overhead, which matters w/ frequent commits https://github.com/commitizen/cz-cli
* how to https://drewdevault.com/2021/08/05/In-praise-of-Postgres.html
* prepopulate
```sh
# https://stackoverflow.com/a/53804934
git config commit.template <template_file.txt>
```

---

* sign/verify https://www.youtube.com/watch?v=4166ExAnxmo
* _tilde_: refers to parent; w/ args refers to nth parent `HEAD~2` (two parents prior); w/out args defaults to most proximate parent i.e. `HEAD~1` https://stackoverflow.com/a/23714994
* _entry mode_: inline (`-m`) verbose (`-v`) https://github.com/so-fancy/diff-so-fancy/issues/365 [Chacon 2.54]
> be nice if there was a way to commit that combined `commit -v` (show diff) and `di` (show some previous messages)
* _rm tracked file_: 📍 clarify usage w/ `-cache` flag [ibid 2.56-57]
* _checkout previous commit_: `checkout <commit>` enters 'detached HEAD state' (exit via `checkout - `); to actually do work based off old commit, better off creating branch `git checkout -b version2 <has>` https://git-scm.com/book/en/v2/Git-Basics-Tagging

update old
* _add changes_: `add <file>; commit --amend --no-edit` https://stackoverflow.com/a/40503483
* _update n prev msgs_: `rebase -i HEAD~num_of_commits` then use `reword` https://stackoverflow.com/a/7070976
* _rm previous commit_: `reset --hard <hash>`
* rewrite w/ amend/rebase https://www.youtube.com/watch?v=efJhX4SONVA

view https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History
* _specific commit_: `show <hash>` https://stackoverflow.com/a/7663506/6813490
* _all commits that touched file_: `git log --follow -- <file>` https://stackoverflow.com/a/8808453
* _change for commit_: diff `--patch` files and lines change `--stat`
* `--format`: msg description for single commit (`log --format=%B -n 1`) msg subj and desc `log --pretty=format:"%s %b"` https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History#pretty_format
* `--pretty`: oneline, short, full, fuller https://git-scm.com/book/en/v2/Git-Basics-Viewing-the-Commit-History
* filter out merges: `--no-merges`
* _date_: `--relative-date`, `--since=2.weeks`
* _search_: `--grep`, `log -S <query>` (commits that touched query), `-- <file>` (commits that touched file)

* _sink_: https://chris.beams.io/posts/git-commit/ https://fatbusinessman.com/2019/my-favourite-git-commit https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html https://stackoverflow.com/a/40506149/6813490 https://drewdevault.com/2019/02/25/Using-git-with-discipline.html use file for Git commit https://stackoverflow.com/a/20438380/6813490 https://medium.com/@hugooodias/the-anatomy-of-a-perfect-pull-request-567382bb6067 https://news.ycombinator.com/item?id=23739633

tags
* _tag_: way to label commits
* _use cases_: label release version https://softwareengineering.stackexchange.com/a/165731
* _types_: lightweight (just label on commit) annotated (itself a Git obj); can push only annotated tags to remote but not vice versa https://git-scm.com/book/en/v2/Git-Basics-Tagging
* _list_: `tag`
* _search_: `tag -l <glob>` https://git-scm.com/book/en/v2/Git-Basics-Tagging
* rm from local/remote https://git-scm.com/book/en/v2/Git-Basics-Tagging

## diff

* _modified_: `diff`
* _staged_: `--staged`/`--cached` [Chacon 2.53]
* _branches_: `diff <branch>..<branch>`
* _file across branches_: `diff <branch>..<branch> -- path/to/file` https://stackoverflow.com/a/4099805/6813490
* _commits_: `diff HEAD~2..HEAD`
* _LOC add/rm_: `git diff --numstat` https://stackoverflow.com/a/14879457/6813490
* no line numbers https://stackoverflow.com/a/24456418/6813490
* language-aware https://tekin.co.uk/2020/10/better-git-diff-output-for-ruby-python-elixir-and-more
* _sink_: https://www.atlassian.com/git/tutorials/saving-changes/git-diff 

## log

* all commits that touched LOC: `log -Lstart,end:path/to/file` https://stackoverflow.com/a/27108677
* overview of commits: `shortlog -sne`

---

* _unmerged commits on current branch_: `git log master..sprint --oneline` https://stackoverflow.com/a/4649377
* _time_: during a month `--since="2008-10-01" --before="2008-11-01"`
* _msg_: `log --format=%B -n 1"`

* git log no merges and only current branch https://stackoverflow.com/a/4649377/6813490
🔗 https://zwischenzugs.com/2018/03/26/git-log-the-good-parts/

* graph https://stackoverflow.com/q/5382255/6813490
* _time_: `log --since=2.weeks`

* _search commit content_: `log -S <query>` https://stackoverflow.com/a/2928721/6813490
* _search commit content by file_: `log -S <query> -- <path/to/file>`

## merge

semantics
* _merge_: interleave n commits 📙 Chacon 144
* _cherry pick_: put 1 commit onto tip of branch https://stackoverflow.com/a/9339460
* can always just merge other branch if it's only one commit ahead of master
* _rebase_: put n commits onto tip of branch https://stackoverflow.com/a/43551395
* can also use `squash` https://stackoverflow.com/q/2427238
* my notes workflow: `git rebase -i main`
```sh
# https://stackoverflow.com/a/5340773

# main
git init
echo "hi" > ex.txt
ga
gc  # init

# feature
git nb feature
echo "hey" > feat.txt
ga
gc  # on feature

# master
echo "hola" > ex.txt
ga
gc   # on main

# before rebase
* 353382c (main) on main
| * dd8a610 (HEAD -> feature) on feature
|/
* 44496c2 init

# rebase
git rebase main

# after rebase
* 99f30ad (HEAD -> feature) on feature
* 353382c (main) on main
* 44496c2 init
```


scenarios
* squash commits on feature: `rebase -i main` (pick first commit)
* changes from master onto feature: `rebase main` https://medium.com/front-end-weekly/avoid-80-of-merge-conflicts-with-git-rebase-b5d755a082a6
> this calls into question the above definition of rebase insofar as commits from master go onto tip of feature *and then feature commits go after that*

---

scenarios
* fetch: 
* pull: 
* pull --rebase https://goiabada.blog/git-tricks-avoiding-merge-when-dealing-with-remote-conflicts-52c175e526e6 https://stackoverflow.com/questions/2472254/when-should-i-use-git-pull-rebase https://gitolite.com/git-pull--rebase

* use case is maintaining linear history https://www.atlassian.com/git/tutorials/rewriting-history/git-rebase apparently the use case for why you'd want to rebase instead of merge becomes more clear if you understand directed acyclic graphs https://stackoverflow.com/a/9147389/6813490 use rebase to split up a commit https://github.com/thoughtbot/til/blob/master/git/split-up-a-commit.md rebase faster https://github.com/thoughtbot/til/blob/master/git/squashing-commits.md
* _grab file from another branch_: https://github.com/thoughtbot/til/blob/master/git/grab-a-file-from-another-branch.md

__how to__

* _squash feature already on remote_: `rebase -i develop; push --f` https://davidwalsh.name/squash-commits-git
* _put feature on master as single commit_: `rebase -i master; checkout master; merge <feature>` (irl open PR) https://stackoverflow.com/a/3697230/6813490 

* _rebase_: feature branch onto master as single commit  (everything in one commmit, but probably skip merging directly into master in favor of PR) `merge --squash my_feature` (still includes commit history) https://stackoverflow.com/a/3697263/6813490 more complex use case https://stefanoborini.com/beautiful-git-rebasing-of-version-branch/
* _squash_: everything on branch `git rebase --root -i` https://stackoverflow.com/a/9254257/6813490 could just blow away `.git` but would lose all other branches https://stackoverflow.com/a/1657287/6813490
```sh
$ echo "hey" > foo.txt  # 'first'
$ echo "hi" > foo.txt  # 'second'
$ echo "hello" > foo.txt  # 'third'

pick 80658a7 first  # have to squash newer commits into older ones i.e. pick the oldest commit and squash everything else https://stackoverflow.com/a/51516360/6813490 
squash a573038 second
squash c211c5b third
```

## remotes

📜 https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes

```sh
# create
remote add <name> <URL>  # defaults to `origin`
git remote add gl git@gitlab.com:zachvalenta/calendar.git

# read
remote -v  # all
remote show <name>  # single
<name>/<branch>  # reference non-origin remote

# update
remote rename <old_name> <new_name>  # name
remote set-url origin git@<provider>.com:<user>/<proj>.git  # URL
remote rm <name>
```

misc
* _upstream_: SSoT repo forked from w/ `remote -v show <repo` https://gist.github.com/Chaser324/ce0505fbed06b947d962 https://en.wikipedia.org/wiki/Downstream_(software_development)

push
* push to specific remote: `push <remote>`
* push specific branch: `push <branch>`
* push specific commit: `push <remote> <hash>:<branch>`
* rm branch from remote: `push origin --delete <branch_name>`
* _alias clone_: `clone <url> <alias>` https://git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository

---

* setup so you can pull sans args `push -u origin master` https://stackoverflow.com/a/18868188/6813490
* _branch - track_: `branch --set-upstream <local> <origin/remote`; think that `git checkout` from remote will automatically create local branch of same name already setup to track upstream
* _branch - check for changes_: `log origin/<branch>` https://stackoverflow.com/a/3278427/6813490
* _branch - view all_: `git branch -r`
* _log_: `log --no-merges HEAD..<remote>/<branch>`

## stash

create
* interactive: `stash -p` https://stackoverflow.com/a/12421642
* single file: `stash -- <file>`
* single file + msg: `stash push -m "my msg" <file>` https://stackoverflow.com/a/55073847
* all + msg: `stash save "my msg"` https://dev.to/srebalaji/useful-tricks-you-might-not-know-about-git-stash-117e

view
* list all: `stash list`
* show most recent: `stash show`
* show single: `stash show stash@{num}`
* show single - contents: `stash show -p stash@{num}`

use https://dev.to/srebalaji/useful-tricks-you-might-not-know-about-git-stash-117e
* _apply_: use but don't rm from stack; specific `stash apply stash@{1}`
* _pop_: use and rm from stack; specific `stash pop stash@{1}`
* _drop_: rm from stack; specific `drop stash@{index}` all `stash clear`

## undo

🔗 https://wizardzines.com/zines/oh-shit-git/ https://git-scm.com/book/en/v2/Git-Basics-Undoing-Things#_undoing https://git-scm.com/book/en/v2/Git-Internals-Maintenance-and-Data-Recovery#_data_recovery

repository
* ?: `reset --hard HEAD`
* rm most recent commit: `reset --hard HEAD~1`
* mv most recent commit to index: `reset --soft HEAD~1`

staging area
* unstage single file: `reset HEAD <file>` https://git-scm.com/book/en/v2/Git-Basics-Undoing-Things
* unstage all files: `reset` https://michaelsoolee.com/git-unstage-all/
* `git add .` is a bug magnet https://www.semicolonandsons.com/episode/how-to-make-less-mistakes-when-programming 2:20

the past
* _blame_: https://github.com/casperdcl/git-fame
* _bisect_: search for bug https://drewdevault.com/2019/02/25/Using-git-with-discipline.html https://lchsk.com/debugging-with-git-bisect.html remove secrets from commit https://startcodingnow.com/removing-secrets-from-django-project-in-docke https://news.ycombinator.com/item?id=26567969
* _reflog_: find stuff you've deleted e.g. reset back a few commits but need something from one of the commits you've skipped past, reflog will help you find it http://gitready.com/intermediate/2009/02/09/reflog-your-safety-net.html ❓ so Git doesn't rm stuff it sends to a trash can

---

* run background server to commit for you e.g. dura https://news.ycombinator.com/item?id=29784238
https://news.ycombinator.com/item?id=27579701
* revert to previous commit (if unpublished) `reset --hard <hash>` https://stackabuse.com/git-revert-to-a-previous-commit/
* reset modified files to working directory: `git checkout`

## workflow

🗄
* merge
* `di`: one-step add and commit for single file 
* `ding`: same as `di` but for multiples files 
* `gr`: one-step hard reset 

PR 🗄 `pr-workflow.pdf`
* fork
* clone fork
* cut feature branch
* impl
* pull upstream (`pull https://github.com/<ORIGINAL_OWNER>/<ORIGINAL_REPOSITORY>.git <BRANCH_NAME>` https://help.github.com/en/articles/merging-an-upstream-repository-into-your-fork)
* run tests
* push to your remote
* open PR against upstream

* UM
```sh
git commit
git checkout master
git pull
git checkout -
git rebase master
git push
# To github.com:tommyboytech/t3.git
# ! [rejected]            ur-branch -> ur-branch (non-fast-forward)
# error: failed to push some refs to 'repo'
# hint: Updates were rejected because the tip of your current branch is behind
# hint: its remote counterpart. Integrate the remote changes (e.g.
# hint: 'git pull ...') before pushing again.
# hint: See the 'Note about fast-forwards' in 'git push --help' for details.
git pull
# fatal: Not possible to fast-forward, aborting.
git push -f  # https://stackoverflow.com/a/39400690
```
---

* https://zaiste.net/15-git-commands-you-may-not-know/ autocompletion https://git-scm.com/book/en/v1/Git-Basics-Tips-and-Tricks https://git-scm.com/book/en/v2/Appendix-A%3A-Git-in-Other-Environments-Git-in-Bash  https://apple.stackexchange.com/q/55875* https://stackoverflow.com/questions/33495152/enabling-auto-completion-in-git-bash-on-windows https://github.com/donnemartin/gitsome
* undoing - https://gitexplorer.com/ https://github.com/k88hudson/git-flight-rules https://ohshitgit.com/ https://cheat.readthedocs.io/en/latest/git.html https://www.youtube.com/watch?v=FdZecVxzJbk https://blog.github.com/2015-06-08-how-to-undo-almost-anything-with-git/ rm sensitive data from history https://dev.to/edmondso006/removing-sensitive-data-from-git-history-5g63 艘 Gith Guardian 
* pager https://github.com/dandavison/delta these are the config that diff-so-fancy updates https://github.com/so-fancy/diff-so-fancy#usage
* Nick J https://www.youtube.com/watch?v=S0_pOvrfN0U https://www.youtube.com/watch?v=IL1ktpzfT8E

* crd git workflow
```sh
git fetch --prune origin
git rebase -i --autosquash origin/master
git push -f origin crd/my-feature-branch
git checkout master
git merge origin/master
git merge origin crd/my-feature-branch
git push origin master
git push origin :crd/my-feature-branch
git branch -d crd/my-feature-branch
```

# SERVER

* bug tracking: https://github.com/MichaelMure/git-bug https://www.youtube.com/watch?v=6Q4Lac0MCL0
* https://gemini.nytpu.com/gemlog/2021-03-07.gmi
* https://github.com/charmbracelet/soft-serve
* admin setup: create bare repository, scp to server with Git installed, if devs on your team have ssh access to server you're set https://git-scm.com/book/en/v2/Git-on-the-Server-Getting-Git-on-a-Server
* user setup: add public key

* _bare repository_: only git data (`.git`) with no working directory i.e. no actual files https://git-scm.com/book/en/v2/Git-on-the-Server-The-Protocols
* _GitWeb_: built-in GUI for server https://git-scm.com/book/en/v2/Git-on-the-Server-GitWeb
* _snippets_: Gist, pastebin https://softwareengineeringdaily.com/2020/06/08/tilt-kubernetes-tooling-with-dan-bentley/ 46:45
* _types of hosting_: aaS (Github, Gitlab EE, SourceHut) self-hosted (Gitweb, Gitlab CE, https://gogs.io/ https://gitea.io/en-us/ https://github.com/honza/smithy)

## auth

* store credentials using macos Keychain https://gist.github.com/nepsilon/0fd0c779f76d7172f12477ba9d71bb66

protocols for data transfer https://git-scm.com/book/en/v2/Git-on-the-Server-The-Protocols https://git-scm.com/book/en/v2/GitHub-Account-Setup-and-Configuration
* _local_: use own machine (or NFS mount) as remote
* _http_: smart version uses auth and allows writes, dumb version read-only and no auth; can cache user/pass using macos Keychain
* _ssh_: non-anonymous, need to futz with keys
* _Git_: daemon that comes packaged with Git, hard to set up, for reads only

* no auth: this is server dependent e.g. work servers prompt user/pw for public repos but Github/lab do not
```sh
# PUBLIC REPOS
git clone https://gitlab.com/zachvalenta/pre-commit-test  # ✅ yours
git clone https://gitlab.com/esr/microjson.git  # ✅ others

# PRIVATE REPOS
# error msg ("No such device or address") suggests resource doesn't exist (bc it doesn't, for your user)
git clone https://gitlab.com/zachvalenta/dummy-repo.git  # ❌ yours
git clone https://gitlab.com/pulphead/film-censorship.git  # ❌ others
```

## Github

🔗 https://github.com/github/roadmap

CLI
* dashboard https://github.com/dlvhdr/gh-dash
```sh
# alias https://cli.github.com/manual/gh_alias
gh alias set --shell prl "gh pr list --author zachvalenta --repo tommyboytech/t3"  # get PR number
gh alias set --shell prv 'gh pr view "$1" --repo tommyboytech/t3 -w'               # view PR in browser

##################3

# get PRs
gh pr list --author zachvalenta --repo tommyboytech/t3

# ❌ reviews requested
gh pr list --search "user-review-requested:zachvalenta" --repo tommyboytech/t3
gh pr list --search "user-review-requested:@me" --repo tommyboytech/t3
gh pr list --search "review-requested:zachvalenta" --repo tommyboytech/t3

# get PR number
gh pr list --author zachvalenta --repo tommyboytech/t3 | rg "\d" | awk '{ print $1 }'

# view PR
gh pr view 9985 --repo tommyboytech/t3 
gh pr view 9985 --repo tommyboytech/t3 -w
gh pr view 9985 --repo tommyboytech/t3 --comments

# view PR in browser
gh pr list --author zachvalenta --repo tommyboytech/t3 | rg '\d' | awk '{ print $1 }' | xargs gh pr view --repo tommyboytech/t3 -w

# ❌ awk needs single quotes to work but Github CLI removes column parameter
gh alias set --shell prv "gh pr list --author zachvalenta --repo tommyboytech/t3 | rg '\d' | awk '{ print $1 }' | xargs gh pr view --repo tommyboytech/t3 -w"
gh alias list
# prl:  !gh pr list --author zachvalenta --repo tommyboytech/t3
# prv:  !gh pr list --author zachvalenta --repo tommyboytech/t3 | rg '\d' | awk '{ print  }' | xargs gh pr view --repo tommyboytech/t3 -w
```

adding org
* add org email address to personal account but keep personal email as primary https://docs.github.com/en/account-and-profile/setting-up-and-managing-your-github-user-account/managing-email-preferences/adding-an-email-address-to-your-github-account
* send notifications to org w/ 'custom routing' https://docs.github.com/en/account-and-profile/managing-subscriptions-and-notifications-on-github/setting-up-notifications/configuring-notifications#customizing-email-routes-per-organization
```txt
If you have two-factor authentication enabled or not
Your public profile information
Certain activity within this organization
Country of request origin
Your access level to repositories within the organization
Your IP address
Opt out of future invitations from this organization.
```

search https://docs.github.com/en/github/searching-for-information-on-github/searching-on-github
* files in repo: `t`
* filters: `org:freeCodeCamp language:python filename:.tigrc user:zachvalenta extension:py` https://stackoverflow.com/a/28347129 https://stackoverflow.com/a/42418887
> doesn't seem to work for hidden files
> doesn't seem to work for exact searches e.g. `[behave]`
* can use regex https://news.ycombinator.com/item?id=22396824
* file with text inside: `callback_whitelist filename:ansible.cfg`
* issues you created `author:zachvalenta`

---

* draft PR https://github.blog/2019-02-14-introducing-draft-pull-requests/
* Mermaid support https://github.blog/2022-02-14-include-diagrams-markdown-files-mermaid/ 
* feedback https://github.com/github/feedback/discussions/8293 https://support.github.com/ticket/personal/0/1530410
* _Actions_: https://github.com/nektos/act https://hynek.me/articles/python-github-actions/ https://help.github.com/en/actions/configuring-and-managing-workflows/configuring-a-workflow https://github.com/sdispater/mixology/blob/master/.github/workflows/tests.yml https://github.com/github/super-linter https://www.youtube.com/watch?v=E1OunoCyuhY https://github.com/nektos/act https://news.ycombinator.com/item?id=30060765 https://towardsdatascience.com/ultimate-ci-pipeline-for-all-of-your-python-projects-27f9019ea71a
* _analytics_: watchers `<URL>/watchers` stars `<URL>/stargazers` https://webapps.stackexchange.com/a/41800 profile views https://rushter.com/blog/github-profile-markdown/ 3rd party analytics around your commit history https://sourcerer.io/elena
* _CLI_: https://github.com/cli/cli
* _dependency graph/tree_: https://github.com/zachvalenta/create-python-app/network/dependencies
* _CLI_: https://github.com/donnemartin/gitsome https://github.com/github/hub
* _issues_: 😮 https://github.com/isaacs/github/issues/6
* _linking_ https://blog.github.com/2011-10-12-introducing-issue-mentions/
* _metrics_: https://www.gitprime.com/ https://github.com/treyhunner/django-simple-history -> Code Climate https://rushter.com/blog/github-profile-markdown/
* _profile README_: create repo with same name as user, add README
* _repo language_: https://github.com/github/linguist#overrides
* _repo config_: branch protections http://blog.jaredsinclair.com/post/183676881105/think-twice-before-downgrading-to-a-free-github owners https://blog.github.com/2017-07-06-introducing-code-owners/
* _shortcuts_: file search in repo `t` jump to symbol in code review `t` blame in file `b` https://darrenburns.net/posts/github-tips 

## Gitlab

---

https://simonwillison.net/2022/Feb/10/github-burndown/

🔐 tokens and keys https://gist.github.com/zachvalenta/d7187130c63c75aa7ea86465e82198ec 🗄 `gitlab-deploy-token.md` `python.md` libs/Git
|  type        | protocol | ownership     | scope | actions           | notes
| ------------ | -------- | ------------- | ----- | ---------------   | --------------
| access token | https    | user          | ?     | API, read, write  | https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html#limiting-scopes-of-a-personal-access-token
| deploy token | https    | project/group | ?     | read              | https://docs.gitlab.com/ee/user/project/deploy_tokens/
| deploy key   | ssh      | service       | ?     | read, write       | https://docs.gitlab.com/ee/user/project/deploy_keys

* docs: https://docs.gitlab.com/ee/user/project/deploy_keys/#differences-between-deploy-keys-and-deploy-tokens
* deploy tokens belong to a project/group and also *seem* like they're only able to interact with the project/group to which they belong
|  type        | actions     | protocol | scoped to        | used for                                                           |
| ------------ | ----------- | -------- | ---------------- | ------------------------------------------------------------------ |
| deploy key   | read, write | ssh      | service          | clone repo to run build in CICD pipeline, merge feature branch     |
| deploy token | read        | https    | project or group | clone repo to run build in CICD pipeline                           |
| access token | read        | https    | user             | hit Gitlab API (get info on repo/group, download repo as tarball)  |

---

* CE used to only have deploy keys
* EE used to not have deploy token
```sh
# ACCESS TOKEN (personal, project)
# clone - needs to be enabled on server (e.g. didnt' work on corporate network)
git clone https://user_name:access_token@gitlab.com/zachvalenta/dummy-repo.git
# API - get repo stats https://stackoverflow.com/a/54383282
curl --header "PRIVATE-TOKEN: <access_token>" https://gitlab.com/api/v4/users/zachvalenta/projects

# DEPLOY TOKEN
git clone https://token_name:token@gitlab.com/zachvalenta/dummy-repo.git
```

general
* _version_: https://gitlab.com/help
* _account will be deleted if inactive_: https://news.ycombinator.com/item?id=23827772
* test pipelines locally https://news.ycombinator.com/item?id=26236677

CICD https://gitlab.com/zachvalenta/pre-commit-test.git https://docs.gitlab.com/ee/ci/yaml/ https://docs.gitlab.com/ https://docs.gitlab.com/runner/
* _job_: declarative series of steps
* _stage_: grouping mechanism for jobs e.g. test, deploy
* _pipeline_: collection of stages; can force manual interaction https://docs.gitlab.com/ee/ci/pipelines/index.html#add-manual-interaction-to-your-pipeline to run without, toggle off in project (visibility and merge requests)
* conditionals https://docs.gitlab.com/ee/ci/yaml/#rulesif
* _artifact_: static files produced by pipeline e.g. coverage report from tests
* generate report: `pytest --junitxml=report.xml` https://docs.gitlab.com/ee/ci/unit_test_reports.html#python-example
```yaml
# basic
unit_tests:
  image: python:3.7
  script:
    - "pip install -r requirements.txt"
    - "ln -sf .env.dev .env"
    - "pytest -v app_test.py"

# ref env var set via GL instance
ax2: "${ax2}"
```

# ZA

* file diff: `git diff --no-index <file1> <file2>` https://stackoverflow.com/a/54656539
* do code review before story starts https://calpaterson.com/wasting-time.html
* _auth_: https://github.com/thoughtbot/til/blob/master/git/osx-keychain.md
* _identity_: https://www.micah.soy/posts/setting-up-git-identities/
* _patch set_: diff btw files [Chacon 1.28] making patches more granular when staging, stashing https://stackoverflow.com/a/34610928 📍 add answer re: using GitUp
* _worktree_: check out separate branch into separate directory https://stackoverflow.com/a/31951225 https://huonw.github.io/blog/2020/04/worktrees-and-pyenv/
* can't add empty dir https://git.wiki.kernel.org/index.php/Git_FAQ#Can_I_add_empty_directories.3F don't deploy `.git` to PROD https://slashcrypto.org/2018/11/28/eBay-source-code-leak/

installation https://git-scm.com/book/en/v2/Getting-Started-Installing-Git
* macOS: 10.9 onwards handled by Command Line Tools https://github.com/creationix/nvm#important-notes ❓ Homebrew install being used?
* Linux: `git-all`

config https://git-scm.com/book/en/v2/Customizing-Git-Git-Configuration https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup
* aliases split btw `.gitconfig` and `.bash_profile` 
* set based on repo https://utf9k.net/blog/conditional-gitconfig/
* _list_: `git config --list --show-origin` https://stackoverflow.com/a/2115116 might see dupes bc Git reads from all config files, with most local (e.g. repo-level) taking precedence
* _precedence_: repo-level (`.git/config`) user-level/global? (`~/.gitconfig`) system-level (`/etc/gitconfig`; don't touch)
* _rm attribute from config_: `git config --unset <attr>`
* aliases https://git-scm.com/book/en/v2/Git-Basics-Git-Aliases
```sh
# update config from shell
git config           # local ($CWD/.git/config)
git config --user    # user (~/.gitconfig)
git config --system  # system
```

gitignore https://git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository
* _user_: `~/.config/git/ignore`
* _repo_: `.gitignore`
* `/` interpolated as the root of your directory i.e. `/app/logs` will ignore anything in `/app/logs` but not, say, `/logs` (that is, a `logs` dir located in your root direct)
* this works recursively; [all subdirectories are affected as well](http://qr.ae/TU1tsk) i.e. any `logs` deeper inside `app/logs` will also be ignored
* `logs`, on the other hand, will ignore anything in *any* `logs` directory located *anywhere* in your project

notas post-mortem
* outcome: messed up looking git log
* cause: `commit --amend --no-edit` on feature branch (`sprint`) and then merged to main
* work around: forked repo, then realized I could just create new `main` in existing repo bc `sprint` and `master` had always been aligned (my workflow was squashing `sprint` at week's end and merging that to `master`). so, spent a week working in a new repo and moving those file changes to old repo, and then at week's end, once I confirmed the git log looked better, just replaced new repo w/ old repo.

## hooks

📜 https://git-scm.com/book/en/v2/Customizing-Git-Git-Hooks https://githooks.com/

* actions: client-side (commit, merge) server (push)
* file-system location: `.git/hooks` 
* ignore failed hooks w/ `git commit --no-verify` http://omerkatz.com/blog/2013/2/15/git-hooks-part-1-the-basics

pre-commit https://pre-commit.com https://github.com/pre-commit/pre-commit/issues https://gitlab.com/zachvalenta/pre-commit-test
* set: `pre-commit install -t pre-commit; pre-commit install -t pre-push` (i.e. copy Python scripts in place of Git samples) https://pre-commit.com/#3-install-the-git-hook-scripts https://pre-commit.com/#pre-commit-install
* skip: `SKIP=<stage> git commit -m "foo"`
* uninstall: `pre-commit uninstall -t <action>`
* conf: `.pre-commit-config.yaml`
* run in parallel, can cause random failures, run in serial using `require_serial = true` https://pre-commit.com/#hooks-require_serial
* official hooks: black handles `trailing-whitespace` and `end-of-file-fixer` https://github.com/pre-commit/pre-commit-hooks/tree/master/pre_commit_hooks https://www.youtube.com/watch?v=BzC3ft8rm4c
* pylint is a pain https://github.com/pre-commit/pre-commit/issues/266#issuecomment-399682269 black https://github.com/pre-commit/pre-commit-hooks/issues/356 https://github.com/psf/black#version-control-integration pytest 

```yaml
---
- repo: local  #  https://pre-commit.com/#repository-local-hooks https://github.com/pre-commit/pre-commit/issues/1245
  hooks:
  - id: lint
    stages: [commit]
    name: run lint
    entry: make lint
    language: system
    types: [python]
  - id: test
    stages: [push]
    name: run test
    entry: make test
    language: system
    types: [python]
```

## utils

GUI (GitUP)
* good for granular stages
* switch views `cmd #`
* open commit into quick view `space`
* alternatives https://git-scm.com/downloads/guis/ https://git.wiki.kernel.org/index.php/InterfacesFrontendsAndTools https://git-scm.com/book/en/v2/Appendix-A%3A-Git-in-Other-Environments-Graphical-Interfaces

pager / diffview (diff-so-fancy)
* set to use external tool via `git difftool -help` 📙 Chacon 2.54
* _diff-so-fancy_
* _delta_: 📍 try again, diffs/filenames were too dark https://github.com/dandavison/delta
* node version of delta https://github.com/banga/git-split-diffs https://news.ycombinator.com/item?id=27007844
* https://github.com/sindrets/diffview.nvim https://www.youtube.com/watch?v=aJikrPnTOtI
* _difftastic_: https://github.com/Wilfred/difftastic
* _dunk_: https://github.com/darrenburns/dunk

porcelain (vim-fugitive)
* autocomplete: https://github.com/chriswalz/bit
* _magit_: https://github.com/magit/magit https://github.com/dandavison/delta/issues/194#issuecomment-636001812 https://emacsair.me/2017/09/01/magit-walk-through/
* _lazygit_ https://github.com/jesseduffield/lazygit
* _forgit_: https://github.com/wfxr/forgit#-features
* _vim-fugitive_: https://github.com/tpope/vim-fugitive https://www.youtube.com/watch?v=kFVjoIish0E https://gumroad.com/vimtricks https://github.com/TimUntersberger/neogit http://vimcasts.org/episodes/archive/ https://www.semicolonandsons.com/episode/IDE-like-refactors-snippets-tests-hover-docs-commenting-and-git 3:15

repo browser (Tig) https://github.com/jonas/tig https://jonas.github.io/tig/doc/manual.html
* _modes_: main `m` diff `d` log `l` blame `b`; main view with message body https://github.com/jonas/tig/issues/1032
* _all commits_: `tig` in repo 
* _file history_: `tig path/to/file`
* _blame_: `tig blame path/to/file` https://stackoverflow.com/q/15304804 or tree view `t` then `b`
* alternatives https://github.com/rgburke/grv https://git-scm.com/docs/gitk https://github.com/isacikgoz/gitin
* repo stats: onefetch https://github.com/o2sh/onefetch
