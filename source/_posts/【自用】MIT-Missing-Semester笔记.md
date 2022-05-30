---
title: 【自用】MIT-Missing-Semester笔记
categories: 技术
index_img: https://baokker-oss-blog-hangzhou.oss-cn-hangzhou.aliyuncs.com/cdn_for_blog/blog_imgs/peanuts-6919261_1920.jpg
banner_img: https://baokker-oss-blog-hangzhou.oss-cn-hangzhou.aliyuncs.com/cdn_for_blog/blog_imgs/peanuts-6919261_1920.jpg
date: 2022-02-13 22:33:20
excerpt: 一门很好的计算机知识补充课程
---



# MIT-Missing-Semester

> 在csdiy上被安利的首个课程，虽然是全英文，而且整个课程比较硬核，但是确实是如标题所言，讲到了很多息息相关但是在课程里未曾涉及的知识，对我整个知识体系的完善有了很大帮。（还锻炼了点英语）
>
> 观看的时候，也不必强求理解所有东西，正如课程的一位教师所言，**仅仅是知道有这样的东西存在**，已经足够了。
>
> 另外，课后练习还是很推荐做的，有助于知识的巩固。
>
> 好啦，继续加油！
>
> https://missing.csail.mit.edu/2020/

# Lecture 1 Shell

```bash
date # current date

echo hello
echo hello\ world
echo "hello world"

echo $PATH # the environment paths;the bash execute files straightforwardly which is in $PATH

which echo # determine where the echo is executed

pwd # present working directory

cd .. # parent directory
cd ./home # .means current path
cd ../../../../../hgfs # traverse search
cd ~ # ~ brings to home direc  tory
cd - # move to the previous path
cd /mnt/hgfs # from the root path

ls
ls -l # give you more detailed information

mv [oldpath/]oldFileName [newpath/]newFileName # move or rename
mv oldpath/* newpath # move all files in oldpath

rm fileName # remove
rm -rf fileordirName # delete all

rmdir dirName # remove dir only if it's empty
mkdir "my Photos" # make new dir

man ls # get the manual page of ls

echo hello > hello.txt
cat hello.txt
cat < hello.txt > hello2.txt # rewire,the cat get the content of hello.txt and then copy it into a new one.the cat means concatenate
cat < hello.txt >> hello2.txt # > means overwrite,and >> means append
ls -l / | tail n1 > ls.txt # pipe character.ls -l / as input to tail n1,and tail n1 output the last line to ls.txt

sudo echo 500 > brightness # super user do
echo 1060 | sudo tee brightness # tee output the content to both std out and designated out

xdg-open fileName
```



distinguish between absolute path/relative path



`ls -l` will return a string like

```bash
-rwxr-xr-x 1 root root xxxxxx
```

第一个`rwx`表示root（user）用户具有read，write，和execute的权限；第二个`r-x`表示其所在group owner能read和write；第三个`r-x`表示everyone的权限。

对file来说，read、write、execute的意思很明显；对文件夹来说，read是表示能够浏览文件夹中的内容，write是表示能够重命名、创建，或删除文件；execute表示能否进入到这个文件夹中。没有execute，read和write无法进行。



ctrl+L 清空屏幕



`$` 表示你是user而非root，root对应的是`#`

在试图修改某些文件时（例如，修改亮度）：

```bash
$ cd /sys/class/backlight/thinkpad_screen
$ sudo echo 3 > brightness
An error occurred while redirecting file 'brightness'
open: Permission denied
```



learn from practice:

- `touch` can change the information of files. If the file doesn't exist,it will create one.

- ```bash
  # usage of chmod
  sudo chmod chmod ugo+r file1.txt # all can read
  chmod a+r file1.txt # all can read
  chmod 777 file # all can read,write,and execute it
  chmod u=rw,go= file # user can write and read,group and other don't have any power
  ```



# Lecture 2 Shell Tools

