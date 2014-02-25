<a id="top"></a>
#An Introduction to Django

*Walking you through your first application in Django*

Written and developed by [Matt Piccolella](mailto:matthew@adicu.com) and [ADI](adi).

Credit to [Django Book](django-book).

-------

<a id="getting-started"></a>
## Getting Started
Before we begin, it is valuable to first understand what Django is exactly.

### What is Django?
[Django](django) is "a high-level Python Web framework that encourages rapid development and clean, pragmatic design." It includes awesome data modeling written entirely in Python, an automatic admin interface that allows you to manage content, customization of URLs, and a very powerful templating system. It is very similar to, yet much more robust than, Flask.

### What is Django used for?
Django is used primarily by complex, database-driven websites. It is used by such popular websites as Pinterest, Instagram, and the Washington Post.

### How does Django relate to other alternatives?
Many of you have probably heard of Ruby on Rails. Django is very similar to Ruby on Rails, except it is written in Python. However, Django is generally used for applications that are more data-heavy and require better database support. Django is very similar to Flask in its templating and URL linking; however, Django is much more robust and offers much more functionality.

---------
<a id="about-this-document"></a>
## Using this Document
This tutorial walks you through creating your first application in Django. It assumes that you have Python installed on your computer. If you do not have Python installed on your computer, [here](python) is where to install Python for your particular operating system.

While you don't have to be an expert programmer to understand the content in this tutorial, it is tailored to someone who knows at least one programming language, preferrably Python. The code is not complicated that is featured in this tutorial, though, so someone new will probably be able to understand it.

--------
<a id="table-of-contents"></a>
## Table of Contents
-	[0.0: Installing Django](#install)
	- [0.1: Mac](#mac)
	- [0.2: Windows](#windows)
-	[1.0 The Structure of a Django Application](#structure)
	- [1.1 Models](#models)
	- [1.2 Views](#views)
	- [1.3 Templates](#templates)
	- [1.4 URLs](#urls)
- 	[2.0 Starting our Application](#starting)
	- [2.1 Creating a Project](#creating)
	- [2.2 File Structure](#filestructure)
	- [2.3 Running the Server](#server)
-	[3.0 Views, URLs, and Templates](#views)
	- [3.1 Hello World!](#helloworld)
	- [3.2 URL Patterns](#urls)
	- [3.3 Dynamic Content](#content)
	- [3.4 Templates](#templates)
		- [3.4.1 Common Tags](#tags)
	- [3.5 Loading Templates](#loading)
- 	[4.0 Models](#models)
	- [4.1 Configuring the Database](#database)
	- [4.2 Creating our First App](#app)
	- [4.3 Basic Data Access](#access)
	- [4.4 Enabling Admin](#enable)
	- [4.5 Registering our Models](#registering)
-	[5.0 Forms and Users](#forms)
	- [5.1 Normal HTML Forms](#html)
	- [5.2 Writing Django Forms](#django)
	- [5.3 User Registration](#user)
	- [5.4 Sessions](#sessions)
	
	
----------

## 0.0 Installing Django

While this talk does not require you to follow along, it will help to learn in the learning process. If you don't already have Django installed on your computer, here are some resources that will help in installing it.

###0.1 Mac
If you already have Python and pip installed on your computer, simply type the following into Terminal:

``` bash
$ sudo pip install Django==1.6.2
```

This will, pending any other complications, install Django onto your computer. To check that it is properly installed, simply type and expect something like this for a successful installation:

``` bash
$ django-admin.py version
1.6.2
```

If you do not have pip, you can download the `.tar` file [here](install-django) and follow the appropriate instructions. 

If Python is not installed, please first follow the instructions [here](python) before installing Django by either of the above methods.

###0.2 Windows

While Django is often harder to install on Windows, it is still very simple and can be completed in just a few steps. After ensuring that Python is installed by visiting the above link, simply go to [this simple tutorial](windows-install) allows you to install Django on a windows machine in just a few minutes.

It, however, requires the installation of [SVN](svn) and [Exemaker](exe). If you have any questions about installing these, both websites provide good documentation, or email [me](mailto:matthew@adicu.com) with any questions.

-----

















[python-install]: http://python.org/download/releases/2.7.6/
[adi]: http://www.adicu.com
[django]: https://www.djangoproject.com
[djangobook]: http://www.djangobook.com/en/2.0/index.html
[install-django]: https://www.djangoproject.com/download/
[svn]: http://sourceforge.net/projects/win32svn/
[windows-install]: http://effbot.org/zone/django.htm
