---
title: "Day 39"
date: 2018-10-11
tags: []
draft: false
---

# Learning Bash

Today I've decided to plunge a little deeper into the bash world.

```
mkdir hammerTime
chmod 500 hammerTime
cd hammerTime
touch this
```

#### Interactive and non-interactive modes

- Interactive: Shell commands such as; `ls`, `cd`, `mkdir`, `rm`.

- Non-interactive: Where the shell reads commands from a .bash file or a pipe and executes them.

#### Useful Commands:

- `touch` - to create a script file
- `chmod +x "<file name>"` - to create an executable file
- `man` - to query a bash command
- `which` - to search for a directory
- `cat` or `less` - to read a .txt files
- `ls` - to print current working directory
- `cd` - to change current working directory
- `pwd` - print working directory
- `echo` - to print

#### Non-interactive

- To run a script from local directory: `./<file name>.bash`
- In script files you can basically code processes to automate routines that you do on your system. Scripts can be made to input/output data to certain programmes, create files, pull data .etc.
- In this this script you can create both global and local variables to be used, however many global variables already exist in bash.
- For global variables `$<CAPITALS>` syntax is used.
- **Global variables:** `$PWD $CD $MKDIR $USER $HOME`

#### Pipelines:
Piping in bash seems useful, it's a way of directing data around programmes on one command line. The syntax pipe `|` is used for this. Similarly `>` can be used for redirecting output and `<` can be used for redirecting input.

**Right now, I can't see much personal use for writing non-interactive script, but can see the use of learning some key interactive commands.**

**In order to get a better appreciation of non-interactive scripts, I think it may help to see how a more experienced developer uses bash scripting.**
