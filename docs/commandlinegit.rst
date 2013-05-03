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

Sometimes you'll discover that your GitHub fork and the upstream repository
have changes that GitHub can't merge. You could make a pull request, as you
did in the previous module, from the upstream version to yours, only for
GitHub to tell you:

    We can’t automatically merge this pull request.
    
    Use the command line to resolve conflicts before continuing.

GitGub will in fact tell you the steps you need to take to solve this, and you
can go ahead and do that now if you need to, but to understand what's actually
happening, and to do it yourself when you need to, we need to cover some
important concepts.
