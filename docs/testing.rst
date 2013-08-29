###########################
Testing Django applications
###########################

The Django Project tutorials include a testing tutorial, which is what we'll
follow. It assumes you have built the Polls application over the previous four
parts of the tutorial.

To save you having to create it now, I've made the tutorial project
application on GitHub. If you haven't followed the Django tutorial right the
way through though, you really should.

This section of the workshop will follow roughly the tutorial at
https://docs.djangoproject.com/en/1.5/intro/tutorial05/. 

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
----------

::

    python manage.py syncdb # set up the database
    
.. note::
   ImportError: No module named django.core.management

   Maybe you don't have Django installed. That's no problem; you already know
   the answer to this::

       pip install django # install Django into your virtualenv

You *will* need to be a superuser, so enter a username and password.

::

    python manage.py runserver 0.0.0.0:8000 # start the runserver

Developing tests
================

The first bug
-------------

Visit the site's admin, and create a new poll. You'll soon see that you can
expose a little bug. In the list of polls in the admin, you'll see that polls
published in the last day are considered to have been ``published recently``,
but so are polls whose ``pub_date`` is in the future.

We can fix that bug easily enough, but in order to be sure that it *stays*
fixed, a test will help. So, we should:

#.  create a test that exposes the bug
#.  work on the bug
#.  run the test, and go back to step 2 until the test passes

https://docs.djangoproject.com/en/1.5/intro/tutorial05/#we-identify-a-bug

Following good Git working practices, *before you change a single byte of code*,
create a new branch to work in::

    git checkout -b test-for-published-recently
    
When you've worked through that section in the tutorial, you'll have fixed the
bug and created three tests. This would be a good moment to add your changed
files, commit your changes, and push them to your GitHub repository before
continuing.

Your next bugfix and tests
--------------------------

What about your next bugfix and tests? Should they be in a branch based on
*tutorial-four*, or based on *test-for-published-recently*?

That really depends on whether your next bugfix and tests can be regarded as
independent of the ones in *test-for-published-recently*, in which case it
might be better to start again based on *tutorial-four*::

    git checkout -b improve-list-view tutorial-four
    
This will mean that you can make a pull request for those changes
independently of the previous ones, meaning your pull request will be smaller,
simpler and easier to understand - maintainers love that.
    
On the other hand, if you're going to build on the work you've just done,
you'll need::

    git checkout -b improve-list-view 
    
Keep creating new branches as appropriate, as you work through the tutorial.

     
Following the tutorial
======================

The Django testing tutorial covers a number of key ideas and approaches. It's
worth following the whole thing, and making sure you understand the points
its making.

Unfortunately as of Django 1.5.1 the tutorial actually includes a bugfix that
doesn't actually work, and a test that lets it slip through! Details are at
https://code.djangoproject.com/ticket/20249 - if nothing else, this
demonstrates some of the pitfalls that can catch you out when testing.

When you tackle
https://docs.djangoproject.com/en/1.5/intro/tutorial05/#improving-our-view,
you'll therefore need to find a different approach.
