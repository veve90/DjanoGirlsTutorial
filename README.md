# DjangoGirlsTutorial
I will participate to the Djsngo girls Lyon as a mentor. Therefore I will complete the Django girls tutorial before this event (:D).
This are my notes for the Djano girls Tutorial: http://tutorial.djangogirls.org/en/

## What will you learn during the tutorial?
Once you've finished the tutorial, you will have a simple, working web application: your own blog. We will show you how to put it online, so others will see your work!

## Installation
* Install Python: ```https://www.python.org/ftp/python/3.4.3/python-3.4.3.amd64.msi```
* Set up virtualenv and install Django: 
    * create a folder: ```D:\Users\agherman\Documents\djangogirls```
    * go to this folder  ```cd /d d: ``` in cmd and do ```C:\Python34\python -m venv myvenv```
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
## Django admin
Change the blog/admin.py file to:
```
from django.contrib import admin
from .models import Post

admin.site.register(Post)
```
Run the server ``` python manage.py runserver ``` and go to ```http://127.0.0.1:8000/admin```
Since we hanven't created a user we can't authentificate. Let's create it!
```
python manage.py createsuperuser
```
Use for example as a password: django123

Run agin the server ``` python manage.py runserver ``` and go to ```http://127.0.0.1:8000/admin```
and create 6 posts, 3 with the publish date set.

## Deploy!
Until now, your website was only available on your computer. Now you will learn how to deploy it! Deploying is the process of publishing your application on the Internet so people can finally go and see your app :).


As you learned, a website has to be located on a server. There are a lot of server providers available on the internet. We will use one that has a relatively simple deployment process: PythonAnywhere. PythonAnywhere is free for small applications that don't have too many visitors so it'll definitely be enough for you now.

The other external service we'll be using is GitHub, which is a code hosting service. There are others out there, but almost all programmers have a GitHub account these days, and now so will you!

### Git
```
$ cd /d d:
$ cd Users\agherman\Documents\djangogirls

$ git init
Initialized empty Git repository in ~/djangogirls/.git/
$ git config --global user.name "Your Name"
$ git config --global user.email you@example.com
```

Git will track changes to all the files and folders in this directory, but there are some files we want it to ignore. We do this by creating a file called .gitignore in the base directory. Open up your editor and create a new file with the following contents:
```
*.pyc
__pycache__
myvenv
db.sqlite3
/static
.DS_Store
```
In order to create this gitignore file: 
* Create the text file gitignore.txt
* Open it in a text editor and add your rules, then save and close
* Hold SHIFT, right click the folder you're in, then select Open command window here
* Then rename the file in the command line, with ```ren gitignore.txt .gitignore```
 

```
 git status
 git add --all .
 git commit -m "My Django Girls app, first commit"
 git remote add origin https://github.com/veve90/DjanoGirlsTutorial.git
 git push -u origin master
 
```


### Setting up our blog on PythonAnywhere
We will put our code from girt to pythonanywhere
```
git clone https://github.com/veve90/DjanoGirlsTutorial.git
tree DjanoGirlsTutorial
```

### Creating a virtualenv on PythonAnywhere
```
cd DjanoGirlsTutorial
virtualenv --python=python3.4 myvenv
source myvenv/bin/activate
pip install django~=1.9.0

```
### Creating the database on PythonAnywhere
```
python manage.py migrate
python manage.py createsuperuser
```

### Publishing our blog as a web app
Click back to the PythonAnywhere dashboard by clicking on its logo, and go click on the Web tab. Finally, hit Add a new web app.

After confirming your domain name, choose manual configuration (NB not the "Django" option) in the dialog. Next choose Python 3.4, and click Next to finish the wizard.
#### Setting the virtualenv
In the "Virtualenv" section, click the red text that says "Enter the path to a virtualenv", and enter: ```/home/<your-PythonAnywhere-username>/my-first-blog/myvenv/```. Click the blue box with the check mark to save the path before moving on.


#### Configuring the WSGI file
Django works using the "WSGI protocol", a standard for serving websites using Python, which PythonAnywhere supports. The way we configure PythonAnywhere to recognise our Django blog is by editing a WSGI configuration file.

Put this as a WSGI file:
```
import os
import sys

path = '/home/<your-PythonAnywhere-username>/my-first-blog'  # use your own PythonAnywhere username here
if path not in sys.path:
    sys.path.append(path)

os.environ['DJANGO_SETTINGS_MODULE'] = 'mysite.settings'

from django.core.wsgi import get_wsgi_application
from django.contrib.staticfiles.handlers import StaticFilesHandler
application = StaticFilesHandler(get_wsgi_application())
```
## Django URLs

Every page on the Internet needs its own URL. This way your application knows what it should show to a user who opens a URL. In Django we use something called URLconf (URL configuration). *URLconf* is a set of patterns that Django will try to match with the received URL to find the correct view.

* check the ```mysite/urls.py``` script for the URL configurations

### Regex
* ^ for beginning of the text
* $ for end of text
* \d for a digit
* + to indicate that the previous item should be repeated at least once
* () to capture part of the pattern



We also want to keep the mysite/urls.py file clean, so we will import urls from our blog application to the main mysite/urls.py file.

Go ahead, add a line that will import blog.urls into the main url (''). Note that we are using the include function here so you will need to add that to the import on the first line of the file.

Your mysite/urls.py file should now look like this:
 ```
from django.conf.urls import include, url
from django.contrib import admin

urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'', include('blog.urls')),
]
 ```
 
 
 Create a new  ```blog/urls.py ``` empty file. All right! Add these two first lines:
 ```
from django.conf.urls import url
from . import views
 ```
