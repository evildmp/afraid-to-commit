##########
Cheatsheet
##########


virtualenv
==========

create
    ``virtualenv [name-of-virtualenv]``
    
include system's Python packages
    ``virtualenv [name-of-virtualenv] --install-site-packages``

activate
    ``source bin/activate``
  
deactivate
    ``deactivate``
    

pip
===

install
    ``pip install [name-of-package]``

install a particular version
    ``pip install [name-of-package]==[version-number]``

upgrade
    ``pip install --upgrade [name-of-package]``
    
uninstall
    ``pip uninstall [name-of-package]``
    
show what's installed
    ``pip freeze``
 
git
===

tell git who you are
    ``git config --global user.email "you@example.com"``

    ``git config --global user.name "Your Name"``

clone a repository
    ``git clone [repository URL]``


checkout
    ``git checkout [branch]`` switches to another branch

    ``git checkout -b [new-branch]`` creates and switches to a new branch

    ``git checkout -b [new-branch] [existing branch]`` creates and
    switches to a new branch based on an existing one

    ``git checkout -b [new-branch] [remote/branch]`` creates and
    switches to a new branch based on ``remote/branch`` 
    
    ``git checkout [commit sha]`` checks out the state of the repository at a
    particular commit

status
    ``git status``

commit
    git commit -m "[your commit message]"
    
add
    ``git add [filename]`` adds a file to the staging areas   

    ``git add -u [filename]`` - the ``-u`` flag will also remove deleted files  
    
remote
    ``git remote add [name] [remote repository URL]`` sets up remote

    ``git remote show`` lists remotes
    
    ``git remote show -v`` lists remotes and their URLs    

branch
    ``git branch``

    ``git branch -a`` to show remote branches too  
    
fetch
    ``git fetch`` gets the latest information about the branches on the default
    remote
    
    ``git fetch [remote]`` gets the latest information about the branches on the
    named remote
    
merge
    ``git merge [branch]`` merges the named branch into the working directory

    ``git merge [remote/branch] -m "[message]"`` merges the branch referred to
    into the working directory - **don't forget to fetch the remote before the
    merge**
    
pull
    ``fetch`` followed by ``merge`` is often safer than ``pull`` - don't assume that
    ``pull`` will do what you expect it to

    ``git pull`` fetches updates from the default remote and merges into the
    working directory

push
    ``git push`` pushes committed changes to the default remote, in branches
    that exist at both ends

    ``git push [remote] [branch]`` pushes the current branch to the named
    ``branch`` on ``remote``  
    
log
    ``git log`` will show you a list of commits

Notes
-----

Throughout Git, anything in the form ``remote/branchname`` is a reference, not a
branch.
