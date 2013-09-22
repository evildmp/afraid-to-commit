###################
Resolving conflicts
###################

In this section you will:

*	encounter a merge conflict on GitHub
*	encounter a merge conflict on the commandline
*	resolve the confluct in a new temporary Git branch


Encountering a merge conflict on GitHub
=======================================

Sometimes you'll discover that your GitHub fork and the upstream repository
have changes that GitHub can't merge. 

There's an *unmergeable-branch* at https://github.com/evildmp/afraid-to-commit.
It's unmergeable because it deliberately contains changes that conflict with
other changes made in *master*. 

Try creating a pull request from *unmergeable-branch* to your *amend-my-name*
on GitHub. If you do, GitHub will tell you:

    We can’t automatically merge this pull request.
    
    Use the command line to resolve conflicts before continuing.

GitGub will in fact tell you the steps you need to take to solve this, but to
understand what's actually happening, and to do it yourself when you need to,
we need to cover some important concepts.

Merging changes from a remote branch        
====================================

::

    $ git checkout amend-my-name # make sure you're on the right branch
	$ git fetch upstream
    $ git merge upstream/unmergeable-branch
    Auto-merging attendees_and_learners.rst
    CONFLICT (content): Merge conflict in attendees_and_learners.rst
    Automatic merge failed; fix conflicts and then commit the result.

When there's a conflict, Git marks them for you in the files. You'll see
sections like this::

    <<<<<<< HEAD
    * Daniel Pass <daniel.antony.pass@googlemail.com>
    * Kieran Moore
    =======
    * Kermit the Frog
    * Miss Piggy
    >>>>>>> upstream/unmergeable-branch
       
The first section is what you have in your version. The second section is what
Git found in the version you were trying to pull in.

You'll have to decide what the file should contain, and you'll need to edit
it. If you decide you want the changes from both versions::

    * Daniel Pass <daniel.antony.pass@googlemail.com>
    * Kieran Moore
    * Kermit the Frog
    * Miss Piggy

    $ git add attendees_and_learners.rst
    $ git commit -m "fixed conflict"
    [amend-my-name 91a45ac] fixed conflict
    $ git push origin amend-my-name

Creating a branch for merging work
==================================

Sometimes it's sensible *not* to do merging work in a branch you rely on. In
the example above, your *amend-my-name* branch doesn't contain a great deal of
work. If you had a branch that contained many complex changes however, you
certainly wouldn't want to discover dozens of conflicts making a mess in the
files containing all your hard work.

So remember, **branches are cheap and disposable**. Rather than risk messing
up the branch you've been working on, create a new one specially for the
purpose of discovering what sort of conflicts arise, and to give you a place
to work on resolving them without disturbing your work so far::

	git checkout -b resolve-conflict amend-my-name

As before, this means: create and switch to a new branch called
*resolve-conflict*, based on branch *amend-my-name*.

We'll use this new branch as a safe place to do the potentially messy work of
resolving the conflicts in. 

You have already resolved the conflict with *unmergeable-branch*, so I have
provided *unmergeable-branch-2* for you. The conflict I here is extremely
simple, but you could have conflicts across dozens of files, if you were
unlucky. Even if it all goes horribly wrong in here, that won't affect either
of the two branches you were trying to reconcile - they'll remain safely
untouched.

Tell Git to attempt to merge the conflicting branch into this one::

    $ git merge upstream/another-unmergeable-branch

Resolve the conflicts as before (edit the file, ``add`` it, ``commit`` the
changes). Now your *resolve-conflict* branch has reconciled the latest changes
in your *amend-my-name*, *and* my *unmergeable-branch-2*.

At this point, you would make quite sure that everything is correct (that
tests run and so on), *before* merging back into *amend-my-name*.

Then the last step is to merge *resolve-conflict* into *amend-my-name*, thus
bringing with it the changes from *unmergeable-branch-2*::

    git checkout amend-my-name
    git merge resolve-conflict
    git push origin amend-my-name
