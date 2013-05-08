###################
Resolving conflicts
###################


Using a remote branch to resolve a conflict        
-------------------------------------------
                                 
We're going to use a remote branch now to resolve a conflict that GitHub
can't. Let's say that you manage to push something to your *master* banch on
GitHub,and when you create a pull request to your *master* from mine, GitHub
tells you that it can't do an automatic merge. 

So::

    git fetch upstream
    
This means: get the latest information about the branches on **upstream**.

	git checkout -b resolve-conflict upstream/master

This means: create and switch to a new branch called *resolve-conflict*,
based on branch *master* of the remote **upstream**. 

This branch now contains my *master*.

Tell Git to merge it with *your* local master::

    daniele@v029:~/afraid-to-commit$ git merge master
    Auto-merging attendees_and_learners.rst
    CONFLICT (content): Merge conflict in attendees_and_learners.rst
    Automatic merge failed; fix conflicts and then commit the result.
    
Fix conflicts in the files Git has warned you about, and::

    daniele@v029:~/afraid-to-commit$ git add attendees_and_learners.rst
    daniele@v029:~/afraid-to-commit$ git commit -m "resolved conflicts"
    [resolve-conflict 3c8e780] resolved conflicts
    
Now your *resolve-conflict* branch has merged the latest changes in your own master, *and* my master. 

You want to push this to your *master* branch at GitHub. There are various ways to do it, but one way is:

*   get your local *master* up-to-date
*   push it

::
    
    daniele@v029:~/temp/afraid-to-commit$ git checkout master 
    Switched to branch 'master'
    daniele@v029:~/temp/afraid-to-commit$ git merge resolve-conflict 
    Updating fed5a0d..3c8e780
    Fast-forward
     attendees_and_learners.rst |    3 +--
     1 files changed, 1 insertions(+), 2 deletions(-)
    daniele@v029:~/temp/afraid-to-commit$ git status
    # On branch master
    # Your branch is ahead of 'origin/master' by 2 commits.
    #
    nothing to commit (working directory clean)
    daniele@v029:~/temp/afraid-to-commit$ git push
    Counting objects: 10, done.
    Delta compression using up to 2 threads.
    Compressing objects: 100% (6/6), done.
    Writing objects: 100% (6/6), 754 bytes, done.
    Total 6 (delta 2), reused 0 (delta 0)
    To git@github.com:evildmp/afraid-to-commit.git
       fed5a0d..3c8e780  master -> master

.. note::
   Keeping master 'clean' (again)
   
    This was necessary because your *master* on GitHub was allowed to diverge
    from the **upstream** *master*. It would have been better to avoid that.
    
    All the same, when you are working with branches, from time to time you
    will need to resolve a conflict, and the basic steps here are what you
    need to do that.
    
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
