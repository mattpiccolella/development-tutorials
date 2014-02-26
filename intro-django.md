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
-	[5.0 Putting it all Together: Forms](#forms)
	- [5.1 Normal HTML Forms](#html)
	- [5.2 Writing Django Forms](#django_forms)
	- [5.3 Writing our Template](#user_template)
	- [5.4 Our App](#our app)
	
	
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
    '/home/django/myproject/templates',
)
```

In this part of the file, we simply specify the path to our template directory. Remember to use the absolute path; this is very important, as Django will not be able to find your templates otherwise. Do not worry about the other parts of the `settings.py` file for now; we will explain it in later sections.

Now that we have added this to our file, save your changes to both your `home.html` and `views.py`, then start our server. Go to your site's homepage, and you should see your new page. Refresh a few times and you will see that the number changes. This is because a new number is being passed to our template each time we load the page.

There are many other ways to render templates in Django; we simply chose `render_to_response` because it is simple and easy to explain. You can go to the official documentation on [templates](templates) to learn some alternative ways render templates.

-----
<a id="models"></a>
## 4.0 Models
Now that we know how to process data and pass it to our templates, let's work on making some data and storing that data so we can use it for later. For this, we use models.
<a id="database"></a>
### 4.1 Configuring the Database
Before we can create out model and start creating our application, we need to first configure our database to store the information we want it to. To do this, open up your `settings.py` file and edit the portion called `DATABASES`:

``` python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.', # Add 'postgresql_psycopg2', 'mysql', 'sqlite3' or 'oracle'.                                                    
        'NAME': '',                      # Or path to database file if using sqlite3.                                                                    
        # The following settings are not used with sqlite3:                                                                                              
        'USER': '',
        'PASSWORD': '',
        'HOST': '',                      # Empty for localhost through domain sockets or '127.0.0.1' for localhost through TCP.                          
        'PORT': '',                      # Set to empty string for default.                                                                              
    }
}
```

We see that Django comes with some default comments that help us to understand what we need to do to configure our database. For this simple application, we will use sqlite3, which is a SQL database that is stored locally in a file, rather than on its own server like MySQL. To configure, we simply add 'sqlite3' to the end of our `ENGINE` line and add the path on your computer to the location we want to store the database (normally in our project directory). We can call our file something like 'database.db'. Our finalized configuration should look something like this:

``` python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3', # Add 'postgresql_psycopg2', 'mysql', 'sqlite3' or 'oracle'.                                                    
        'NAME': '/Users/Matt/Desktop/django-tutorial/myproject/database.db',                      # Or path to database file if using sqlite3.                                                                    
        # The following settings are not used with sqlite3:                                                                                              
        'USER': '',
        'PASSWORD': '',
        'HOST': '',                      # Empty for localhost through domain sockets or '127.0.0.1' for localhost through TCP.                          
        'PORT': '',                      # Set to empty string for default.                                                                              
    }
}
```
<a id="app"></a>
### 4.2 Creating our First App
Now that our database settings are configured, let's start our application. To do this, type the following into your Terminal in the home directory of your project:

``` bash
$ python manage.py startapp sampletwitter
```

If we look at our project directory, we will see that we have a new directory called 'sampletwitter' with the following structure:

	sampletwitter/
	├── __init__.py
	├── models.py
	├── tests.py
	├── views.py
	
We have explained what each of these files does already, except for `tests.py`, which is self-explanatory. In this tutorial, we will be only worrying about models.py; we can write our views in our previous `views.py` file and we won't need to worry about testing. Open your `models.py` file and you should see something like this:

``` python
from django.db import models

# Create your models here. 
```

To start, let's add a model for an author. We are going to have authors for our tweets, so we should probably store those. Here, we create a model for 'author':

``` python
from django.db import models

class Author(models.Model):
	first_name = models.CharField(max_length=30)
	last_name = models.CharField(max_length=40)
```

This is about as simple a model as we will see; an author simply stores two strings, one for the first name and one for the last name. Now, let's add a model to represent a 'tweet:':

``` python
from django.db import models

class Author(models.Model):
	first_name = models.CharField(max_length=30)
	last_name = models.CharField(max_length=40)

class Tweet(models.Model):
	tweet = models.CharField(max_length=140)
	author = models.ForeignKey(Author)
```

In this, we see it is very similar to the Author model, except for the inclusion of something called a foreign key. A foreign key is essentially a way to link a Tweet to an Author, in that a Tweet HAS-AN Author.

Before we finish, we need to come up with a way to create new objects. For this, we use a class method called 'create':

``` python
from django.db import models

