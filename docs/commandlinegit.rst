######################
Git on the commandline
######################

So far we've done all our Git work using the GitHub website, but that's often not the most appropriate way to work. 

You'll find that most of your Git-related operations can and need to be done on the commandline.

Install Git
===========

::

    apt-get install git

There are other ways of installing Git; you can even get a graphical Git application, that will include the commandline tools. These are described at:

    http://git-scm.com/book/en/Getting-Started-Installing-Git

Some basic Git operations
=========================

Clone a repository
------------------

Getting a copy of a repository on your local machine is called **cloning**.

*   got to https://github.com/evildmp/afraid-to-commit
*   copy `git@github.com:evildmp/afraid-to-commit.git`
*   on your machine::

    daniele@v029:~$ git clone git@github.com:evildmp/afraid-to-commit.git
    Cloning into afraid-to-commit...
    remote: Counting objects: 47, done.
    remote: Compressing objects: 100% (35/35), done.
    remote: Total 47 (delta 17), reused 27 (delta 6)
    Receiving objects: 100% (47/47), 14.72 KiB, done.
    Resolving deltas: 100% (17/17), done.

If you have a look in the newly-created directory, you'll find all the source
code of the *Don't be afraid to commit* project.

Edit a file
-----------

*   find the `attendees_and_learners.rst` file again
*   after your name and email address, add your Github account
*   save the file

Examine the status
------------------

We want to know the status of our **working directory**. The working directory is files that you currently have in front of you, available to edit.

::

    daniele@v029:~/afraid-to-commit$ git status
    # On branch master
    # Changes not staged for commit:
    #   (use "git add <file>..." to update what will be committed)
    #   (use "git checkout -- <file>..." to discard changes in working directory)
    #
    #	modified:   attendees_and_learners.rst
    #
    no changes added to commit (use "git add" and/or "git commit -a")

What this is telling us:

*   we're on the *master* branch
*   that we have one modified file
*   that there's nothing to commit

Create a branch
---------------

.. note::
   Branch early and branch often

    As you may have noticed on GitHub, a respoitory can have numerous branches
    within it. Branches are ways of organising work on a project: you can have
    a branch for a new feature, for trying out something new, for exploring an
    issue - anything at all.
    
    Just as Virtualenvs are disposable, so are **branches** in Git. You *can*
    have too many branches, but don't hesitate to create new ones; it costs
    almost nothing.
    
    It's a good policy to create a new branch for every new bit of work you
    start doing, even if it's a very small one.
    
Until they are committed, any changes in your working directory remain unrecorded by Git. If you're on a branch, that's where they'll be committed. 

It would be nice to keep the *master* branch as clean as possible (this will make it easier for you to keep it up-to-date with my upstream master in the future). So, rather than commit it to *master*, we will create a new branch for your changes to go into::

    daniele@v029:~/afraid-to-commit$ git checkout -b add-my-github-name
    M	attendees_and_learners.rst
    Switched to a new branch 'add-my-github-name'
    
`git checkout` is a command you'll use a lot, to switch between branches. The `-b` flag tells it to **create a new branch** at the same time.

.. note::
   When to branch
   
    You don't actually *need* to create your new branch until you decide to
    commit. But creating your new branches before you start making changes
    makes it less likely that you will forget later, and commit things to the
    wrong branch.

Stage your changes
------------------

.. note::
   Staging files

    Git has a **staging area**, for files that you want to commit. On GitHub
    when you have edited a file, you commit it as soon as you save it. On your
    machine, you can edit a number of files and commit them altogether.
    **Staging a file** in Git's terminology means adding it to the staging
    area, in preparation for a commit.
    
To add your amended file to the staging area::

    git add attendees_and_learners.rst
    
and check the result::

    daniele@v029:~/afraid-to-commit$ git status
    # On branch add-my-github-name
    # Changes to be committed:
    #   (use "git reset HEAD <file>..." to unstage)
    #
    #	modified:   attendees_and_learners.rst
    #

If there are other files you want to change, you can add them when you're
ready; until you commit, they'll all be together in the staging area.

.. note::
   What gets staged?
   
    It's not your files, but the **changes to your files**, that are staged.
    Make a further change to `attendees_and_learners.rst`, and run `git
    status`::
    
        daniele@v029:~/afraid-to-commit$ git status
        # On branch master
        # Changes to be committed:
        #   (use "git reset HEAD <file>..." to unstage)
        #
        #	modified:   attendees_and_learners.rst
        #
        # Changes not staged for commit:
        #   (use "git add <file>..." to update what will be committed)
        #   (use "git checkout -- <file>..." to discard changes in working directory)
        #
        #	modified:   attendees_and_learners.rst
        #

    Your more recent changes are in the file, but are not going to be
    committed. You'll need to `git add` the file again for that.
    
Commit your changes
-------------------

When you're happy with your files, and have added the changes you want to
commit to the staging area::

    daniele@v029:~/afraid-to-commit$ git commit -m "added my github name" 
    [master 4373299] added my github name
     1 files changed, 1 insertions(+), 0 deletions(-)

Push your changes to GitHub
---------------------------

When you made a change on GitHub, it not only saved the change and committed the file at the same time, it also showed up right away in your GitHub repository. To get your change to GitHub, you'll have to push it there::

