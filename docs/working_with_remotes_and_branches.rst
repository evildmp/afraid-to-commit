######################
Branches and remotes
######################

Using branches
==============

We've been using a branch already, the *master* branch (the only branch).

As you may have noticed on GitHub, a repository can have numerous branches
within it. Branches are ways of organising work on a project: you can have
a branch for a new feature, for trying out something new, for exploring an
issue - anything at all.

Just as virtualenvs are disposable, so are **branches** in Git. You *can*
have too many branches, but don't hesitate to create new ones; it costs
almost nothing.

It's a good policy to create a new branch for every new bit of work you
start doing, even if it's a very small one.

**Branch early and branch often**; if you're in any doubt; create a new
branch.

.. note::
   Keeping master 'clean'

		Though you didn't create new branches in the previous section for your
        local changes, you could have, and probably should have done. It would
        have kept the *master* branch as clean of changes, in turn making it
        easier for you to keep it up-to-date with my upstream master in the
        future. From now on, create a new branch for changes.

Create a branch
---------------

You're going to create a new branch for new changes to go into::

    daniele@v029:~/afraid-to-commit$ git checkout -b amend-my-name
    Switched to a new branch 'amend-my-name

`git checkout` is a command you'll use a lot, to switch between branches. The
`-b` flag tells it to **create a new branch** at the same time, based upon
whatever branch you were on.

* now make some changes to your name in `attendees_and_learners.rst`

`git status` is always useful::

    daniele@v029:~/afraid-to-commit$ git status
    # On branch amend-my-name
    # Changes not staged for commit:
    #   (use "git add <file>..." to update what will be committed)
    #   (use "git checkout -- <file>..." to discard changes in working directory)
    #
    #	modified:   attendees_and_learners.rst
    #
    no changes added to commit (use "git add" and/or "git commit -a")

These changes will only be applied to this branch when they're committed. You can `git add` changed files, but until you commit they won't belong to any branch.
    
.. note::
   When to branch
   
    You don't actually *need* to create your new branch until you decide to
    commit. But creating your new branches before you start making changes
    makes it less likely that you will forget later, and commit things to the
    wrong branch.

Add and commit your changes
---------------------------

*   `git add` your changes
*   commit them

::

    daniele@v029:~/temp/afraid-to-commit$ git commit -m "I amended my name"
    [amend-my-name 1fcac0e] I amended my name
     1 files changed, 0 insertions(+), 4 deletions(-)

Push your new branch to GitHub
------------------------------

This time, you need to tell git *where* to push it (i.e. back to the remote
repository you cloned from, on GitHub) and *what* exactly to push (your new
branch).

The repository you cloned from can be referred to as **origin**. The new
branch is called **add-my-github-name**. So::

    daniele@v029:~/afraid-to-commit$ git push origin amend-my-name 
    Counting objects: 34, done.
    Delta compression using up to 2 threads.
    Compressing objects: 100% (21/21), done.
    Writing objects: 100% (28/28), 6.87 KiB, done.
    Total 28 (delta 13), reused 12 (delta 7)
    To git@github.com:evildmp/afraid-to-commit.git
     * [new branch]      amend-my-name -> amend-my-name


Check your GitHub repository
----------------------------

*   go to https://github.com/<your GitHub name>/afraid-to-commit
*	check that your new *amend-my-name* branch is there
*	check that your latest change to `attendees_and_learners.rst` is in it


Send me a pull request
----------------------    

You can make more changes locally, and continue committing them, and pushing
them to GitHub. When you've made all the changes that you'd like me to accept
though, it's time to send *me* a pull request, *from your new branch*.

.. note::
   Keeping master 'clean' (again)
   
    You *could* of course have merged your new branch into your *master*
    branch, and sent me a pull request from that. But, once again, it's a good
    policy to keep your *master* branch, on GitHub too, clean of changes you
    make, and only to pull things into it from upstream.
    
    In fact the same thing goes for other branches on my upstream that you
    want to work with. Keeping them clean isn't strictly necessary, but it's
    nice to know that you'll always be able to pull changes from upstream
    without having to tidy up merge conflicts.

Switching between branches locally
----------------------------------

You can switch between local branches using `git checkout`. To switch back to
the *master* branch::

    git checkout master

If you have a changed tracked file - a tracked file is one that Git is managing - it will warn you that you can't switch branches without either committing, abandoning or 'stashing' the changes.

Commit
^^^^^^

You already know how to commit changes.

Abandon
^^^^^^^

You can abandon changes in a couple of ways. The recommended one is::

    git checkout <file> 

This checks out the previously-committed version of the file.         

The one that is not recommended is::

	git checkout -f <branch> 
	
The `-f` flag forces the branch to be checked out.

.. note::
   Keeping master 'clean'

		Generally speaking, using the `-f` flag for Git operations is to be
        avoided. It offers plenty of scope for mishap. If Git tells you about
        a problem and you force your way past it, you're inviting trouble.  

^^^^^
Stash

If you're really interested, look up `git stash`, but it's beyond the scope of this tutorial. 

Remotes
=======

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
	    add-name      tracked
	    amend-my-name new (next fetch will store in remotes/origin)
	    master        tracked
	  Local branch configured for 'git pull':
	    master merges with remote master
	  Local ref configured for 'git push':
	    master pushes to master (local out of date)  
	
It's very useful for Git to know about other remote repositories too. For
example, at the end of the previous section, we considered a conflict between
your GitHub fork and and the upstream GitHub repository. The only way to fix
that is locally, on the command line, and by being able to refer to both those
remotes.

Now you *can* refer to a remote using its full address:

	https://github.com/evildmp/afraid-to-commit
	
But just as your remote is called **origin**, you can give any remote a more
memorable name. Your own **origin** has an upstream repository (mine); it's a
convention to name that **upstream**.

Add a remote
^^^^^^^^^^^^

::

	git remote add upstream git@github.com:evildmp/afraid-to-commit.git
	
	 
Checkout a remote branch
^^^^^^^^^^^^^^^^^^^^^^^^
        
Update from upstream
--------------------