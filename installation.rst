Installation
############

While this manual contains Linux-specific instructions, CORE is capable of 
running on other web servers, such as IIS. Currently CORE can only be installed
through command line operations.

Requirements
============

* Running web server. This can be local or on the internet
* `CakePHP <http://cakephp.org>`_ 1.3.x (tested up to 13) in the same directory 
  where CORE will reside, named ``cakephp``. 
  Example:: 

    /var/www/core
    /var/www/cakephp

* MySQL Server

Downloading CORE and CakePHP
============================

CORE makes use of other open source software. Because of this, the easiest way 
to install it is to install it by cloning with `git <http://git-scm.com>`_. This
will ensure that all dependencies are downloaded as well. Start by cloning both
CORE and CakePHP::

    $ git clone --recursive https://github.com/rockharbor/core.git core
    $ git clone https://github.com/cakephp/cakephp.git cakephp
    $ cd cakephp
    $ git checkout 1.3.11

Configuration
=============

There is some basic configuration to CORE you will need to make when you first 
install.

1. Rename the ``config/core.php.default`` to ``config/core.php``
2. Change the salt value in ``config/core.php``
3. Rename the ``config/database.php.default`` to ``config/database.php``
4. Change the username/password/database values in ``config/database.php``
5. Make sure MySQL is running and create the database you configured in 
``config/database.php``

Install default application data
================================

.. note::

    In order to run the installer, you must have 
    `CakePHP's bake <http://book.cakephp.org/view/1106/The-CakePHP-Console>`_ running. 

To install the default data and initialize the upload directories, run the 
following bake commands::

	$ cake install install
	$ cake media init

After installing the default data, an admin user will be created. The username is
'admin' and the password is 'password'.

Other server configuration
==========================

CORE needs some directories writable, for cache and uploads. You will need to 
make sure the ``tmp`` and ``webroot/media/transfer`` directories are writeable.

To reduce server load and improve the user experience when sending large amounts
of emails, CORE uses a CRON job to send emails in groups. In order to send email
you will need to set up a CRON job (or Scheduled Task). The command to call is::

    $ cake -app "/var/www/core" queue_sender send