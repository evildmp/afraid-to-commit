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
                                 
We want to merge the *unmergeable-branch* into one of your branches,
*amend-my-name*.

	git checkout -b resolve-conflict upstream/unmergeable-branch

As before, this means: create and switch to a new branch called
*resolve-conflict*, based on branch *unmergeable-branch* of the remote
**upstream**.

This branch now contains my *unmergeable-branch*.

Tell Git to merge it with *your* local *amend-my-name* branch::

    $ git merge amend-my-name
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
    $ git commit -m "resolved conflicts"
    [resolve-conflict 3c8e780] resolved conflicts
    
Now your *resolve-conflict* branch has merged the latest changes in your
*amend-my-name*, *and* my *unmergeable-branch*.

The last step is to merge *resolve-conflict* into *amend-my-name*, thus
bringing with it the changes from *unmergeable-branch*:

#.  `git checkout checkout amend-my-name`
#.  `git merge resolve-conflict`
#.  `git push origin amend-my-name`
