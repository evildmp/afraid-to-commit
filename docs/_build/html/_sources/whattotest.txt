===========================
Testing policy and strategy 
===========================

It's often not at all obvious *what* to test, especially when you're
approaching it for the first time.

Where to start
==============

So what should you test? The correct but distinctly unhelpful answer is
*everything*. What you need to do is find a good place to get started,
particularly if you find yourself in a situation with a lot of code, and no
tests at all.

Here are some basic rules that will help guide you into the process:

* write a test for the next thing you add, fix or change 
* write a test for each link in a chain of logic
* write tests from the centre outwards

These are all explained in more detail further below.

What should tests look like?
============================

Should they be many or few; should each one be small or large, simple or
complex, limited or comprehensive, weak or powerful, atomic or compound?

The thing to realise is that **your tests should not be like your code**. They
are complementary to it. Your code is synthetic, complex, productive and. It
does new and clever things. Your tests need to be the opposite; analytic,
simple and merely reproductive. The duller and more banal they are, the
better.

Be uninteresting and trite in your tests that you be imaginative and creative
in your code. Tests are *meant* to look unexciting.

Arrangement of test classes and methods
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Use your test classes to organise tests into logical, sensible groups.
Sometimes it's suggested to have a test class for each class in your code;
often that makes sense, but it's not a rule and won't always be appropriate.

The rule for test methods on the other hand is very simple: in each test
method, test **one case that could go wrong**.

Yes, this will mean you end up with lots of test methods. But that's good!
Their strength comes not from their complexity, but their number.

How to write tests
==================

Code is synthetic; tests are analytic
-------------------------------------

It's tempting, but a mistake, to think about tests the way you think about
your code. 

Your system is designed to do the right thing at every stage in a sucession of
unfolding scenarios, and that's what you want it to do correctly. The obvious
way to test this then might be to model the circumstances and check the
behaviour of the system as you put it through its paces.

It's not impossible to write tests like this, and it will even work. But, it
will not prove efficient or effective or sustainable. That's because this way
of thinking is the way you need to think when *creating* your code, about a
*synthetic* process that itself produces something new. Testing on the other
hand is merely *analytic*; nothing new is produced or created in tests, and
your thinking about them should reflect that.

So, to think about testing think about the operation, out of context of the
whole, of the little pieces of the mechanisms of your system.



The three rules of What to test
===============================

Write a test for the next thing you add, fix or change 
------------------------------------------------------

Rather than trying to select something in your code to create tests, just wait
until the next time you add code, fix a bug or otherwise make a change. Then
create tests that proves your new code works the way it should.

For example, suppose you create or amend a method that calculates the area of
a surface from some combination of its dimensions and its shape; now is the
time to write a series of tests that call this methods with a series of
parameters and check that it returns the correct value for surface area in
each case.                                                          

You don't have to cover every possible case the first time round
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

For a simple calculation, you might write a test that catches all possible
combinations of input and output of the method. It's quite likely though that
you won't. That's OK. However, the moment you spot it misbehaving, that's your
cue to fix the bug and write a test that checks it now behaves correctly. 

Regression tests
^^^^^^^^^^^^^^^^

When you fix a bug and write a test that would catch the buggy behaviour in
the code, this is called a *regression test*; it's a test that ensures that
your code doesn't later get *worse*, and that bugs that were once fixed creep
back into your commits.

If you fix a bug, you're doing a good job. If you fix two bugs, that's twice
as good. But if you *fix the same bug twice* you are *wasting your precious
time*. You should never have to do that. Fix it once, write a test for it, and
know that it won't slip in again undetected.

Write a test for each link in a chain of logic
----------------------------------------------

The temptation might be to test the chain as a whole. After all, the proof of
a pudding is in its eating, and what we're really interested in is the
outcome, not the details of the process.

Well, that's not follow. The outcome *is* more important than the details of
the process, but just because it's the thing that matters most doesn't mean
that that it's the best thing to test.

Suppose you have a method on a ``Person`` model that determines what address
should be displayed for the individual. This could involve a long chain of
logic:

*	has the ``Person`` given consent to have their address displayed?
*	if so, does the ``Person`` have an explicit address?
*	if not, does the ``Person`` belong to an ``Institution``?
*	if so, does that ``Institution`` have an address?
* if not, does that ``Institution`` have a parent ``Institution`` which does?

... and so on.

Now you could just test the end result - certainly you'd have fewer tests than
if you tested all the intermediate logic and methods. However:

* your tests will be more complicated
* they'll be harder to maintain
* they will never tell you exactly *where* something went wrong
* they'll make it harder to refactor your code
* if you want to rely on one of the intermediate methods for something else,
  you won't have so much faith in it 
  
Write tests from the centre outwards
------------------------------------

Your models are at the heart of your code in the way that your views, for
example, are not. The views depend on the models; so start with the models'
managers and their methods before moving outwards to views and URLconfs -
start with the things that *other* things depend on.