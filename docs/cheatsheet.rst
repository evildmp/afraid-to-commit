##########
Cheatsheet
##########


virtualenv
==========

create
    `virtualenv [name-of-virtualenv]`
    
include system's Python packages
    `virtualenv [name-of-virtualenv] --install-site-packages`

activate
    `source bin/activate`
  
deactivate
    `deactivate`
    

pip
===

install
    `pip install [name-of-package]`

install a particular version
    `pip install [name-of-package]==[version-number]`

upgrade
    `pip install --upgrade [name-of-package]`
    
uninstall
    `pip uninstall [name-of-package]`
    
show what's installed
    `pip freeze`
