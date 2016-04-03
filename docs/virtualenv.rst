##################
Virtualenv and pip
##################

In this section you will:

*	use pip to install packages
*	install virtualenv
*	create and destroy, activate and deactivate virtual environments
*	use ``pip freeze`` to show installed items

What is virtualenv?
===================

**Virtualenv** lets you create and manage virtual Python environments.

If you're running a Python project for deployment or development, the chances
are that you'll need more than one version of it, or the numerous other Python
applications it depends upon, at any one time.

For example, when a new version of Django is released, you might want to check
to see if your project is still compatible. You don't want to have to set up a whole new
server with a different version of Django to find out.

With virtualenv, you can quickly set up a brand new Python environment, and
install your components into it - along with the new version of Django,
without touching or affecting what you already have running.

You can have literally dozens of virtualenvs on the same machine, all running
different versions of your Python software, all independently of each other,
and can safely make changes to one without affecting anything else.

**pip** goes hand-in-hand with virtualenv; in fact, it comes with virtualenv
(as well as separately). It's an installer, and is the easiest way to install
things into a virtualenv.

Installing pip
==============

You will most probably find that pip is already installed on your system.

Run::

    pip --version

to find out.

If it's not, you have various options.

On Debian/Ubuntu systems
------------------------

::

    sudo apt-get install python-pip

On Debian you probably will not be authorised to use ``sudo``.  In this case use::

    su -

to switch to the root user before installing pip.


Use get-pip.py
--------------

Another option is to use the official `get-pip.py <https://pip.pypa.io/en/stable/installing/#installing-with-get-pip-py>`_ script.



Install virtualenv
==================

Try::

    virtualenv --version

Keep it up-to-date::

    sudo pip install --upgrade virtualenv
    hash -r # purge shell's PATH, though this may not be necessary for you

If you got a "Command not found" when you tried to use virtualenv, try::

    sudo pip install virtualenv

or::

    sudo apt-get install python-virtualenv # for a Debian-based system

If that fails or you're using a different system, you might need more help:

    `Virtualenv installation documentation
    <http://www.virtualenv.org/en/latest/#installation>`_


Create and activate a virtual environment
=========================================

::

    virtualenv my-first-virtualenv
    cd my-first-virtualenv
    source bin/activate

.. note:: **Windows users** should run ``Scripts\activate`` instead of ``source bin/activate``.

Notice how your command prompt tells you that the virtualenv is active (and it remains active even
while you're not in its directory)::

    (my-first-virtualenv)~/my-first-virtualenv$


Using pip
=========

pip freeze
----------

``pip freeze`` lists installed Python packages::

    (my-first-virtualenv)daniele@v029:~/my-first-virtualenv$ pip freeze
    argparse==1.2.1
    distribute==0.6.24
    pyasn1==0.1.7
    virtualenv==1.9.1
    wsgiref==0.1.2

pip install
-----------

Earlier, you may have used ``sudo pip install``. You **don't** need ``sudo``
now, because you're in a virtualenv. Let's install something.

::

    pip install rsa

pip will visit PyPI, the Python Package Index, and will install Python-RSA (a
"Pure-Python RSA implementation"). It will also install its dependencies -
things it needs - if any have been listed at PyPI.

Now see what ``pip freeze`` reports. You will probably find that as well as
Python-RSA it installed some other packages - they were ones that Python-RSA
needed.

And try::

    (my-first-virtualenv)~/my-first-virtualenv$ python
    Python 2.7.2+ (default, Jul 20 2012, 22:15:08)
    [GCC 4.6.1] on linux2
    Type "help", "copyright", "credits" or "license" for more information.
    >>> import rsa

To uninstall it::

    pip uninstall rsa

To install a particular version::

    pip install rsa==3.0

To ugrade the package to the latest version::

    pip install --upgrade rsa

Where packages get installed
----------------------------

Your virtualenv has a site-packages directory, in the same way your system does. So now rsa can be found in::

    ~/my-first-virtualenv/lib/python2.7/site-packages/rsa

(It's possible that you'll have a different version of Python listed in that
path.)

Dependencies
------------

Python-RSA doesn't have any dependencies, but if it did, and if those
dependencies had dependencies, pip would install them all.

So if all the package authors have done a good job of informing PyPI about
their software's requirements, you can install a Django application, for
example, and pip will will install it, and Django, and possibly dozens of other
pieces of software, all into your virtualenv, and without your having to make
sure that everything required is in place.

Managing virtualenvs
====================

Create a second virtualenv
--------------------------

::

    cd ~/ # let's not create it inside the other...
    virtualenv my-second-virtualenv

When you activate your new virtualenv, it will deactivate the first::

    cd my-second-virtualenv
    source bin/activate

.. note:: **Windows users**: don't forget to use ``Scripts\activate`` rather than ``source bin/activate``.

``pip freeze`` will show you that you don't have Python-RSA installed in this
one - it's a completely different Python environment from the other, and both
are isolated from the system-wide Python setup.

Deactivate a virtualenv manually
--------------------------------

Activating a virtualenv automatically deactivates one that was previously
active, but you can also do this manually::

    deactivate

Now you're no longer in any virtualenv.

--system-site-packages
-----------------------

When you create a virtualenv, it doesn't include any Python packages already
installed on your system. But sometimes you do want to install all packages. In that
case you'd do::

    virtualenv --system-site-packages my-third-virtualenv

remove a virtualenv
-------------------

virtualenvs are disposable. You can get rid of these::

    cd ~/
    rm -r  my-first-virtualenv my-second-virtualenv my-third-virtualenv

And that's pretty much all you need to get started and to use pip and
virtualenv effectively.
