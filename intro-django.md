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
	- [1.1 Models](#models_top)
	- [1.2 Views](#views_top)
	- [1.3 Templates](#templates_top)
	- [1.4 URLs](#urls_top)
- 	[2.0 Starting our Application](#starting)
	- [2.1 Creating a Project](#creating)
	- [2.2 File Structure](#filestructure)
	- [2.3 Running the Server](#server)
-	[3.0 Views, URLs, and Templates](#views)
	- [3.1 Hello World!](#helloworld)
	- [3.2 URL Patterns](#urls)
	- [3.3 Dynamic Content](#content)
	- [3.4 Templates](#templates)
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
<a id="install"></a>
## 0.0 Installing Django

While this talk does not require you to follow along, it will help to learn in the learning process. If you don't already have Django installed on your computer, here are some resources that will help in installing it.

<a id="mac"></a>
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

<a id="windows"></a>
###0.2 Windows

While Django is often harder to install on Windows, it is still very simple and can be completed in just a few steps. After ensuring that Python is installed by visiting the above link, simply go to [this simple tutorial](windows-install) allows you to install Django on a windows machine in just a few minutes.

It, however, requires the installation of [SVN](svn) and [Exemaker](exe). If you have any questions about installing these, both websites provide good documentation, or email [me](mailto:matthew@adicu.com) with any questions.

-----
<a id="structure"></a>
## 1.0 The Structure of a Django Application
Many of you have probably heard of the [Model-View-Controller](mvc) framework in Software Development. Basically what it means is that the model is meant to represent, or "model", the data, the view is meant to visually represent the content, and the controller is meant to link the user and the interface.

Django uses its own adaptation of this framework, known as the "Model-View-Template" framework. We will explain what each one of these means here.

<a id="models_top"></a>
### 1.1 Models
Models in Django represent data that is stored in a database. Things like Users, Documents, Locations (think nouns). We write models to "model" the data we want to store for later. These classes, written in Python, allow us to create, retrieve, update, and delete records from our database very easily. For those of you who have taken Java, think objects in Object-Oriented Programming.

<a id="views_top"></a>
### 1.2 Views
Views are generally the point that Django begins to stray from the MVC framework. In Django, rather than being a way to visually present content, views are used to provide the data to the visual template. In Python, we see these as functions that are called before a page is loaded. For example, if you were building a social media site that had a User Profile page, a function called something like `profile()` would exist that would be called whenever our User Profile page was loaded. The function would then be responsible for providing information like the user's name or profile picture to the page. In this way, we can see our view function as providing the data that a visual representation needs.

<a id="templates_top"></a>
### 1.3 Templates
Templates, then, are the visual representations that we referred to in the last section. For our User Profile page, we would need a kind of "template" that would structure our data visually. We would need a basic page that could later be supplied with the user's name or how many friends they have. The template, then, is generic and can later be filled in with whatever data we pass it. In Django, the template, then, is a simply HTML page that is modified slightly to fit with the MVT model we are used.

<a id="urls_top"></a>
### 1.4 URLs
Although they do not fall under the MVT framework we have been discussing, URLs are very important to Django. They essentially link URLs, as they are typed in to a search box on a browser, to a specific view function. For example, if my site were named `www.facetagram.com` and I wanted my users to see their profile when they went to `www.facetagram.com/profile`, I could specify that whenever a user visits that particular URL, my `profile()` view function would be called.

-----
<a id="starting"></a>
## 2.0 Starting our Application

To gain a better understanding of how these parts fit together, we will now begin our sample Django application. This application will be a simple implementation of a Twitter-like application. Users will be able to see a news feed on their homepage of "tweets" that other users have shared. By building this, we will be able to become much more familiar with each one of these parts and how they are implemented in our Python framework.

<a id="creating"></a>
### 2.1 Creating a Project
Once you have Django installed, it is very simple to create a new project. Simply type the following into your command line:

``` bash
$ django-admin.py startproject myproject
```

The project name, in this case 'my-project', can be anything that you would like. Once you have run this command, Django will create a new directory for you. To enter that directory, type:

``` bash
$ cd myproject
```

or whatever you named your project. We now have our first Django project!
<a id="filestructure"></a>
### 2.2 File Structure
Here is a basic file structure for a Django project:

	ProjectName/
	├── manage.py
	├── ProjectName/
	│   ├── __init__.py
	│   ├── settings.py
	│   ├── urls.py
	│   └── wsgi.py
	
By typing `ls` within your directory you should see these files.

The `manage.py` in the main project directory file contains some utilities we will use later to sync our databases, to create new models, etc. You should never have to edit the file, though, so don't worry at all about it.

If we move into our `myproject` sub-directory, we will see some more files:

`__init__.py` is an empty file that is required for Python to treat the directory as a package. You will generally not add anything to this file.

`settings.py` is one of the most important files in our entire project. It defines the configuration for our application, including information about our database, where we store our templates and other files, among many other things. 

`urls.py` is the file that links our views to particular URLs for our web addresses.
<a id="server"></a>
### 2.3 Running the Server
Now that we understand the different parts of our Django application, we can run our application server. To do this, simply type the following:

``` bash
$ python manage.py runserver
```

Then, visit the link `127.0.0.1:8000/` in your browser, and if everything is working, you should see the "It Worked!" default page that Django provides for us.

-----
<a id="views"></a>
## 3.0 Views, URLs, and Templates
Now that we have gotten Django up-and-running and you have an understanding of its different parts, let's start programming! 
<a id="helloworld"></a>
### 3.1 Hello World!
To start, we will get Django to show us a basic page that says "Hello World!". First, start by creating a new file in our project sub-directory, so that the new file structure works as follows:

	ProjectName/
	├── manage.py
	├── ProjectName/
	│   ├── __init__.py
	│   ├── settings.py
	│   ├── urls.py
	│   ├── views.py	
	│   └── wsgi.py
	
Inside of this views function, type the following:

``` python
from django.http import HttpResponse

def hello(request):
	return HttpResponse("Hello World!")
```

The first thing we do is import the class HttpResponse, which is used to issue a response from the HttpRequest that is passed to us, named `request`. This is pretty simple to think about: each view takes a request from the server, to which it must give a response. In this case, our response is a simple string that says "Hello World!". 

Now that we have written our view, we have to link it to a particular URL, so that the users can access the page. So, open up yours `urls.py` file, which will look something like this:

``` python
from django.conf.urls import patterns, include, url

# Uncomment the next two lines to enable the admin:
# from django.contrib import admin
# admin.autodiscover()

urlpatterns = patterns('',
    # Examples:
    # url(r'^$', 'myproject.views.home', name='home'),
    # url(r'^myproject/', include('myproject.foo.urls')),

    # Uncomment the admin/doc line below to enable admin documentation:
    # url(r'^admin/doc/', include('django.contrib.admindocs.urls')),

    # Uncomment the next line to enable the admin:
    # url(r'^admin/', include(admin.site.urls)),
)
```

You see that Django is very helpful in provided examples that are commented out. From this, we can easily recreate an example for our simple function: Add the following inside of the parentheses along with the other URLs, so that your new file looks like this:

``` python
from django.conf.urls import patterns, include, url

# Uncomment the next two lines to enable the admin:
# from django.contrib import admin
# admin.autodiscover()

urlpatterns = patterns('',
    # Examples:
    # url(r'^$', 'myproject.views.home', name='home'),
    # url(r'^myproject/', include('myproject.foo.urls')),

    # Uncomment the admin/doc line below to enable admin documentation:
    # url(r'^admin/doc/', include('django.contrib.admindocs.urls')),

    # Uncomment the next line to enable the admin:
    # url(r'^admin/', include(admin.site.urls)),
    url(r'^hello/', 'myproject.views.hello', name='hello'),
)
```

What is inside of these URL is called a regular expression. It is basically a way to match certain patterns in text, in this case the names of URLs. What we did in that last line that we added was specify that whenever someone goes to our website named followed by 'home/', the request will be redirected to the `hello` view, which we just wrote, which sites in the `myproject.views.hello` module, in this case. To make it easier, we could also import the entire `myproject.views` module, but by specifying the entire path, we gain a better understanding of how the file system is laid out.

To see our new page, return to the directory in which `manage.py` sits, and run our command again:

``` bash
$ python manage.py runserver
```

If there are no errors, when you visit `http://127.0.0.1:8000/hello`, you should see the "Hello World!" page that we just created.
<a id="urls"></a>
### 3.2 URL Patterns

To give a better understanding of how we write our URL patterns, we must first understand how requests are processed in Django.

In our `settings.py` file, we specify where our URLs file should be, which is by default in the `myproject.urls` file. When the Django server gets a request, it searches the `urls.py` file for a URL that matches the link that was typed in to the search box. Once the server finds a match, it sends its request to the view function associated with that URL, which then issues its own response. If you go to a URL we haven't specified, you will get an error.

Now, let's begin to gain a better understanding of the regular expressions we used. In the URL that we wrote before:

``` python
url(r'^hello/', 'myproject.views.hello', name='hello')
```

the `r'^hello/` is the part that is known as a regular expression. The '^' character, in regular expressions, represents the start of the string we are inputting, in this case the part of the URL that follows the site name. More information about regular expressions can be seen [here](regex). 

To add one more basic regular URL, let's add a URL to match our site root, in this case meaning `http://127.0.0.1:8000/`. To do this, add the following to the `urls.py` file:

``` python
url(r'^$', 'myproject.views.home', name='home',)
```

so that your final file looks something like:

``` python
from django.conf.urls import patterns, include, url

# Uncomment the next two lines to enable the admin:
# from django.contrib import admin
# admin.autodiscover()

urlpatterns = patterns('',
    # Examples:
    # url(r'^$', 'myproject.views.home', name='home'),
    # url(r'^myproject/', include('myproject.foo.urls')),

    # Uncomment the admin/doc line below to enable admin documentation:
    # url(r'^admin/doc/', include('django.contrib.admindocs.urls')),

    # Uncomment the next line to enable the admin:
    # url(r'^admin/', include(admin.site.urls)),
    url(r'^hello/', 'myproject.views.hello', name='hello'),
    url(r'^$', 'myproject.views.home', name='home'),
)
```

In this, we used a dollar sign character, which is meant to simply to match the end of the string. The exact meaning is not important, however, as most of the expressions you will be writing will be quite simple.

<a id="content"></a>
### 3.3 Dynamic Content
In the previous line, we specified our the base URL of our site, `http://127.0.0.1:8000`, to point to a view function called `home()`. If we try to visit our URL now, we get an error because we haven't implemented our function yet. Let's implement it now, but with some dynamic content. 

The best part about Django is that it makes dynamic content simple to create. To show this, let's make a simple page that displays the current date and time.

To start, go back to our `views.py` file and type the following:

``` python
from django.http import HttpResponse
import datetime

def hello(request):
	return HttpResponse("Hello World!")
	
def home(request):
	now = datetime.datetime.now()
	html = "<html><body>It it now %s.</body></html>" % now
	return HttpResponse(html)
```

Thhere are a few things we must notice about the changes we have made. First, we imported `datetime`, which is a module in Python responsible for, you guessed it, providing the date and time. In our `home` function, we call a method called `now()` to store the current date and time into a variable. Next, we construct our response string. Notice this time, instead of simply returning a string, this time we return some HTML. This shows that `HttpResponse` can take any type of string. We add in the time to our page using the '%', and then return it. Now, start your server and go to your site, and check our new homepage. Refresh the page, and you will see it change. Pretty cool, right? You have just made your first dynamic webpage in Django!
<a id="templates"></a>
### 3.4 Templates
As you can probably imagine, once we get into large applications, it would be incredibly unrealistic to type all of our HTML into a simple string and return it. For this, we use templates! 

A template, in its most basic form, is an HTML page. However, they are much more than that. We can use templates to display variables, loop through information, make decisions using if's and else's, and much more. While this tutorial does not cover all of the functionality of Django templates, much more can be read about them [here](templates). 

Let's write an incredibly simple template for a page that will display a random number from 1 to 6, simulating a dice roll. Before we start, make sure you are in your base project directory (i.e. the one that contains `manage.py`). Create a new directory called `templates`, so your new file structure looks as follows:

	ProjectName/
	├── manage.py
	├── ProjectName/
	│   ├── __init__.py
	│   ├── settings.py
	│   ├── urls.py
	│   ├── views.py	
	│   └── wsgi.py
	├── templates/
	
You can do this simply by typing:

``` bash
$ mkdir templates
``` 

Now, enter this directory using `cd` and create a new file called `home.html`, and type the code as follows:

``` html
<html>
	<head>
		<title>Home</title>
	</head>
	<body>
		<h1>This is my first template!</h1>
		<p>Your random number is {{random}}</p>
	</body>
</html>
```

This is a simple HTML page, that includes a simple title and a header. The interesting part is enclosed in the paragraph tag. We see inside of a two pairs of curly braces a variable name called `random`. What this means is that our view will pass us a variable called 'random', which, when the page is loaded, will be placed where random is placed. 

Now that we have our template written, let's write our view:


``` python
from django.http import HttpResponse
import random
from django.shortcuts import render_to_response

def hello(request):
	return HttpResponse("Hello World!")
	
def home(request):
	rand = random.randint(1,6)
	c = {}
	c['random'] = rand
	return render_to_response('home.html', c)
```

Notice we have replaced the code in our `home(request)` function. First, we imported random, a module used in Python used to generate random numbers. Next, we imported a function called `render_to_response` from a module called `django.shortcuts`. This function is very useful for rendering a template in python while being able to pass a dictionary of data to the template. 

In our `home(request)` function, we generate a random number from 1 to 6, and store it in a variable. We then instantiate an empty dictionary, which we call 'c'. We then add our random number to the dictionary using the key 'random'. Notice, this is the same variable name we used in our template. We then use our function to render our template by passing the template name, in this case 'home.html', along with our corresponding data dictionary. Once our template is rendered, our template will be able to access by name the data that we passed. That is why we used the name 'random'.

<a id="loading"></a>
### 3.5 Loading Templates

We are almost ready to see our new dynamic page. However, there is one more step. In the previous section, we created a directory called 'templates'. Also, inside of our `views.py` file, we specified our template as simply `home.html`. In order for Django to find this folder, we need to specify where we keep our templates. To do this, we must modify our `settings.py` file. In order to do this, open the file and scroll down to the part that says `TEMPLATE_DIRS` in all caps. Modify it to something like this:

``` python
TEMPLATE_DIRS = (
    # Put strings here, like "/home/html/django_templates" or "C:/www/django/templates".
    # Always use forward slashes, even on Windows.
    # Don't forget to use absolute paths, not relative paths.
    'home/django/myproject/templates',
)
```

In this part of the file, we simply specify the path to our template directory. Remember to use the absolute path; this is very important, as Django will not be able to find your templates otherwise. Do not worry about the other parts of the `settings.py` file for now; we will explain it in later sections.

Now that we have added this to our file, save your changes to both your `home.html` and `views.py`, then start our server. Go to your site's homepage, and you should see your new page. Refresh a few times and you will see that the number changes. This is because a new number is being passed to our template each time we load the page.

There are many other ways to render templates in Django; we simply chose `render_to_response` because it is simple and easy to explain. You can go to the official documentation on [templates](templates) to learn some alternative ways render templates.

-----




[python-install]: http://python.org/download/releases/2.7.6/
[adi]: http://www.adicu.com
[django]: https://www.djangoproject.com
[djangobook]: http://www.djangobook.com/en/2.0/index.html
[install-django]: https://www.djangoproject.com/download/
[svn]: http://sourceforge.net/projects/win32svn/
[windows-install]: http://effbot.org/zone/django.htm
[mvc]: http://www.codinghorror.com/blog/2008/05/understanding-model-view-controller.html
[regex]: http://www.webforefront.com/django/regexpdjangourls.html
[templates]: https://docs.djangoproject.com/en/dev/topics/templates/
