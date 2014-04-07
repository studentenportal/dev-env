dev-env
=======

A Vagrant developer environment for the studentenportal project.
Please note that while this configuration is similar to the deploy repo, it is
only meant for setting up a local dev environment, not as a stage environment.

This dev environment is meant to ease the development for Windows users.

Requirements
------------
Vagrant is used to setup a virtual machine, it should work with VirtualBox and
VMWare.
Ansible is used to setup all the tools and the runtime environment.

Installation instructions:
- https://docs.vagrantup.com/v2/installation/
- http://www.ansibleworks.com/docs/intro_installation.html

Setup Machine
-------------
Setup the machine and provision it
```bash
vagrant up
```
Now connect to the VM:
```bash
vagrant ssh
```
Assuming you have the following folder structure, Vagrant will automatically
sync the `web` folder with `/srv/www/studentenportal`
```
`-- <your projects>
    |-- web (https://github.com/studentenportal/web.git)
    `-- dev-env (https://github.com/studentenportal/dev-env.git)
```


Setup Environment
-----------------
Go to the folder `/srv/www/studentenportal` and proceed like described in the
web repository:
https://raw.githubusercontent.com/studentenportal/web/master/README.md