class Author(models.Model):
	first_name = models.CharField(max_length=30)
	last_name = models.CharField(max_length=40)
	@classmethod
	def create(cls, first_name, last_name):
		author = cls(first_name=first_name,last_name=last_name)
		return author

class Tweet(models.Model):
	tweet = models.CharField(max_length=140)
	author = models.ForeignKey(Author)
	@classmethod
	def create(cls, tweet, author):
		tweet = cls(tweet=tweet, author=author)
		return tweet
```

This completes our `models.py` file. Now, before we sync our database to contain our new models, we just have to add our 'sampletwitter' app to the `INSTALLED_APPS` tuple in our `settings.py`:

``` python
INSTALLED_APPS = (
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.sites',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    # Uncomment the next line to enable the admin:                                                                                                       
    # 'django.contrib.admin',                                                                                                                            
    # Uncomment the next line to enable admin documentation:                                                                                             
    # 'django.contrib.admindocs', 
    'sampletwitter',                                                                                                                       
)
```

Once this file is saved, go into your Terminal and type the following command in your project directory:

``` bash
$ python manage.py syncdb
```

You will see Django will create lots of different tables for you. It will also ask you to create a user for the database. This is important! Doing this now will allow us to access our admin interface later.

<a id="access"></a>
### 4.3 Basic Data Access
To show a basic demonstration of how we will access this data, let's open up our Django shell by typing the following:

``` bash
$ python manage.py shell
```

Once you type this, you should see several carots appear. Let's now create our first model:

``` bash
>>> from sampletwitter.models import Author, Tweet
>>> a1 = Author.create("Matt", "Piccolella")
>>> a1.save()
>>> authors = Author.objects.all()
>>> authors
[<Author: Author object>]
```

First, we import the modules we need for our models. Then, we create our first author object, giving it a first and a last name. Then, we save it to the database using our `save()` function. Then, we query the database for all its authors by using the call to `Author.objects.all()`. We then print that object, which shows us a single author object, the one that we just created. This same thing can be 

<a id="enable"></a>
### 4.4 Enabling Admin
While we can see these objects from the Django shell, it would make more sense if we could see this pieces of information in a better interface. This is exactly what the Django admin interface is for! By taking a few simple steps, we can ensure that we can see all the information that we need to. 

First, go back to your `settings.py` file to our list of installed apps. Uncomment the two lines where instructured so our line looks as follows:

``` python
INSTALLED_APPS = (
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.sites',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    # Uncomment the next line to enable the admin:                                                                                                       
    'django.contrib.admin',                                                                                                                            
    # Uncomment the next line to enable admin documentation:                                                                                             
    'django.contrib.admindocs', 
    'sampletwitter',                                                                                                                       
)
```

Next, go to our `urls.py` file and uncomment the two lines at the top as well as the two lines at the bottom, as instructed, so our new file looks like this:

``` python 
from django.conf.urls import patterns, include, url

# Uncomment the next two lines to enable the admin:                                                                                                      
from django.contrib import admin
admin.autodiscover()

urlpatterns = patterns('',
    # Examples:                                                                                                                                          
    # url(r'^$', 'myproject.views.home', name='home'),                                                                                                   
    # url(r'^myproject/', include('myproject.foo.urls')),                                                                                                

    # Uncomment the admin/doc line below to enable admin documentation:                                                                                  
    url(r'^admin/doc/', include('django.contrib.admindocs.urls')),

    # Uncomment the next line to enable the admin:                                                                                                       
    url(r'^admin/', include(admin.site.urls)),
    url(r'^$', 'myproject.views.home', name='home'),
)
```

Once we make these changes, run our server again by typing from the project directory:

``` bash
$ python manage.py runserver
```

Now, visit `http://127.0.0.1:8000/admin`, and log in with the username you created earlier. Pretty awesome, right? From within here, we can view already created objects, we can create new objects, or even delete old objects. 

However, there's just one problem: we can't see our Author and Tweet object tables. For this, we need to make one correction.

<a id="registering"></a>
### 4.5 Registering our Models
To see our models on our Admin site, we simply have to register our models. We do this by creating a file called `admin.py` inside of our `sampletwitter` application. In this file, we type the following:

