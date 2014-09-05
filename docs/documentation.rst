##############################################
Documentation using Sphinx and ReadTheDocs.org
##############################################

Without documentation, however wonderful your software, other potential
adopters and developers simply won't be very interested in it.

The good news is that there are several tools that will make presenting and
publishing it very easy, leaving you only to write the content and mark it up
appropriately.

For documentation, we'll use **Sphinx** to generate it, and **Read the Docs**
to publish it. GitHub will be a helpful middleman.

If you have a package for which you'd like to create documentation, you might
as well start producing that right away. If not, you can do it do it in a new
dummy project.

Set up your working environment
===============================

The virtualenv
--------------

As usual, create and activate a new virtualenv::

    $ virtualenv documentation-tutorial
    [...]
    $ cd documentation-tutorial/
    $ source bin/activate


The package or project
----------------------

If you have an existing package to write documentation for
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If your package is on GitHub already and you want to start writing documention
for, clone it now using Git. And of course, start a new branch::

    git checkout -b first-docs

You can merge your docs into your master branch when they start to look
respectable.

If you don't have an existing package that needs docs
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

If you don't have a suitable existing package on GitHub, you'll need to create
a repository on GitHub the way you did before. Call it ``my-first-docs``. Then
create a Git repository locally, point it at GitHub, and create a new branch
for your work::

    $ mkdir my-first-docs
    $ cd my-first-docs/
    $ git init
    $ git remote add origin git@github.com:<your git username>/my-first-docs.git
    $ git checkout -b first-docs

Create a ``docs`` directory
^^^^^^^^^^^^^^^^^^^^^^^^^^^

And either way, create a ``docs`` directory for your docs to live in::

    $ mkdir docs

Sphinx
======

Install Sphinx
--------------

::

    pip install sphinx

It might take a minute or so, it has quite a few things to download and install.

sphinx-quickstart
-----------------

``sphinx-quickstart`` will set up the source directory for your documentation.
It'll ask you a number of questions. Mostly you can just accept the defaults
it offers, and some are just obvious, but there are some you will want to set
yourself as noted below::

    sphinx-quickstart

Root path for the documentation
    ``docs``

Project name
    ``<your name>'s first docs``, or the name of your application

Source file suffix
    ``.rst`` is the default. (Django's own documentation uses ``.txt``. It
    doesn't matter too much.)

You'll find a number of files in your ``docs`` directory now, including
``index.rst``. Open that up.


Using Sphinx & reStructuredText
===============================

reStructuredText elements
-------------------------

Sphinx uses reStructuredText. Start with
http://sphinx-doc.org/rest.html#rst-primer, which will tell you most of what
you need to know to get started. Keep it simple to start with - start with:

*   paragraphs
*   lists
*   headings ('sections', as Sphinx calls them)
*   quoted blocks
*   code blocks
*   emphasis, strong emphasis and literals

Edit a page
-----------

Create an **Introduction** section in the ``index.rst`` page, with a little text
in it; save it.

Create a new page
-----------------

You have no other pages yet. In the same directory as ``index.rst``, create
one called ``all-about-me.rst`` or something appropriate. Perhaps it might
look like::


        ############
        All about me
        ############

        I'm Daniele Procida, a Django user and developer.

        I've contributed to:

        *   django CMS
        *   Arkestra
        *   Django

Sphinx needs to know about it, so in ``index.rst``, edit the ``.. toctree::``
section to add the ``all-about-me`` page::

    .. toctree::
       :maxdepth: 2

       all-about-me

Save both pages.

Render your documentation
-------------------------

In the ``docs`` directory::

    make html

This tells Sphinx to render your source pages. *Pay attention to its warnings*
- they're helpful!

.. note::
    Sphinx can be fussy, and sometimes about things you weren't expecting. For
    example, you well encounter something like::

        WARNING: toctree contains reference to nonexisting document u'all-about-me'
        ...
        checking consistency...
        <your repository>/my-first-docs/docs/all-about-me.rst::
        WARNING: document isn't included in any toctree

    Quite likely, what has happened here is that you indented ``all-about-me``
    in your ``.. toctree::`` with *four* spaces, when Sphinx is expecting
    *three*.

If you accepted the ``sphinx-quickstart`` defaults, you'll find the rendered
pages in ``docs/_build/html``. Open the ``index.html`` it has created in your
browser. You should find in it a link to your new ``all-about-me`` page too.

Publishing your documentation
=============================

Exclude unwanted rendered directories
-------------------------------------

Remember ``.gitignore``? It's really useful here, because you don't want to
commit your *rendered* files, just the source files.

In my ``.gitignore``, I make sure that directories I don't want committed are
listed. Check that::

    _build
    _static
    _templates

are listed in ``.gitignore``.

Add, commit and push
--------------------

``git add`` the files you want to commit; commit them, and push to GitHub.

If this is your first ever push to GitHub for this project, use::

    git push origin master

otherwise::

    git push origin first-docs # or whatever you called this branch

Now have a look at the ``.rst`` documentation files on GitHub. GitHub does a
good enough job of rendering the files for you to read them at a glance,
though it doesn't always get it right (and sometimes seems to truncate them).

readthedocs.org
---------------

However, we want to get them onto Read the Docs. So go to
https://readthedocs.org, and sign up for an account if you don't have one.

You need to **Import** a project: https://readthedocs.org/dashboard/import/.

Give it the details of your GitHub project in the **repo** field -
``git@github.com:<your git username>/my-first-docs.git``, or whatever it is -
and hit **Create**.

And now Read the Docs will actually watch your GitHub project, and build,
render and host your documents for you automatically.

It will update every night, but you can do better still: on GitHub:

#.  select **settings** for your project
#.  choose **Service Hooks**
#.  enable ``ReadTheDocs``

... and now, every time you push documents to GitHub, Read the Docs will be
informed that you have new documents to be published. It's not magic, but it's
pretty close.
