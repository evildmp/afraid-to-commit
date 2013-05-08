####################
Working with remotes
####################


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
------------

::

	git remote add upstream git@github.com:evildmp/afraid-to-commit.git
	
Fetch remote data
-----------------

The remote's there, but you don't yet have any information about it. You need
to **fetch** that::

    git fetch upstream
    
This means: get the latest information about the branches on **upstream**. 

List remote branches
--------------------

`git branch` shows your local branches, to see a list of them all, including
the remote branches::

    git branch -a   

Checkout a remote branch
------------------------

You'll have seen from `git branch -a` that there's a branch called
*additional-branch* on the **upstream* repository.       

You can check this out::

	git checkout -b additional-branch upstream/additional-branch

This means: create and switch to a new branch called *additional-branch*,
based on branch *additional-branch* of the remote **upstream**. 

.. note::
   Branches and references
   
    Whenever you see something in Git of the form `remote-name/branch-name`,
    remember that that is a **reference** to a branch, not a branch itself.
    You can't checkout a reference.