Here we're importing Django's function url and all of our views from blog application (we don't have any yet, but we will get to that in a minute!)

After that, we can add our first URL pattern:
 ```
urlpatterns = [
    url(r'^$', views.post_list, name='post_list'),
]
 ```
 
 As you can see, we're now assigning a view called post_list to ^$ URL. This regular expression will match ^ (a beginning) followed by $ (an end) - so only an empty string will match. That's correct, because in Django URL resolvers, 'http://127.0.0.1:8000/' is not a part of the URL. This pattern will tell Django that views.post_list is the right place to go if someone enters your website at the 'http://127.0.0.1:8000/' address.
 
 The last part name='post_list' is the name of the URL that will be used to identify the view. This can be the same as the name of the view but it can also be something completely different. We will be using the named URLs later in the project so it is important to name each URL in the app. We should also try to keep the names of URLs unique and easy to remember
 
 If you try to visit http://127.0.0.1:8000/ now, then you'll find some sort of 'web page not available' message. This is because the server (remember typing runserver?) is no longer running. Take a look at your server console window to find out why.
## Django views
The views will be declared in the file: ```blog/views.py ```
Let's declare our first view:
  ```
 from django.shortcuts import render

# Create your views here.
def post_list(request):
    return render(request, 'blog/post_list.html', {})
```
     
As you can see, we created a function (def) called post_list that takes request and return a function render that will render (put together) our template blog/post_list.html.

## Introduction to HTML
What's a template, you may ask?

A template is a file that we can re-use to present different information in a consistent format - for example, you could use a template to help you write a letter, because although each letter might contain a different message and be addressed to a different person, they will share the same format.

A Django template's format is described in a language called HTML (that's the HTML we mentioned in the first chapter How the Internet works).
### What is HTML?
HTML is a simple code that is interpreted by your web browser - such as Chrome, Firefox or Safari - to display a webpage for the user.

HTML stands for "HyperText Markup Language". HyperText means it's a type of text that supports hyperlinks between pages. Markup means we have taken a document and marked it up with code to tell something (in this case, a browser) how to interpret the page. HTML code is built with tags, each one starting with < and ending with >. These tags represent markup elements.

### Your first template
Creating a template means creating a template file. Everything is a file, right? You have probably noticed this already.

Templates are saved in blog/templates/blog directory. So first create a directory called templates inside your blog directory. Then create another directory called blog inside your templates directory:

```
blog
└───templates
    └───blog
```

Now add some content:
```
<html>
    <head>
        <title>Django Girls blog</title>
    </head>
    <body>
        <div>
            <h1><a href="">Django Girls Blog</a></h1>
        </div>

        <div>
            <p>published: 14.06.2014, 12:14</p>
            <h2><a href="">My first post</a></h2>
            <p>Aenean eu leo quam. Pellentesque ornare sem lacinia quam venenatis vestibulum. Donec id elit non mi porta gravida at eget metus. Fusce dapibus, tellus ac cursus commodo, tortor mauris condimentum nibh, ut fermentum massa justo sit amet risus.</p>
        </div>

        <div>
            <p>published: 14.06.2014, 12:14</p>
            <h2><a href="">My second post</a></h2>
            <p>Aenean eu leo quam. Pellentesque ornare sem lacinia quam venenatis vestibulum. Donec id elit non mi porta gravida at eget metus. Fusce dapibus, tellus ac cursus commodo, tortor mauris condimentum nibh, ut f.</p>
        </div>
    </body>
</html>
```


Here are some explications:
* <h1>A heading</h1> - for your most important heading
* <h2>A sub-heading</h2> for a heading at the next level
* <h3>A sub-sub-heading</h3> ... and so on, up to <h6>
* <p>A paragraph of text</p>
* <em>text</em> emphasizes your text
* <strong>text</strong> strongly emphasizes your text
* <br /> goes to another line (you can't put anything inside br)
* <a href="http://djangogirls.org">link</a> creates a link
* <ul><li>first item</li><li>second item</li></ul> makes a list, just like this one!
* <div></div> defines a section of the page

### Deploy
```
 git status
 git add --all .
 git status
 git commit -m "Changed the HTML for the site."
 git push
 ```
 
 Pull the new code down to pythonanywhere:
  ```
  $ cd ~/my-first-blog
$ git pull
[...]
   ```
## Django ORM and QuerySets
In this chapter you'll learn how Django connects to the database and stores data in it. Let's dive in!

What is a QuerySet?

A QuerySet is, in essence, a list of objects of a given Model. QuerySet allows you to read the data from the database, filter it and order it.

Open the Django commandline:
```
   (myvenv) ~/djangogirls$ python manage.py shell
```

Get All objects:
```
>>> from blog.models import Post
>>> Post.objects.all()
Traceback (most recent call last):
      File "<console>", line 1, in <module>
NameError: name 'Post' is not defined
```

Create Object:
```
>>> from django.contrib.auth.models import User
>>> Post.objects.create(author=me, title='Sample title', text='Test')
>>> User.objects.all()
me = User.objects.get(username='ola')
>>> Post.objects.create(author=me, title='Sample title', text='Test')

```
Filter  Object:
```
>>> Post.objects.filter(author=me)
>>> Post.objects.filter(title__contains='title')
>>> from django.utils import timezone
>>> Post.objects.filter(published_date__lte=timezone.now())
[]
>>> post = Post.objects.get(title="Sample title")
>>> post.publish()
>>> Post.objects.filter(published_date__lte=timezone.now())
[<Post: Sample title>]
```

Ordering  Object:
```
>>> Post.objects.order_by('created_date')
>>> Post.objects.order_by('-created_date')
```



Chaining querySets  :
```
>>> Post.objects.filter(published_date__lte=timezone.now()).order_by('published_date')
>>> exit()
$
```