```bash
foo = bar # error,equal to execute "foo" with arguments like '=' and 'bar'
foo=bar # right.spaces are critical
echo $foo # print bar

echo 'value is $foo' # value is $foo
echo "value is $foo" # value is bar

vim mcd.sh
#mcd(){
#	mkdir -p "$1" # the first argv
#	cd "$1"
#}
source mcd.sh
mcd test # move into test folder

mkdir /mnt/new # error don't have permission
sudo !! # replace !! with mkdir /mnt/new

grep foobar mcd.sh
echo $? # error code 1

# the operator goes like what is in cpp 
false || echo "opps fail"
true || echo "it won\'t be printed"
false && echo "it won\'t be printed"

foo=$(pwd) 
echo "we are now in $(pwd)" # command substitution

cat <(ls) <(ls ..) # process substitution

# globbing
ls *.sh # all length is accepted 
ls name? # ? only supports one length 

# also brackets 

convert image.{png,jpg}
# Will expand to
convert image.png image.jpg

cp /path/to/project/{foo,bar,baz}.sh /newpath
# Will expand to
cp /path/to/project/foo.sh /path/to/project/bar.sh /path/to/project/baz.sh /newpath

# Globbing techniques can also be combined
mv *{.py,.sh} folder
# Will move all *.py and *.sh files

# This creates files foo/a, foo/b, ... foo/h, bar/a, bar/b, ... bar/h
touch {foo,bar}/{a..h}
diff < folder1 < folder2

# below is a Python script 
# the first line is a shebang which indicates that the kernel should use a Python interpreter instead of a shell command
# you can use command like #!/usr/bin/env python
# it takes advantage of the $PATH ,which will help to search the Python 
#!/usr/local/bin/python
import sys
for arg in reversed(sys.argv[1:]):
    print(arg)
    
    
tldr convert # tldr is a useful tool to give you practical commands example compared to manpage

# find
# Find all directories named src
find . -name src -type d
# Find all python files that have a folder named test in their path
find . -path '*/test/*.py' -type f
# Find all files modified in the last day
find . -mtime -1
# Find all zip files with size in range 500k to 10M
find . -size +500k -size -10M -name '*.tar.gz'
 
# you can also perform actions on the results of find
# Delete all files with .tmp extension
find . -name '*.tmp' -exec rm {} \;
# Find all PNG files and convert them to JPG
find . -name '*.png' -exec convert {} {}.jpg \;

# fd is a easier 
fd ".*py"

# locate equals to find,but it uses inner database so it's faster but maybe not fresher than the find func.
updatedb # update database for locate
history

# grep search for the content in the files
grep -C 5 # Context.the result will print 5 lines before and after the match
grep -R # recursively find all files in the folders

# developed tools to take place of grep like ack ag rg is recommended
# Find all python files where I used the requests library
rg -t py 'import requests'
# Find all files (including hidden files) without a shebang line
rg -u --files-without-match "^#!"
# Find all matches of foo and print the following 5 lines
rg foo -A 5
# Print statistics of matches (# of matched lines and files )
rg --stats PATTERN

# fzf is a good tool combined with Ctrl+R to get the previous command you want to reuse

ls -R
# tree
# broot
```

these dollars:

| name         | func                                                         |
| ------------ | ------------------------------------------------------------ |
| `$0`         | the name of the script that we're running                    |
| `$1` to `$9` | the first to the ninth argument                              |
| `$#`         | the num of arguments                                         |
| `$$`         | the process ID of this command that is running               |
| `$?`         | return the code of the previous command                      |
| `$_`         | last argument from the last command                          |
| `$@`         | expand all arguments                                         |
| !!           | entire last command(including arguments).A usual usage is like `sudo !!` |

`Ctrl+shift+e` 搜狗输入法切换英文自动联想（）



`ctrl+R` can perform backwards search