``` python
from django.contrib import admin
from models import Author, Tweet

class AuthorAdmin(admin.ModelAdmin):
    list_display = ('first_name', 'last_name')
    search_fields = ('first_name', 'last_name')

class TweetAdmin(admin.ModelAdmin):
    list_display = ('tweet', 'author')
    search_fields = ('tweet',)

admin.site.register(Author, AuthorAdmin)
admin.site.register(Tweet, TweetAdmin)
```

First, we import the modules that we need. Then, we create new Admin objects for each of our two models. We do not need to do this, but it adds some functionality to our admin site, including the ability to be able to search our tables. Once we save this and run our server again, we will be able to see our app models registered in the site. Click on "Author" and you will see the Author object we created earlier.

------
<a id="forms"></a>
## 5.0 Forms
One of the most important parts of web development is being able to get input from our users. Django provides a simple way for dealing with forms in a way that avoids writing the same code over and over again.

<a id="html"></a>
### 5.1 Normal HTML Forms
In normal HTML, this is normally a pretty tedious task that consists of writing things like this over and over again:

``` html
<html>
    <head>
        <title>Search</title>
    </head>
    <body>
        <form action="/search/" method="get">
            <input type="text" name="q">
            <input type="submit" value="Search">
        </form>
    </body>
</html>
```

In Django, we can get these results in a view. Say we have the URL `/search/`, that we call on submit, hooked up to a view function called `search`:

``` python
def search(request):
    if 'q' in request.GET:
        message = "You searched for: %r" % request.GET['q']
    else:
        message = "You submitted an empty form."
    return HttpResponse(message)
```
As you can see from this, `request.GET` is a dictionary that contains all of the information that is passed to us by 'GET' methods from within the HTML. If we have that, then we know the user submitted the form. If they didn't, then we know the form was an empty form.

While this can be used to write basic forms, it is still very inefficient. There will be all sorts of error handling we will have to account for; for example, say there is a user registration form that has many fields. We want to be able to give particular error messages without having to customize this every time. For this, we can use Django Form classes.

<a id="django_forms"></a>
### 5.2 Writing Django Forms
Inside of Django, there is a module called `django.forms` that allows for the functionality that we have been looking for: simple, easy-to-customize forms with automatic error handling and validation.

To begin writing our first Django form, create a file in our project sub-directory (the same folder with `settings.py` in it) called `forms.py`. Inside of it, type the following code:

``` python
from django import forms

class TweetForm(forms.Form):
    first_name = forms.CharField(max_length=30)
    last_name = forms.CharField(max_length=40)
    tweet = forms.CharField(max_length=140)
```

Once we have created this form, we can use it inside of our `views.py` folder to take care of the handling of tweets. Open up the `views.py` file and create a new function called `post_tweet` and add the code as follows:

``` python
from django.http import HttpResponse
from django.shortcuts import render_to_response
import random
from forms import TweetForm
from models import Author, Tweet
from django.views.decorators.csrf import csrf_exempt

@csrf_exempt
def post_tweet(request):
    c = {}
    if request.method == 'POST':
        form = TweetForm(request.POST)
        if form.is_valid():
            cd = form.cleaned_data
            first_name = cd['first_name']
            last_name = cd['last_name']
            tweet = cd['tweet']
            current_authors = Author.objects.filter(first_name=first_name).filter(last_name=last_name)
            if (len(current_authors) == 1):
                author = current_authors[0]
            else:
                author = Author.create(first_name=first_name, last_name=last_name)
                author.save()
            tweet = Tweet.create(tweet=tweet,author=author)
            tweet.save()
            form = TweetForm()
    else:
        form = TweetForm()
    c['form'] = form
    tweets = Tweet.objects.all()
    c['tweets'] = tweets
    return render_to_response('tweets.html', c)
``` 
This is our longest and most complicated piece of code yet, so we will go through it piece by piece. First, we import the form and our two models from their respective folders. One thing to notice is our last import: csrf. CSRF stands for cross-site registry forgery. It basically means that people can forge their registry on your site, making it a security risk. Django normally requires measures to be taken to protect against this, which ensures the safety of a site. To get around this in our simple example, we simply use the csrf_exempt decorator for our function, which we import. 

Inside of our method, we first create a dictionary, in which we can store data that is to be returned to the template. First, we check if any data has been posted to our method. If it has been, we know we will have some processing to do. If it hasn't, we instead create a blank TweetForm that will be passed to our page. 

