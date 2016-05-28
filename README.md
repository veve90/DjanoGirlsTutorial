# DjanoGirlsTutorial
I will participate to the Djsngo girls Lyon as a mentor. Therefore I will complete the Django girls tutorial before this event (:D).
This are my notes for the Djano girls Tutorial: http://tutorial.djangogirls.org/en/

## What will you learn during the tutorial?
Once you've finished the tutorial, you will have a simple, working web application: your own blog. We will show you how to put it online, so others will see your work!

## Installation
* Install Python: https://www.python.org/ftp/python/3.4.3/python-3.4.3.amd64.msi
* Set up virtualenv and install Django: 
    * create a folder: D:\Users\agherman\Documents\djangogirls
    * go to this folder in cmd and do C:\Python34\python -m venv myvenv
    * start the virtual env: C:\Users\Name\djangogirls> myvenv\Scripts\activate
* Install Django: pip install django~=1.9.0
* Install gedit: http://ftp.gnome.org/pub/GNOME/binaries/win64/gedit/gedit-x86_64-3.20.1.msi
* Create a python anywhere account: https://www.pythonanywhere.com


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
