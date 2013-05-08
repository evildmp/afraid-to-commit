###########################
Testing Django applications
###########################

The Django Project tutorials include a testing tutorial, which is what we'll
follow. It assumes you have built the Polls application over the previous four
parts of the tutorial.

To save you having to create it now, I've made the tutorial project
application on GitHub. If you haven't followed the Django tutorial right the
way through though, you really should.

Get the code set up
===================

Create a virtualenv
-------------------

::

    $ virtualenv testingtutorial
    New python executable in testingtutorial/bin/python
    Installing setuptools............done.
    Installing pip...............done.
    $ cd testingtutorial/
    $ source bin/activate

Install Django using pip
------------------------

::

    (testingtutorial)$ pip install django==1.5.1
    Downloading/unpacking django
    [...]

Clone the repository
--------------------

Visit https://github.com/evildmp/django-tutorials-project. Fork the
repository.

::

    (testingtutorial)$ git clone git@github.com:<your git name>/django-tutorials-project.git
    Cloning into 'django-tutorials-project'...
    [...]

Checkout the code we want
-------------------------

::

    (testingtutorial)$ cd django-tutorials-project/
    (testingtutorial)$ git checkout tutorial-four 
    Branch tutorial-four set up to track remote branch tutorial-four from origin.
    Switched to a new branch 'tutorial-four'

Fire it up
-------------------

::

    python manage.py syncdb # set up the database

You *will* need to be a superuser, so enter a username and password.

::

    python manage.py runserver 0.0.0.0:8000 # start the runserver
