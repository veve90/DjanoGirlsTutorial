# DjanoGirlsTutorial
I will participate to the Djsngo girls Lyon as a mentor. Therefore I will complete the Django girls tutorial before this event (:D).
This are my notes for the Djano girls Tutorial: http://tutorial.djangogirls.org/en/

## What will you learn during the tutorial?
Once you've finished the tutorial, you will have a simple, working web application: your own blog. We will show you how to put it online, so others will see your work!

## Installation
* Install Python: ```https://www.python.org/ftp/python/3.4.3/python-3.4.3.amd64.msi```
* Set up virtualenv and install Django: 
    * create a folder: ```D:\Users\agherman\Documents\djangogirls```
    * go to this folder in cmd and do ```C:\Python34\python -m venv myvenv```
    * start the virtual env: ``` myvenv\Scripts\activate```
* Install Django: ```pip install django~=1.9.0```
* Install gedit: ```http://ftp.gnome.org/pub/GNOME/binaries/win64/gedit/gedit-x86_64-3.20.1.msi```
* Create a python anywhere account: ```https://www.pythonanywhere.com```


## How the Internet works
We could compare Internet to a mailing system:
* letters = data packets
* post offices = routers
* adresses = DNS(Domain Name System) + IP

## Introduction to the command-line interface
 command line = command-line interface = cmd = CLI = prompt = console = terminal = text-based application for viewing, handling, and manipulating files on your computer.

| Command (Windows) | Command (Mac OS / Linux) | Description             | Example                                   |
|-------------------|--------------------------|-------------------------|-------------------------------------------|
| exit              | exit                     | close the window        | exit                                      |
| cd                | cd                       | change directory        | cd test                                   |
| dir               | ls                       | list directories/files  | dir                                       |
| copy              | cp                       | copy file               | copy c:\test\test.txt c:\windows\test.txt |
| move              | mv                       | move file               | move c:\test\test.txt c:\windows\test.txt |
| mkdir             | mkdir                    | create a new directory  | mkdir testdirectory                       |
| del               | rm                       | delete a directory/file | del c:\test\test.txt                      |


## Introduction to  python
* open python console: write python3 in the cmd
    * Strings: "", '', upper, len
    * Lists: [], len,sort,
    * Dictionary: {}
    * and/or...
    * boolean
    
* write some code in a new file in gedit
    * print('Hello, Django girls!')
    * If...elif...else
    * execute my file:  python3 python_intro.py
    * Methods
```
def hi(name):
    print('Hi ' + name + '!')

hi("Rachel")
```
    * Loops
```
girls = ['Rachel', 'Monica', 'Phoebe', 'Ola', 'You']
for name in girls:
    hi(name)
    print('Next girl')
    
for i in range(1, 6):
    print(i)
```
## What is Django
Django (/ˈdʒæŋɡoʊ/ jang-goh) is a free and open source web application framework, written in Python. A web framework is a set of components that helps you to develop websites faster and easier.

### What happens when someone requests a website from your server?
When a request comes to a web server it's passed to Django which tries to figure out what actually is requested. It takes a webpage address first and tries to figure out what to do. This part is done by Django's urlresolver .It is not very smart - it takes a list of patterns and tries to match the URL. Django checks patterns from top to the bottom and if something is matched then Django passes the request to the associated function (which is called view).

## Your first Django project!
```
django-admin startproject mysite .
```
* django-admin.py : is a script that will create the directories and files for you. You should now have a directory structure which looks like this:
```
djangogirls
├───manage.py
└───mysite
        settings.py
        urls.py
        wsgi.py
        __init__.py
```
* manage.py : is a script that helps with management of the site. With it we will be able to start a web server on our computer without installing anything else, amongst other things.
* settings.py file :contains the configuration of your website.
* urls.py file :contains a list of patterns used by urlresolver.
 
To create a database for our blog, let's run the following in the console:
```
python manage.py migrate
```
 In the console, we can start the web server by running
```
python manage.py runserver
```
## Django models
### Objects
So what is an object? It is a collection of properties and actions. It sounds weird, but we will give you an example.
```
Cat
--------
color
age
mood
owner
purr()
scratch()
feed(cat_food)

CatFood
--------
taste
```

So basically the idea is to describe real things in code with properties (called object properties) and actions (called methods).


In our case:
```
Post
--------
title
text
author
created_date
published_date
```
### Django model
A model in Django is a special kind of object - it is saved in the database.
You can think of a model in the database as a spreadsheet with columns (fields) and rows (data).

### Creating an application
```
python manage.py startapp blog
```
The current blog directory:
```
djangogirls
├── blog
│   ├── __init__.py
│   ├── admin.py
│   ├── apps.py
│   ├── migrations
│   │   └── __init__.py
│   ├── models.py
│   ├── tests.py
│   └── views.py
├── db.sqlite3
├── manage.py
└── mysite
    ├── __init__.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py
```

Tell Django to use this application:
(change the file mysite/settings.py)
```
INSTALLED_APPS = (
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'blog',
)

```


### Creating a blog post model
Change the blog/models.py file to this:
```
from django.db import models
from django.utils import timezone


class Post(models.Model):
    author = models.ForeignKey('auth.User')
    title = models.CharField(max_length=200)
    text = models.TextField()
    created_date = models.DateTimeField(
            default=timezone.now)
    published_date = models.DateTimeField(
            blank=True, null=True)

    def publish(self):
        self.published_date = timezone.now()
        self.save()

    def __str__(self):
        return self.title
```
* from or import are lines that add some bits from other files. So instead of copying and pasting the same things in every file, we can include some parts with from ... import ....
* class Post(models.Model): - this line defines our model (it is an object).
    * class is a special keyword that indicates that we are defining an object.
    * Post is the name of our model. We can give it a different name (but we must avoid special characters and whitespaces). Always start a class name with an uppercase letter.
    * models.Model means that the Post is a Django Model, so Django knows that it should be saved in the database.
*  Now we define the properties we were talking about: title, text, created_date, published_date and author. To do that we need to define a type of each field (Is it text? A number? A date? A relation to another object, like a User?).

    * models.CharField - this is how you define text with a limited number of characters.
    * models.TextField - this is for long text without a limit. Sounds ideal for blog post content, right?
    * models.DateTimeField - this is a date and time.
    * models.ForeignKey - this is a link to another model.
* __str__() we will get a text (string) with a Post title
### Create tables for models in your database
The last step here is to add our new model to our database
```
python manage.py makemigrations blog

```
Django prepared for us a migration file that we have to apply now to our database.

```
python manage.py migrate blog
```
