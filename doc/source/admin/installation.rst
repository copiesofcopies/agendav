Installation
============

In this section you will be able to install AgenDAV.

Prerequisites
-------------

AgenDAV |release| requires the following software to be installed:

* A CalDAV server (developed mainly with `DAViCal <http://www.davical.org/>`_
* A web server
* PHP >= 5.3.0
* PHP mbstring extension
* MySQL > 5.1

.. note::
   AgenDAV will only work with CalDAV servers that support HTTP Basic
   Authentication, and will fail with those that only support HTTP Digest
   Authentication. Please, refer to your CalDAV server for information about
   how to enable Basic Authentication.

Downloading AgenDAV and uncompressing
-------------------------------------

AgenDAV |release| can be obtained at `AgenDAV official webpage
<http://agendav.org>`_, but you can use GitHub to download latest version.
Have a look at `<http://github.com/adobo/agendav>`_.

Uncompress it using ``tar``::

 $ tar xzf adobo-agendav-...tar.gz
 $ cd adobo-agendav-.../

Database and tables
-------------------

AgenDAV needs a MySQL database with several tables created. There is a file
called ``schema.sql`` inside the directory ``sql/`` which contains the
table schemas.

Create an user in MySQL like this::

 $ mysql --default-character-set=utf8 -uroot -p
 Enter password: 
 [...]
 mysql> GRANT ALL PRIVILEGES ON agendav.* TO agendav@localhost IDENTIFIED BY 'yourpassword'
 mysql> CREATE DATABASE agendav CHARACTER SET utf8 COLLATE utf8_general_ci;
 mysql> FLUSH PRIVILEGES;
 mysql> ^D

And then run the schema creation file::

 $ mysql --default-character-set=utf8 -uagendav -p agendav < sql/schema.sql
 Enter password:
 $

Note the UTF8 parts on the previous commands. If you don't specify them you
will have some issues with special characters.

Now your database is ready.

Configuring Apache web server
-----------------------------

Apache has to be configured to point to ``web/public`` directory, using its
own VirtualHost or just an Alias.

Example using a dedicated virtualhost::

 <VirtualHost 1.2.3.4:443>
  ServerAdmin admin@email.host
  DocumentRoot /path/to/agendav/web/public
  ServerName agendav.host
  ErrorLog logs/agendav_error_log
  CustomLog logs/agendav_access_log common
 </VirtualHost>

Example using the Alias directive::

 Alias /agendav /path/to/agendav/web/public

.. note::
   Make sure that you have the following PHP settings *disabled*:

   * ``magic_quotes_gpc``
   * ``magic_quotes_runtime``

Other web servers
^^^^^^^^^^^^^^^^^

AgenDAV should work on all other web server software if they support PHP
scripts, but this is untested.

Configure AgenDAV
-----------------

Now you can proceed to configure AgenDAV following the :doc:`configuration`
section.
