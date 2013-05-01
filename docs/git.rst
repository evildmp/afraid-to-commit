##############
Git and GitHub
##############


What is it?
===========

Git is a source code management system, designed to support collaboration.

GitHub is a web-based service that hosts Git projects, including Django
itself: https://github.com/django/django.

The key idea in Git is that it's *distributed*. If you're not already familiar
with version control systems, then explaining why this is important will only
introduce distinctions and complications that you don't need to worry about,
so that's the last thing I will say on the subject.
                                                      

Set up a GitHub account
=======================

* sign up at http://github.com. 

It's free.


Some basic Git and GitHub operations
====================================

Forking
-------

* visit https://github.com/evildmp/afraid-to-commit/

You can do various things there, including browsing through all the code and files.

* hit the **Fork** button

A few moments later, you'll have your own copy, on GitHub, of everything in that repository, and from now on you'll do your work on your copy of it.

Your copy is at https://github.com/<your github account>/afraid-to-commit/. 

You will typically do this for any Git project you want to contribute to. It's
good for you because it means you don't have to sign up for access to a
central repository to be permitted to work on it, and even better for the
maintainers because they certainly don't want to be managing an small army of
volunteers on top of all their other jobs.

.. note::
   Don't worry about all the forks

    You'll notice that there might be a few forks of
    https://github.com/evildmp/afraid-to-commit; if you have a look at
    https://github.com/django/django you'll see thouands. There'll even be
    forks of the forks. Every single one one is complete and independent. So,
    which one is the real one; which one is *the* Django repository?
    
    In a technical sense, they all are, but the more useful answer is: the
    one that most people consider to be the canonical or official version.
    
    In the case of Django, the version at https://github.com/django/django is
    the one that forms the basis of the package on PyPI, the one behind the
    https://djangoproject.com/ website, and above all, it's the one that the
    community treats as cannonical and official, not because it's the original
    one, but because it's the most useful one to rally around.
    
    The same goes for https://github.com/evildmp/afraid-to-commit and its
    more modest collection of forked copies. If I stop updating it, but
    someone else is making useful updates to their own fork, then in time
    theirs might start to become the one that people refer to and contribute
    to. The same could even happen to Django itself, though it's not likely to
    any time soon.
    
    The proliferation of forks doesn't somehow dilute the original. They are
    simply the way collaboration is made possible.

Edit a file
-----------

GitHub allows you to edit files online. This isn't something you'll want to
spend too much time doing, but it's handy for very small changes, like typos
and spelling mistakes you spot.

*   go to https://github.com/<your github account>/afraid-to-commit
*   find the `attendees_and_learners.rst` file
*   hit the **Edit** button
*   add your name and address to the appropriate place in the file
*   if following the tutorial by yourself, add your
    details in the *I followed the tutorial online* section.

Commit your changes
-------------------

*   hit **Commit Changes**

Now *your* copy of the file, the one that belongs to *your* fork of the
project, has been changed; it's reflected right away on GitHub.

If you managed to mis-spell your name, or want to correct what you entered,
you can simply **edit** it again.

Make a Pull Request
-------------------

When you're ready to have your changes incorporated into my
original/official/canonical repository, you do this by making a **Pull
Request**.

* hit the **Pull Request** button

GitHub will show you that your version, the
**head repo**` - on the right - has some commits containing file changes, that
will be sent to my **base repo** - on the left.

* add a comment if you like
* hit **Send pull request**

GitHub will notify me (by email and on the site, and will show me the changes
you're proposing to make). It'll tell me whether they can be merged in
automatically, and I can reject, or accept, or defer a decision on, or comment
on, your pull request.

GitHub can merge your contribution into my repository if mine hasn't changed
too much since you forked it, leaving GitHub unable to work out how to
incorporate it. If I want to accept it but GitHub can't do it automatically, I
will have to merge the changes manually.
                                        
Once they're merged though, your contribution will become a part of
https://github.com/evildmp/afraid-to-commit, and that's the basic lifecycle of
a contribution using git: *fork*, *edit*, *commit*, *pull request*, *merge*.
Your code did indeed fork away briefly, but only in order to rejoin the
centre.

Incorporate upstream changes
----------------------------

In the meantime, other people may have made their own forks, edits, commits,
and pull requests, and I may have merged those too. Your own version of
afraid-to-commit, *downstream* from mine, doesn't yet know about those.

If you're planning to base your work on mine, then you can think of my
repository as being *upstream* of yours. You need to merge my *upstream*
changes into *your* version, and you can do this with a pull request on GitHub
too:

* hit **Pull Request** once more
* change the **head repo** on the right to *my* version,
  `evildmp/afraid-to-commit`
* change the **base repo** to yours
* add a **Title** and hit **Send pull request**

You're sending a pull request to to yourself, based on updates in my
repository. And in fact if you check in your **Pull Requests** on GitHub,
you'll see one there waiting for you, and you too can review, accept, reject
or comment on it.

If you decide to **Merge** it, your fork will now contain any changes that
other people sent to me and that I merged.
