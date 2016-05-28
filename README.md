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


## Introduction to the python
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





