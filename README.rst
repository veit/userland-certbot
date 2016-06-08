===================
Certbot in Userland
===================

Certbot is a client for automated certificate authorities (CA)
especially Let's Encrypt.

For information about Let's Encrypt please visit: https://letsencrypt.org

This project helps you to setup and run Certbot in userland
which means within an unprivileged user account (non-root) in this context.

For information about Certbot please visit: https://certbot.eff.org

This software is licensed under GNU General Public License, Version 3,
see LICENSE.txt for details.


Scenario
========

We assume you are webmaster of example.com and some related subdomains
and want to acquire and renew TLS certificates from Let's Encrypt.
You have SSH access to the webspace and are allowed to run locally
deployed software and cronjobs in userland.


Installation
============

Create a Python environment with a buildout module:

    $ virtualenv venv
    $ cd venv
    $ bin/pip install zc.buildout

Clone this project from Github:

    $ git clone https://github.com/veit/userland-certbot.git

Change into the projects directory:

    $ cd ../userland-certbot

Buildout (actually install) the environment:

    $ ../venv/bin/buildout


Registration
============

Before use you to have to register first. 
This creates a Let's Encrypt account linked to your email address.

$ bin/certbot-register


Getting Certificates
====================

To acquire a certificate from Let's Encrypt simply run:

$ bin/certbot-runner certonly -d example.com -d www.example.com...

Please ensure that your webserver serves content for
* http://example.com/.well-known/acme-challenge
* http://www.example.com/.well-known/acme-challenge
* ...
from <install-dir>/parts/certbot/web/.well-known/acme-challenge
so that *acquisition requests* can be properly processed.


Renewing Certificates
=====================

To renew all certificates due to renewal simply run:

$ bin/certbot-runner renew [--force-renewal]

Please ensure that your webserver serves content for
* http://example.com/.well-known/acme-challenge
* http://www.example.com/.well-known/acme-challenge
* ...
from parts/certbot/web/.well-known/acme-challenge
so that *renewal requests* can be properly processed.


Fully automated Renewal
=======================

Some notes related to automated renewal:

* A cronjob for automated renewal is automatically installed.
* Please check if it is working correctly.
* After successful renewal an email will be sent to webmaster@example.com.
