+++
date = "2015-11-13T08:01:43-04:00"
title = "Learn to code with PHP"
description = "Need help getting started with PHP? Check those tips."

+++

Make sure you've read [how to code](/code-like-a-hacker/) first. Else this won't make sense.

## PHP is easy to pick up

That's what most self-taught coders and beginners learn first. Thus, code and configs one a lot of servers are messy and insecure. And since there are a lot of PHP enabled servers out there knowing your way around it is pretty useful.

Facebook, Wikipedia, and Wordpress are apps built with PHP that I'm sure you've heard of.

Also, learning PHP will help you learn other languages.

## PHP might get you a job

If you can produce decent code and are capable of working with other people you qualify as a PHP [code monkey](https://www.youtube.com/watch?v=_ZtL_KVzaao&list=PLEShoiqxQUJIblp19IU4y_9GaG5By5Sl-). It'll suck most of the time but you'll learn the ropes and have money for dates.

# Versions

Start with PHP 7 right away. It's blazing fast and there's a lot of neat features. Most servers still run PHP 5 but in a few years, it'll be all gone. Fall back to PHP 5 only if you must.

You can pick up a [pre-made PHP7 Vagrant box](https://atlas.hashicorp.com/rasmus/boxes/php7dev).

# Coding tools

Tools will make your coding life easier, but you need to know about them. Some are easy use, some aren't. At some point, you'll need to use all of them so you should at least know what they are.

## PHP build in tools

### Interactive shell

This shell allows you to type PHP code in your console that executes right away.

php -a

### Local server

You can fire up a web server from any folder on your system to run your code with a browser. It's really useful but if you need fancy stuff provided by full-fledged web servers, it won't work.

php -s localhost:8080

### PHAR archives

There's a way to packages single file executable compressed archive you can easily deploy on any system. I'm sure you can think of how a hacker can use that... It's not easy to get going at though. You'll want to start with [a tool that will help you out](https://github.com/clue/phar-composer).

## Community built tools

### Composer

Composer is a package manager for PHP to help you work with community-built software packages.

First, you need to get Composer from the [official website](https://getcomposer.org/) then you visit [Packagist](https://packagist.org/) to get the packages you need. [Packages from the Symfony framework](https://packagist.org/search/?q=symfony) are awesome and I strongly recommend you take a look at them.

### Linters

If you want to create code readable by other humans and your future self, those are your best friends. Believe me, there's nothing worse than coming back to your projects and not getting what's going on.

I recommend using [PHP Code Sniffer](https://github.com/squizlabs/PHP_CodeSniffer) with the [PSR2 coding style](http://www.php-fig.org/psr/psr-2/), especially if you work with Composer.

You can install PHPCS with Composer. Run "composer global require 'squizlabs/php_codesniffer=*'". Add "~/.composer/vendor/bin" to your executable path. Use with "phpcs --standard=psr2 file.php" to test your file.

### Frameworks

There's a lot of PHP frameworks out there and to be honest they almost always suck. I've worked with many and the only one so far that was helpful is [Laravel](https://laravel.com/). Be careful though it's not easy to pick up there's a big learning curve. Community provided guides and help can be confusing because of the many Laravel versions out there.

[Symfony](http://symfony.com/) and [Zend](http://framework.zend.com/) are also great frameworks but I would only recommend using them if you get into big projects involving more than one developer.

## Starting with basics

[CodeCademy.com](https://www.codecademy.com/learn/php) is a great site to learn. It’s free and offers different classes in many languages. That’s always where I start when picking up a new language.

## MySQL

If you're playing around with MySQL databases there are a few things you need to know.

### MySQL is dead, use MariaDB instead

Read [Dead database walking: MySQL's creator on why the future belongs to MariaDB] (http://www.computerworld.com.au/article/457551/dead_database_walking_mysql_creator_why_future_belongs_mariadb/).

Updating is as simple as "sudo apt-get remove mysql-client mysql-server ; sudo apt-get install mariadb-client mariadb-client".

### Python MyCLI

[MyCLI](https://github.com/dbcli/mycli) is a very powerful tool. It's way better than the default command line tools you'll get. To install, use "sudo apt-get install python-pip ; sudo pip install mycli". Then use as any other MySQL command line tools.