Once we know that data has been posted, we immediately store that form into a variable, which we do using the `request.POST` dictionary. We check if the form is valid first, meaning it passes all of the validations that we established in our `forms.py` file. If it has been, we create a dictionary to hold all the data that we got from the form, only cleaned. This prevents any malicious information that could've been passed to our form from hurting our website.

Next, we take the first_name, the last_name, and the tweet objects from the form. Next, we search for `current_authors`. This means, using the data access tools we saw before, we check for all the Author objects currently defined in our database, filtering those only that have the same first_name and the same_last name as the ones we received from the form. The `current_authors` object is a list of objects from the database that matched our query. If there is an author object that currently exists in the database, meaning we saw a result from our query, we store that as author. Otherwise, if we need to create an object for a new Author, we do that using the `create` method we wrote earlier. We then set that equal to `author` and save it to the database. Once outside of that, we create a new tweet given the tweet itself and the author object, saving that to the database. If we have correctly processed all the information from our form, we can create a new blank one and pass it.

Finally, once we have our form set, either as the invalid form that was passed or a new, blank one, we can then pass it back to the page by setting it to `form` in our dictionary. But first, we want to load all the tweets that are available currently, so we can display those on our page. Once we have passed these tweets, we can then render our template, called 'tweets.html'. 

This may be hard to understand at first, but as you work more and more in Django, you will see the incredible value of these forms.

<a id="user_template"></a>
### 5.3 Writing our Template
As you may have guessed, we still have to write our `tweets.html` template. Let's write that write now:

``` html
<html>
    <head>
        <title>Tweets</title>
    </head>
    <body>
        <h1>Send us a Tweet!</h1>
        {% if form.errors %}
            <p style="color: red;">Please error the error(s) below</p>
        {% endif %}

        <form action="/tweets/" method="post">
            <table>
                {{ form.as_table }}
            </table>
            <input type="submit" value="Submit">
        </form>

        {% for tweet in tweets %}
            <h2>Tweet from {{tweet.author.first_name}} {{tweet.author.last_name}}</h2>
            <h3>{{tweet.tweet}}</h3>
        {% endfor %}
    </body>
</html> 
```

The template is pretty simple. First, we display any errors that are accompanied by our form in the top part, coloring them red. We then create our form, giving it the `/tweets/` action, a URL we will specify inside of our URLs file momentarily. We display the form as a table by calling {{ form.as_table }}. 

We then create a submit input. Then, we cycle through all of our tweets using a simple for loop. We display the name of the author, which can be accessed through the tweet's author attribute. Then we display the content of the tweet. It is quite simple to do! We do not need to worry about specifying the different input types from the form or anything like that; Django does it for us!

### 5.4 Our App
The last thing we need to do is a simple URL connection. We open up our `urls.py` file and add one more URL, to connect our `/tweets/` function to the `post_tweet` view that we wrote:

``` python
from django.conf.urls import patterns, include, url

# Uncomment the next two lines to enable the admin:                                                                                                      
from django.contrib import admin
admin.autodiscover()

urlpatterns = patterns('',
    # Examples:                                                                                                                                          
    # url(r'^$', 'myproject.views.home', name='home'),                                                                                                   
    # url(r'^myproject/', include('myproject.foo.urls')),                                                                                                

    # Uncomment the admin/doc line below to enable admin documentation:                                                                                  
    url(r'^admin/doc/', include('django.contrib.admindocs.urls')),

    # Uncomment the next line to enable the admin:                                                                                                       
    url(r'^admin/', include(admin.site.urls)),
    url(r'^$', 'myproject.views.home', name='home'),
    url(r'^tweets/', 'myproject.views.post_tweet', name='post_tweet'),
)
```

Once this is complete, we can view our app! If we enter a name and a tweet and hit submit, we see it instantly appear on our "news feed" underneath the search box. Try leaving out one of the fields; Django automatically throws the error we need to! 

Congratulations! You have now finished your first app! Albeit a simple version of Twitter, this tutorial has shown you the power of Django and will hopefully inspire you to continue to learn.

-----

## Additional Resources
Perhaps one of the best parts of Django is its strong online resources. Here are some additional resources that will help in your future learning:

[The Django Book](djangobook)

[Official Django Documentation](django)

[Django by Example](by-example)

[Getting Started with Django](getting-started)

## Sample Project Code
The entire code for the project seen here can be retrieved [here](github-code).


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
[by-example]: http://lightbird.net/dbe/
[getting-started]: http://gettingstartedwithdjango.com
[github-code]: https://github.com/mjp2220/development-tutorials/tree/master/django-code
