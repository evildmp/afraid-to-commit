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

When we worked on GitHub, the basic work cycle was *fork*, *edit*, *commit*,
*pull request*, *merge*. The same cycle, with a few differences, is what we
will work through on the commandline.

Clone a repository
------------------

When you made a copy of the *Don't be afraid to commit* repository on GitHub,
that was a *fork*. Getting a copy of a repository onto your local machine is
called **cloning**.

#. go to https://github.com/evildmp/afraid-to-commit
#. copy `git@github.com:evildmp/afraid-to-commit.git`
#. on your machine::

    daniele@v029:~$ git clone git@github.com:evildmp/afraid-to-commit.git
    Cloning into afraid-to-commit...
    remote: Counting objects: 47, done.
    remote: Compressing objects: 100% (35/35), done.
    remote: Total 47 (delta 17), reused 27 (delta 6)
    Receiving objects: 100% (47/47), 14.72 KiB, done.
    Resolving deltas: 100% (17/17), done.

If you have a look in the newly-created directory, you'll find all the source
code of the *Don't be afraid to commit* project. 

And::

    daniele@v029:~/afraid-to-commit$ git status
    # On branch master
    nothing to commit (working directory clean)

Edit a file
-----------

#. find the `attendees_and_learners.rst` file again
#. after your name and email address, add your Github account
#. save the file

Check the status again
----------------------

We want to know the status of our **working directory**. The working directory
is the set of files that you currently have in front of you, available to
edit.

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

Stage your changes
------------------

Git has a **staging area**, for files that you want to commit. On GitHub
when you have edited a file, you commit it as soon as you save it. On your
machine, you can edit a number of files and commit them altogether.
**Staging a file** in Git's terminology means adding it to the staging
area, in preparation for a commit.
    
To add your amended file to the staging area::

    git add attendees_and_learners.rst
    
and check the result::

    daniele@v029:~/afraid-to-commit$ git status
    # On branch master
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
    Make some further change to `attendees_and_learners.rst`, and run `git
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
     
The `-m` flag is for the message ("added my github name") on the commit -
every commit needs a commit message.

Push your changes to GitHub
---------------------------

When you made a change on GitHub, it not only saved the change and committed
the file at the same time, it also showed up right away in your GitHub
repository. 

To get your change to GitHub, you'll have to push it there, using
**git push**::

    daniele@v029:~/afraid-to-commit$ git push
    Counting objects: 5, done.
    Delta compression using up to 2 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (3/3), 373 bytes, done.
    Total 3 (delta 1), reused 0 (delta 0)
    To git@github.com:evildmp/afraid-to-commit.git
       b74db32..6c6d767  master -> master

And if I like them, I'll merge them.

Incorporate upstream changes (again)
------------------------------------

Once again, I may have merged other people's pull requests too. Assuming that
you want to keep up-to-date with my changes, you're going to want to merge
those into your GitHub fork as well as your local clone.

So:

* on GitHub, pull the upstream changes into your fork the way you did previously

Then::

    daniele@v029:~/afraid-to-commit$ git pull
    remote: Counting objects: 5, done.
    remote: Compressing objects: 100% (3/3), done.
    remote: Total 3 (delta 1), reused 0 (delta 0)
    Unpacking objects: 100% (3/3), done.
    From github.com:evildmp/afraid-to-commit
       6c6d767..81374ba  master     -> origin/master
    Updating 6c6d767..81374ba
    Fast-forward
     attendees_and_learners.rst |    2 +-
     1 files changed, 1 insertions(+), 1 deletions(-)

So now we have replicated the full cycle of work we described in the previous
module.

Resolving conflicts
===================

The `pull` operation above does two things: it **fetches** updates from your
GitHub fork (**origin**), and **merges** them in a **fast-forward** operation.

This is only possible when the updates can be merged automatically. Sometimes
there will be conflicts between the changesets, and you'll have to manage the
merge manually.

A conflict between your local clone and your fork on GitHub
-----------------------------------------------------------

::

    daniele@v029:~/temp/afraid-to-commit$ git pull
    remote: Counting objects: 5, done.
    remote: Compressing objects: 100% (3/3), done.
    remote: Total 3 (delta 1), reused 0 (delta 0)
    Unpacking objects: 100% (3/3), done.
    From github.com:evildmp/afraid-to-commit
       81374ba..960517d  master     -> origin/master
    Auto-merging attendees_and_learners.rst
    CONFLICT (content): Merge conflict in attendees_and_learners.rst
    Automatic merge failed; fix conflicts and then commit the result.

When there's a conflict, Git marks them for you in the files. You'll see
sections like this::

    <<<<<<< HEAD
    Daniele Procida <daniele@vurt.org> https://github.com/evildmp
    =======
    John Smith <john@example.com>
    >>>>>>> 960517d68fa4ac4778ac2a47c6721fecd3505309
       
The first section is what you have in your version. The second section is what Git found in the version you were trying to pull in.

In this case, we want both lines, so edit the file::

    Daniele Procida <daniele@vurt.org> https://github.com/evildmp
    John Smith <john@example.com>

then::

#. add the amended file
#. commit your changes
#. push them back to GitHub

A conflict between your fork and and the upstream repository
------------------------------------------------------------





*********************

Using branches
==============

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

    

Push your changes to GitHub
---------------------------

When you made a change on GitHub, it not only saved the change and committed
the file at the same time, it also showed up right away in your GitHub
repository. 

To get your change to GitHub, you'll have to push it there, using
**git push**.

You need to tell git *where* to push it (i.e. back to the remote repository
you cloned from, on GitHub) and *what* exactly to push (your) new branch.

The repository you cloned from can be referred to as **origin**. The new
branch is called **add-my-github-name**. So::

    daniele@v029:~/afraid-to-commit$ git push origin add-my-github-name 
    Counting objects: 54, done.
    Delta compression using up to 2 threads.
    Compressing objects: 100% (31/31), done.
    Writing objects: 100% (54/54), 15.42 KiB, done.
    Total 54 (delta 20), reused 45 (delta 17)
    To git@github.com:evildmp/afraid-to-commit.git
     * [new branch]      add-my-github-name -> add-my-github-name

Check your GitHub repository
----------------------------

*   got to https://github.com/evildmp/afraid-to-commit
*	check that your latest change to `attendees_and_learners.rst` is there

Send a pull request
-------------------    

You can make more changes locally, and continue committing them, and pushing
them to GitHub. When you've made all the changes that you'd like me to accept
though, it's time to send me a pull request, just like the one you did before.

Switching between branches locally
----------------------------------

Remotes
-------
Your repository on GitHub is the **remote** for the clone on your local
machine. By default, your clone refers to that remote as **origin**. At
the moment, it's the only remote you have::

    daniele@v029:~/afraid-to-commit$ git remote
    origin
    
    daniele@v029:~/afraid-to-commit$ git remote show origin
    * remote origin
      Fetch URL: git@github.com:evildmp/afraid-to-commit.git
      Push  URL: git@github.com:evildmp/afraid-to-commit.git
      HEAD branch: master
      Remote branches:
        master   tracked
      Local branch configured for 'git pull':
        master merges with remote master
      Local refs configured for 'git push':
        master   pushes to master   (up to date) 

Add a remote
^^^^^^^^^^^^

Checkout a remote branch
^^^^^^^^^^^^^^^^^^^^^^^^
        
Update from upstream
--------------------