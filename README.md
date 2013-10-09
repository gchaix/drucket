Drucket
==============

Creates VirtualBox VM on your local machine pre-configured with Apache, PHP, MySQL. This method provides a viable alternative to MAMP or XAMPP or even a local LAMP stack, especially for diverse teams working on the same project.

Requirements
==============

* VirtualBox version 4.2.10 or newer - https://www.virtualbox.org/wiki/Downloads
* VirtualBox extensions 4.2.10 or newer - http://download.virtualbox.org/virtualbox/4.2.10
* Vagrant version 1.0.7 or newer - http://vagrantup.com/
* A 64bit-capable processor and operating system (Tested with Ubuntu 12.10 and OS X 10.6)
  * It should be possible to run on a 32bit host machine by substituting a 32bit base box, but this has not been tested. Feedback is welcome!

Installation
=============

* Install [vagrant 1.0.x](http://downloads.vagrantup.com/) (the 1.1 branch might work, but we haven't tested it)
* Install [VirtualBox](https://www.virtualbox.org/wiki/Downloads)
* Install [git](http://git-scm.com/downloads) if you don't have it already. If you're not familiar with git, [ensure you are](http://git-scm.com/doc).
* Clone this repository. It provides the root of a new project repository.
* Put your project webroot in the `{reporoot}/htdocs` directory.

Configuration details
==============

* The VM is running CentOS 6, Apache 2.2.15, MySQL 5.1, PHP 5.3.3.
* The EPEL repo is enabled, so newer versions of packages are available.
* Apache is configured to serve up /server/htdocs by default.
* The root password is 'vagrant'.
* The 'vagrant' user is set to have full sudo rights, no password required.
* The root user on the MySQL server is preconfigured and the credentials are stored in the root user's .my.cnf, so you can run `sudo mysql` and be logged in on the MySQL console as root.
* The directory containing the Vagrantfile config file and the rest of this repository (including your project webroot) on your local machine is mounted on the virtual machine in `/server` to facilitate moving files to and from the virtual machine.

Usage
==============

* To start up the virtual machine, run `vagrant up` in the same directory as the Vagrantfile config file. As soon as it's booted you should be able to hit http://localhost:8080/ and see whatever is in the `{reporoot}/htdocs` directory.
* If your application uses a MySQL database, configure your app to connect to `localhost` with the username `root` and password `root`.
* To access the virtual machine, run `vagrant ssh`.  That will log you into the virtual machine as the user `vagrant`.
  * In typical usage, you should only need to run database commands within the VM. All other work happens on your physical host computer.
* To shut the machine down, run `vagrant halt`.  This gracefully shuts the machine down, retaining whatever changes you've made to the VM.
* To delete the virtual machine, run `vagrant destroy`.  This will completely erase the virtual machine and your MySQL databases. Your `Vagrantfile`, application code, and puppet rules are all left intact.
