###################
Resolving conflicts
###################

With GitHub's help
------------------

Sometimes you'll discover that your GitHub fork and the upstream repository
have changes that GitHub can't merge. 

There's an *unmergeable-branch* at
https://github.com/evildmp/afraid-to-commit. Try creating a pull request from
that to your *amend-my-name* on GitHub. GitHub should tell you:

    We can’t automatically merge this pull request.
    
    Use the command line to resolve conflicts before continuing.

GitGub will in fact tell you the steps you need to take to solve this, but to
understand what's actually happening, and to do it yourself when you need to,
we need to cover some important concepts.

Using a remote branch to resolve a conflict        
-------------------------------------------
                                 
    $ git fetch upstream
    $ git merge upstream/unmergeable-branch
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
       
The first section is what you have in your version. The second section is what
Git found in the version you were trying to pull in.

You'll have to decide what the file should contain, and you'll need to edit
it. If you decide you want the changes from both versions::

    Daniele Procida <daniele@vurt.org> https://github.com/evildmp
    John Smith <john@example.com>

    $ git add attendees_and_learners.rst
    $ git commit -m "fixed conflict"
    $ git add attendees_and_learners.rst
    [amend-my-name 91a45ac] fixed conflict
    $ git push 

Creating a branch for merging work
----------------------------------

Sometimes it's sensible *not* to do merging work in a branch you rely on.
Remember, branches are cheap and disposable.

So, create a new branch specially for the purpose of merging::

	git checkout -b resolve-conflict upstream/unmergeable-branch

As before, this means: create and switch to a new branch called
*resolve-conflict*, based on branch *unmergeable-branch* of the remote
**upstream**.

This branch now contains my *unmergeable-branch*.

We can't use *amend-my-name* to demonstrate merge conflicts, because we merged
it earlier, so create a new branch based on master for the purpose::

	git checkout -b demo-branch master

Tell Git to merge *resolve-conflict* with *demo-branch*::

    $ git merge demo-branch

Resolve the conflicts as before. Now your *resolve-conflict* branch has merged
the latest changes in your *demo-branch*, *and* my *unmergeable-branch*.

At this point, you should make quite sure that everything is correct (that
tests run and so on), *before* merging into *amend-my-name*.

The last step is to merge *resolve-conflict* into *demo-branch*, thus
bringing with it the changes from *unmergeable-branch*::

    git checkout checkout demo-branch
    git merge resolve-conflict
    git push
