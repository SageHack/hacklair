+++
date = "2015-07-01T10:19:22-04:00"
title = "Use the damn terminal"
description = "Tips and tricks to use your terminal efficiently."

+++

This guide is for Debian and Ubuntu but should work with any linux distribution and with OSX.

# Intro

What we, hackers, need is a portable easy and fast to install setup requiring minimal configuration. It’s also important the setup to work servers might you need it.

Here’s some tips and advice to help you out.

## Keyboard typing

To be honest, that part sucks. It’s a hard skill to acquire but **it’s the most important one**. If you can type fast, without looking at your keyboard and without typos, you’ll be like those Hollywood hackers. No software can beat that.

Klavaro is your friend. Just “apt-get install klavaro” and here you go. Check [this guide](http://www.hecticgeek.com/2011/10/a-typing-tutor-for-ubuntu-linux-klavaro/) for more info.

## Terminal emulator

Don’t use the default terminal emulator. It suck.

What we’re going to use here is Terminator. It’s not that great but it works everywhere. What we need it for is split windows. [Download it](http://gnometerminator.blogspot.ca/p/introduction.html). As you get accommodated to using the terminal you’ll need to multi task.

Make sure you change the font to something that suits you. Smaller is better as it will allow you to cram more window in your term.

At some point you’ll probably want to customize your options. Check the [terminator config](http://linux.die.net/man/5/terminator_config) manual.

## Term browsing

Yep... It’s a thing. And it’s very useful. [W3M](http://w3m.sourceforge.net/) is your friend. “apt-get install w3m” and “w3m duckduckgo.com”.

## Multiple sessions over multiple servers

Byobu is a neat software to help you manage multiple terminal sessions. It keep them alive on your local and remote machines. Once installed use the F1 key to configure, access help and use the F2, F3, F4 to create and more between windows.

Just type "apt-get install byobu". To enable by default on remote servers use "byobu-enable".

My favorite trick is keyboard copy/paste. Press F7 and move around, then press spacebar to select your text, press enter to return in normal mode. Paste with F12 and then CTRL plus ].

## Bash the shell

Bash is great and all but ZSH is greater.

The first thing you need to learn about is auto-complete. It’s what happen with you start typing a command or a path and hit the TAB key. ZSH auto-complete is freaking awesome.

Then there’s [OhMyZSH](http://ohmyz.sh). One command curl install and you’ll have a complete setup and you’ll be ready to roll. It’s a bliss. Be sure to check included themes and plug-ins.

## MySQL

If you're playing around with MySQL databases there's a few things you need to know.

### MySQL is dead, use MariaDB instead

Read [Dead database walking: MySQL's creator on why the future belongs to MariaDB] (http://www.computerworld.com.au/article/457551/dead_database_walking_mysql_creator_why_future_belongs_mariadb/).

Updating is as simple as "sudo apt-get remove mysql-client mysql-server ; sudo apt-get install mariadb-client mariadb-client".

### Python MyCLI

[MyCLI](https://github.com/dbcli/mycli) is a very powerful tool. It's way better than default command line tools you'll get. To install use "sudo apt-get install python-pip ; sudo pip install mycli". Then use as any other MySQL command line tools.


## Vim (and not Emacs)

Vim is a great code editor but... [vim.spf13](http://vim.spf3.com) made it awesome. Perfect even. Vim is hard to learn at first but it’s on all systems. You’ll be glad to know about it when you’ll start navigating in those weirds Russian servers ;)

## Color schemes

At some point you’ll want to choose and get used to a color scheme. It’s really important when you spend hours in the terminal so take your time to try some out.

[Solarized](http://ethanschoonover.com/solarized) is the most popular one. I don’t like it but it’s everywhere. You’ll always be able to use it whatever app your on.

If you need help choosing a color scheme check [Vim Colors](https://vimcolors.com).

## Powerline fonts

Some themes and softwares like Vim can take advantage of patched fonts and provide you with advanced feedback. Installing them is easy.

cd ~/Downloads ; git clone https://github.com/powerline/fonts ; cd fonts ; ./install.sh ; cd .. ; rm -fr fonts

### With ZSH

To take advantage of powerline fonts with ZSH use the agnoster theme. You'll need to edit your ~/.zshrc file.

### With SPF13 VIM

You need to create ~/.vimrc.before.local and add the following line "let g:airline_powerline_fonts=1".
