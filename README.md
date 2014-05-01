dev-env
=======

A virtual developer environment to ease the development of the studentenportal project for Windows and MAC users.
This will install the whole environment needed to run the web application on a virtual machine (like VMWare or VirtualBox) with the help of [Vagrant](http://www.vagrantup.com/).

Please note that while this configuration is similar to the deploy repo, it is
only meant for setting up a local dev environment, not as a stage environment.

Requirements
------------

Required programs:
- Virtualization software (VirtualBox or VMWare)
- Vagrant to setup the virtual machine
- Ansible to provision the environment

Installation instructions:

1. Install VirtualBox: https://www.virtualbox.org/wiki/Downloads
2. Install Vagrant: https://docs.vagrantup.com/v2/installation/
3. Install Ansible: http://www.ansibleworks.com/docs/intro_installation.html

There are many platform specific guides on the internet. It might be easier to follow such a guide than fighting yourself through the individual installation instructions.

Setup Machine
-------------

1.  Setup the following folder structure by cloning the github repos:

    ```
    `-- <studentenportal project root>
        |-- web (https://github.com/studentenportal/web.git)
        `-- dev-env (https://github.com/studentenportal/dev-env.git)
    ```
2.  Switch to the dev-env directory and provision it:

    ```bash
    vagrant up
    ```
    Vagrant will automatically sync the `web` folder with `/srv/www/studentenportal`

3.  Connect to the VM via SSH and setup the environment:

    ```bash
    vagrant ssh
    ```

Setup Environment
-----------------

1.  Switch to the folder `/srv/www/studentenportal`
2.  `sudo pip install -r requirements/local.txt`

    Installing all the packages can take a while.
3.  `python manage.py syncdb`
4.  `python manage.py migrate apps.front`
5.  `python manage.py migrate apps.documents 0001`
6.  `python manage.py migrate apps.lecturers 0002`
7.  `python manage.py migrate apps`

Run the server inside the VM and allow external connections:
```
python manage.py runserver 0.0.0.0:8000
```

Access the site via `localhost:8000`

Install Test Data
-----------------
You can create test data manually with the django-admin (`localhost:8000/admin`).
There is more information to test data on the [main repo](https://github.com/studentenportal/web).

It is however far easier to install provided test data (fixtures).
Because the data of the registered users is confidential, we cannot provide the real data publicly. If you want to mirror the real data of the `studentenportal` simply contact us.

Loading fixtures into the database is pretty simple:
```
python manage.py loaddata /path/to/fixture.json
```

More information
----------------
https://github.com/studentenportal/web


