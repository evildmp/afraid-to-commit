##################
Running a workshop
##################

If you'd like to run a workshop based on this material, please do, and please
let me know about it.

Notes on running a workshop
===========================

To cover all the workshop material seems to take about four and a half hours.

Any of the following will make it take longer:

* attendees who aren't already a little familiar with the terminal and using a
  text editor to edit source files 
* attendees whose machines aren't already suitably-configured for the workshop
  and need software installed    
* attendees using operating systems you're not familiar with

If you're lucky, you'll find that the majority of attendees have the same
expertise and the same gaps in expertise. This makes it much easier to decide
which parts to dwell upon and which ones you can skim over. If you're not
lucky, they will each have a completely different skillset.

You'll do a lot of running around to look at people's screens, so it helps to
be able to get around the room easily.         

The *Git on the commandline* section is the one where you will be in most
demand - it helps great if at this stage you have one or two helpers who are
familiar with Git.

Watch out for wireless network limitations - at one session the promised
network turned out to block both github.com and ssh, and we had to rely on an
access point created by someone's mobile telephone.

Things that might look odd
==========================

If you're experienced with things virtualenv and Git, some of the way things
are done here might strike you as odd. For example:

Virtualenvs and code
-------------------- 

The workshop has users put all the code they're working with into their
virtualenv directories. This is done to help associate a particular project and
set of packages with each virtualenv, and saves excessive moving around between
directories.

Editing and committing on GitHub
--------------------------------

That's certainly not what we'd normally do, but we do it here for three main
reasons:

* GitHub's interface is a friendly, low-barrier introduction to Git operations
* it's easy for people to see the effects of their actions straight away
* they get to make commits, pull requests and merges as soon as possible after
  being introduced to the concepts

The last of these is the most significant.    

Other oddities
--------------

There may be others, which might be for a good reason or just because I don't
know better. If you think that something could be done better, please let me
know.
