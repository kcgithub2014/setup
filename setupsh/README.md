# `setupsh`

> Install & update your dotfiles, aliases, functions, preferences, apps, everything with a command.

One command to:

- link your **dotfiles**,
- make available convenient **commands for cli** (_functions & aliases_),
- install **apps** & setup apps **preferences**,
- use some shell **recipes to setup your OS** & some programs.

It does everything you need to get your computer ready to use.

## First run

```console
$ curl -fsSL https://rawgit.com/MoOx/setupsh/master/firstrun | zsh -s $USER/setup
```

## Periodic run

```console
$ setupsh-update && setupsh-run
```

---

## Help

### I'm not familiar with bash/zsh, is there any interesting tutorial you can share ?

[linuxconfig.org/bash-scripting-tutorial](http://linuxconfig.org/bash-scripting-tutorial) is a nice one.


### Find some `defaults write`

http://superuser.com/questions/455755/how-to-explore-more-defaults-write-tweaks-on-os-x

For most non-hidden settings, this is how you can find the correct preference keys in Terminal.app:

```console
$ defaults read > a
# Change the setting
$ defaults read > b
$ diff a b
```

For hidden settings, it gets trickier. You can use the command-line strings utility
on any binary executable and see if any of the resulting text looks like a preference key.
E.g.:

    strings /System/Library/CoreServices/Finder.app/Contents/MacOS/Finder

Here’s another example that will look through all .framework files in /System/Library/Frameworks/
and filter the output somewhat:

    strings /System/Library/Frameworks/*.framework/Versions/Current/* /System/Library/Frameworks/*/Frameworks/*/Versions/Current/* 2> /dev/null | grep -E '^[a-zA-Z0-9_.-]{10,80}$' | sort | uniq

There’s also a tool called GDB which can be used to find hidden preferences.