other multiple tools:

 [fish](https://fishshell.com/) [zsh](https://github.com/zsh-users/zsh-autosuggestions)  [`fasd`](https://github.com/clvv/fasd) [`autojump`](https://github.com/wting/autojump) [`tree`](https://linux.die.net/man/1/tree)  [`broot`](https://github.com/Canop/broot)



# Lecture 3 Editors(vim)

> **the Vim's interface is a programming language**
>
> whenever you’re using your editor and you think “there must be a better way of doing this”, **there probably is**: look it up online.

```bash
vimtutor # offical tutor,very useful
```



- **Modal Editing**

  - normal mode

    - `h` left `j` down `k` up `l` right
    - `w` `b` `e`
    - etc(below)

  - (`i`)insert mode

  - (`r`)replace mode

  - (`v`)visual mode

    - (`shift-v`)  visual line
    - (`ctrl-v`) visual block

  - (`:`)command line mode

    ```bash
    :q # quit one window
    :qa # quit all windows
    :w # write 
    :wq # write and quit 
    :e {name of file} # open file for editing
    :ls # show open buffers
    :help {topic} # open help
    :help :w # opens help for the :w command
    :help w # opens help for the w movement
    ```

- Movement

  - Basic movement: `hjkl` (left, down, up, right)
  - Words: `w` (next word), `b` (beginning of word), `e` (end of word)
  - Lines: `0` (beginning of line), `^` (first non-blank character), `$` (end of line)
  - Screen: `H` (top of screen), `M` (middle of screen), `L` (bottom of screen)
  - Scroll: `Ctrl-u` (up), `Ctrl-d` (down)
  - File: `gg` (beginning of file), `G` (end of file)
  - Line numbers: `:{number}<CR>` or `{number}G` (line {number})
  - Misc: `%` (corresponding item)
  - Find: `f{character}` `t{character} ` `F{character}` `T{character}`

    - find/to forward/backward {character} on the current line
  - `,` / `;` for navigating matches
  - Search: `/{regex}`, `n` / `N` for navigating matches
  - `ctrl+g`:see the info of the file

- Selection

  Visual modes:

  - Visual: `v`
  - Visual Line: `V`
  - Visual Block: `Ctrl-v`

- Edit

  - `i` 

    - enter Insert mode

    - but for manipulating/deleting text, want to use something more than backspace

  - `o` / `O` insert line below / above

  - `d{motion}` delete {motion}

    - e.g. `dw` is delete word, `d$` is delete to end of line, `d0` is delete to beginning of line

  - `c{motion}` change {motion}

    - e.g. `cw` is change word
    - like `d{motion}` followed by `i`

  - `x` delete character (equal do `dl`)

  - `s` substitute character (equal to `xi`)

  - Visual mode + manipulation

    - select text, `d` to delete it or `c` to change it

  - `u` to undo, `<C-r>` to redo

  - `y` to copy / “yank” (some other commands like `d` also copy)

  - `p` to paste

  - Lots more to learn: e.g. `~` flips the case of a character

- Count

  - `3w` move 3 words forward
  - `5j` move 5 lines down
  - `7dw` delete 7 words

- Modifiers

  Some modifiers are `i`, which means “inner” or “inside”
  and `a`, which means “around”.

  - `ci(` change the contents inside the current pair of parentheses
  - `ci[` change the contents inside the current pair of square brackets
  - `da'` delete a single-quoted string, including the surrounding single quotes

# Lecture 4 Data Wrangling

regular expression（regexp）

```bash
ssh myserver journalctl
 | grep sshd
 | grep "Disconnected from"
 | sed 's/.*Disconnected from //'
```

the format always goes like `s/REGEX/SUBSTITUTION/`

some syntax:

- `.` means “any single character” except newline
- `*` zero or more of the preceding match
- `+` one or more of the preceding match
- `[abc]` any one character of `a`, `b`, and `c`
- `(RX1|RX2)` either something that matches `RX1` or `RX2`
- `^` the start of the line
- `$` the end of the line

（https://regexone.com/）

| metacharacter | meaning                                              |
| ------------- | ---------------------------------------------------- |
| \d            | digit                                                |
| \D            | non-digit                                            |
| \w \W         | is (or is not) digit nor an alphanumeric letter      |
| \s \S         | is(or is not) a whitespace                           |
| \t \T         | is (or is not) a tab                                 |
| \b            | the boundary between a word and a non-word character |
| \0            | the whole captured group                             |
| \1 .. \n      | the sequential captured variables                    |

regular expression debugger

and multiple pipelines

这节课的知识量实在太大了..只能说，一个是学会正则表达式，另外一个是，明白linux中可以通过各种各样的指令实现很多数据提取。



# Lecture 5 Command-line Environment

Job Control

signals

`Ctrl-C` means sending `SIGINT` to the process

`Ctrl-\` means `SIGQUIT`.

you can also use `kill -TERM <PID>` to send `SIGTERM` to kill this command.

`Ctrl-Z` will send `SIGTSTP`(signal terminal stop) ,which will pause the process. you can use `bg` or `fg` to continue the job in back/foreground.



 jobs

```bash
$ sleep 1000
^Z # stop but not terminate it 
[1]  + 18653 suspended  sleep 1000

$ nohup sleep 2000 & # & suffix will put it running in the background
[2] 18745
appending output to nohup.out

$ jobs # list
[1]  + suspended  sleep 1000
[2]  - running    nohup sleep 2000

$ bg %1 # check the first one
[1]  - 18653 continued  sleep 1000

$ jobs
[1]  - running    sleep 1000
[2]  + running    nohup sleep 2000

$ kill -STOP %1 # stop the first
[1]  + 18653 suspended (signal)  sleep 1000

$ jobs
[1]  + suspended (signal)  sleep 1000
[2]  - running    nohup sleep 2000

$ kill -SIGHUP %1 # kill the first
[1]  + 18653 hangup     sleep 1000

$ jobs
[2]  + running    nohup sleep 2000

$ kill -SIGHUP %2

$ jobs
[2]  + running    nohup sleep 2000

$ kill %2
[2]  + 18745 terminated  nohup sleep 2000

$ jobs
```



terminal multiplexer(like tmux)

 tmux:

- Sessions

  - window
  - pane

- Sessions

   

  \- a session is an independent workspace with one or more windows

  - `tmux` starts a new session.
  - `tmux new -s NAME` starts it with that name.
  - `tmux ls` lists the current sessions
  - Within `tmux` typing `<C-b> d` detaches the current session
  - `tmux a` attaches the last session. You can use `-t` flag to specify which

- Windows

   

  \- Equivalent to tabs in editors or browsers, they are visually separate parts of the same session

  - `<C-b> c` Creates a new window. To close it you can just terminate the shells doing `<C-d>`
  - `<C-b> N` Go to the *N* th window. Note they are numbered
  - `<C-b> p` Goes to the previous window
  - `<C-b> n` Goes to the next window
  - `<C-b> ,` Rename the current window
  - `<C-b> w` List current windows

- Panes

   

  \- Like vim splits, panes let you have multiple shells in the same visual display.

  - `<C-b> "` Split the current pane horizontally
  - `<C-b> %` Split the current pane vertically
  - `<C-b> <direction>` Move to the pane in the specified *direction*. Direction here means arrow keys.
  - `<C-b> z` Toggle zoom for the current pane
  - `<C-b> [` Start scrollback. You can then press `<space>` to start a selection and `<enter>` to copy that selection.
  - `<C-b> <space>` Cycle through pane arrangements.

https://www.hamvocke.com/blog/a-quick-and-easy-guide-to-tmux/#fnref:2

https://www.hamvocke.com/blog/a-guide-to-customizing-your-tmux-conf/



alias(useful for mapping)

```bash
alias alias_name="command_to_alias arg1 arg2" #no space!!
```

```bash
# Make shorthands for common flags
alias ll="ls -lh"

# Save a lot of typing for common commands
alias gs="git status"
alias gc="git commit"
alias v="vim"

# Save you from mistyping
alias sl=ls

# Overwrite existing commands for better defaults
alias mv="mv -i"           # -i prompts before overwrite
alias mkdir="mkdir -p"     # -p make parent dirs as needed
alias df="df -h"           # -h prints human readable format

# Alias can be composed
alias la="ls -A"
alias lla="la -l"

# To ignore an alias run it prepended with \
\ls
# Or disable an alias altogether with unalias
unalias la

# To get an alias definition just call it with alias
alias ll
# Will print ll='ls -lh'
```

dotfiles&configuration

(you can also search `dotfiles` on github to get configurations)

there also other tools called symlink,whose concept means that you can git all your dotfiles in a folder, and the commands will point to those dotfiles like a trick.in this way, you make it possible to keep every dotfiles neat.



remote machines

SSH 

SSH keys



Frameworks

# Lecture 6 Version Control(git)

before i learn this lesson,i master how to switch between tabs in chrome,using `ctrl 1`or`ctrl tab`.

tree blobs

merge conflicts

---

notes from class notes

**Snapshots trees blobs**

```
<root> (tree)
|
+- foo (tree)
|  |
|  + bar.txt (blob, contents = "hello world")
|
+- baz.txt (blob, contents = "git is wonderful")
```

**Commit merge branch**

```
o <-- o <-- o <-- o <---- o
            ^            /
             \          v
              --- o <-- o
```

**Data Model**

```
// a file is a bunch of bytes
type blob = array<byte>

// a directory contains named files and directories
type tree = map<string, tree | blob>

// a commit has parents, metadata, and the top-level tree
type commit = struct {
    parents: array<commit>
    author: string
    message: string
    snapshot: tree
}
```

**Object, and content-addressing(using SHA-1 hash)**

```
type object = blob | tree | commit

objects = map<string, object>

def store(object):
    id = sha1(object)
    objects[id] = object

def load(id):
    return objects[id]
```

**References**

```
references = map<string, string>

def update_reference(name, id):
    references[name] = id

def read_reference(name):
    return references[name]

def load_reference(name_or_id):
    if name_or_id in references:
        return load(references[name_or_id])
    else:
        return load(name_or_id)
```

then, repository is the combination of objects and references.

## Basics

- `git help <command>`: get help for a git command

- `git init`: creates a new git repo, with data stored in the `.git` directory

- `git status`: tells you what’s going on

- `git add <filename>`: adds files to staging area

- `git commit`

  : creates a new commit

  - Write [good commit messages](https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html)!
  - Even more reasons to write [good commit messages](https://chris.beams.io/posts/git-commit/)!

- `git commit -a`:automatically add untracked files and commit

- `git log`: shows a flattened log of history

- `git log --all --graph --decorate`: visualizes history as a DAG

- `git diff <filename>`: show changes you made relative to the staging area

- `git diff <revision> <filename>`: shows differences in a file between snapshots

- `git checkout <revision>`: updates HEAD and current branch

- `git mv file_from file_to`: rename files in git



## Branching and merging

- `git branch`: shows branches

- `git branch <name>`: creates a branch

- ```plaintext
  git checkout -b <name>
  ```

  : creates a branch and switches to it

  - same as `git branch <name>; git checkout <name>`

- `git merge <revision>`: merges into current branch

- `git mergetool`: use a fancy tool to help resolve merge conflicts

- `git rebase`: rebase set of patches onto a new base



## Remotes

- `git remote`: list remotes
- `git remote add <name> <url>`: add a remote
- `git push <remote> <local branch>:<remote branch>`: send objects to remote, and update remote reference
- `git branch --set-upstream-to=<remote>/<remote branch>`: set up correspondence between local and remote branch
- `git fetch`: retrieve objects/references from a remote
- `git pull`: same as `git fetch; git merge`
- `git clone`: download repository from remote



## Undo

- `git commit --amend`: edit a commit’s contents/message
- `git reset HEAD <file>`: unstage a file
- `git checkout -- <file>`: discard changes

## Advanced Git

- `git config`: Git is [highly customizable](https://git-scm.com/docs/git-config)
- `git clone --depth=1`: shallow clone, without entire version history
- `git add -p`: interactive staging
- `git rebase -i`: interactive rebasing
- `git blame`: show who last edited which line
- `git stash`: temporarily remove modifications to working directory
- `git bisect`: binary search history (e.g. for regressions)
- `.gitignore`: [specify](https://git-scm.com/docs/gitignore) intentionally untracked files to ignore

## .gitignore

```text
# #表示注释 所有#和空行都会忽略
# 遵循简单的globing原则

# 忽略所有的 .a 文件
*.a

# 但跟踪所有的 lib.a，即便你在前面忽略了 .a 文件
# !表示否
!lib.a

# 只忽略当前目录下的 TODO 文件，而不忽略 subdir/TODO
/TODO

# 忽略任何目录下名为 build 的文件夹
build/

# 忽略 doc/notes.txt，但不忽略 doc/server/arch.txt
doc/*.txt

# 忽略 doc/ 目录及其所有子目录下的 .pdf 文件
doc/**/*.pdf
```

除此以外，可以在GitHub上找到别的gitignore文件。



# Lecture 7 Debugging and Profiling

https://askubuntu.com/questions/29284/how-do-i-mount-shared-folders-in-ubuntu-using-vmware-tools

```
sudo vmhgfs-fuse .host:/ /mnt/ -o allow_other -o uid=1000
sudo vmhgfs-fuse .host:/ /mnt/hgfs/ -o allow_other -o uid=1000
```

logging 

debugging

`python -m ipdb myprogram.py`

different static analyzer

flame graph

> you don't need to understand everything here, and even only be aware of these tools is useful enough.	

---

这节课实在是太难了..挑了些自己觉得现阶段能搞定的。

- shell check
- pdb调试器 for python
- 静态检查工具/自动补全




# Lecture 8 Metaprogramming

a build system

make(how to use make from .dat to .png and finally to .pdf)

```makefile
paper.pdf: paper.tex plot-data.png
	pdflatex paper.tex

plot-%.png: %.dat plot.py
	./plot.py -i $*.dat -o $@
```



repository



semantic versioning(avoiding the version conflicts.for example,the function in older versions may be deleted in newer ones.)

**8.1.7**

**major version.minor version.patch version.**

incompatible change.compatible adds or changes.bug fixes

(ex.Python2 vs Python 3.5 vs Python 3.8)

therefore,the lower the version is, maybe the better the compatibility is.



lock file

(lock some key files to avoid conflicts)

> A lock file is simply a file that lists the exact version you are *currently* depending on of each dependency. Usually, you need to explicitly run an update program to upgrade to newer versions of your dependencies. There are many reasons for this, such as avoiding unnecessary recompiles, having reproducible builds, or not automatically updating to the latest version (which may be broken). An extreme version of this kind of dependency locking is *vendoring*, which is where you copy all the code of your dependencies into your own project. That gives you total control over any changes to it, and lets you introduce your own changes to it, but also means you have to explicitly pull in any updates from the upstream maintainers over time.



continuous intergration

（有点像自动化？）

(example: github pages(also where my blog from))



mocking



从作业中学到的：

- xargs:

  ```bash
  echo hello | xargs echo # hellp transfer from input to arguments
  ```

- `git ls-files --others` # files apart from the repository

- Phony: not really a target need to construct,but a command or a request. Examples are like `clean`:

  ```makefile
  .PHONY: clean
  clean:
          rm *.o temp
  ```

  Once this is done, ‘make clean’ will run the recipe regardless of whether there is a file named clean.



# Lecture 9 Security and Cryptography

太累了..看不动了..

**entropy**

useful when determining the strength of a password.

`entropy = log_2(# of possibilities)`

**hash function**

sha1(bytes)->160 bits

```bash
sha1sum README.md # get the sha-1 value of README in Linux
```



some demands:

- non-inverted: hard to get input from output
- collision resistant: hard to find two inputs having the same output
- Target collision resistant: given an input `m_1`, it’s hard to find a different input `m_2` such that `hash(m_1) = hash(m_2)`.
- Collision resistant: it’s hard to find two inputs `m_1` and `m_2` such that `hash(m_1) = hash(m_2)` (note that this is a strictly stronger property than target collision resistance).



applications

sha1 can also be used to test the integrity of large files downloaded from the Internet.



**key derivation function (KDF)**

it should be **slow**,for fear of brute-force attacks.



**encryption decryption**

**symmetric cryptography**

```
keygen() -> key  (this function is randomized)

encrypt(plaintext: array<byte>, key) -> array<byte>  (the ciphertext)
decrypt(ciphertext: array<byte>, key) -> array<byte>  (the plaintext)
```

**asymmetric cryptography**

```
keygen() -> (public key, private key)  (this function is randomized)

encrypt(plaintext: array<byte>, public key) -> array<byte>  (the ciphertext)
decrypt(ciphertext: array<byte>, private key) -> array<byte>  (the plaintext)

sign(message: array<byte>, private key) -> array<byte>  (the signature)
verify(message: array<byte>, signature: array<byte>, public key) -> bool  (whether or not the signature is valid)
```

https://missing.csail.mit.edu/2020/security/

就这样吧，以后用到了再看。



# Lecture 10 Potpourri

> some miscellaneous items

**keyboard remapping**

the core concept is using keyboard mostly and with the optimal usage.

(for example,`CapsLock` is a rarely used key,and you can use it to remap)

Some software resources to get started on the topic:

- macOS - [karabiner-elements](https://pqrs.org/osx/karabiner/), [skhd](https://github.com/koekeishiya/skhd) or [BetterTouchTool](https://folivora.ai/)
- Linux - [xmodmap](https://wiki.archlinux.org/index.php/Xmodmap) or [Autokey](https://github.com/autokey/autokey)
- Windows - Builtin in Control Panel, [AutoHotkey](https://www.autohotkey.com/) or [SharpKeys](https://www.randyrants.com/category/sharpkeys/)
- QMK - If your keyboard supports custom firmware you can use [QMK](https://docs.qmk.fm/) to configure the hardware device itself so the remaps works for any machine you use the keyboard with.



**daemon**(programs running in the background)

(sshd->ssh daemon)

(systemd systemctl)

(cron->a daemon your system already runs to perform scheduled tasks.)   



file system

**FUSE**

Some interesting examples of FUSE filesystems are:

- [sshfs](https://github.com/libfuse/sshfs) - Open locally remote files/folder through an SSH connection.
- [rclone](https://rclone.org/commands/rclone_mount/) - Mount cloud storage services like Dropbox, GDrive, Amazon S3 or Google Cloud Storage and open data locally.
- [gocryptfs](https://nuetzlich.net/gocryptfs/) - Encrypted overlay system. Files are stored encrypted but once the FS is mounted they appear as plaintext in the mountpoint.
- [kbfs](https://keybase.io/docs/kbfs) - Distributed filesystem with end-to-end encryption. You can have private, shared and public folders.
- [borgbackup](https://borgbackup.readthedocs.io/en/stable/usage/mount.html) - Mount your deduplicated, compressed and encrypted backups for ease of browsing.



encrypted system



**backups**

google drive/RAID is not really backup(sync is not backup)

offline hardware



APIs

`curl`



**some useful common arguments**

`--help` 

`--version` 

`--verbose`->print more detailed info

 `--silent`->only print when having errors

`-i`->interactive mode,in which the shell will inform you every time you have a dry run(where the command couldn't undo)

`-r`->recursive flag,especially useful in destructive commands like `rm` or `cp`

however,sometimes we meet with the situation,where the filenames are the same as the arguments, like `-i`.the solution is, using `--`:

```bash
rm -i # a flag
rm -- -i # won't interpret, consider as a name
```

In many tools, `-` in place of a file name means “standard input” or “standard output”, depending on the argument.



**windows manager**

using keyboard instead of mouse



**VPN**

danger: being tracked,or don't encrypted



**Markdown**

good for learning



**hammerspoon**

(a powerful desktop automation framework for MacOS)



**boot up in a live USB**



**virtual machine/Docker**



**notebook programming environment**

https://jupyter.org/try

https://www.wolfram.com/mathematica/

适用于交互性的开发，比如有利于小的函数的debug和测试



**Github**

issue & pull request



# Lecture 11 Q&A

using keyboard more ,using mouse less.

reduce repetitive operations





