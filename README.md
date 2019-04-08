## Linux Server Configuration

In this project I take the application that I developed for the Item Catalog project, [Music Catalog](https://github.com/tipcat/item-catalog), and place it onto a public Ubuntu Linux web server, while also securing the back-end from potential intruders. The application is hosted at [AWS Lightsail](https://aws.amazon.com/lightsail/) via the IP address ``3.94.214.35`` and may be viewed here: http://3.94.214.35.xip.io/. The ``xip.io`` suffix is necessary to conform to Google's requirements for authenticating the user via OAuth 2.0.

### Logging in
To log in to the server, the ``grader`` user will have saved the private key I gave them (and *only* them) to their local machine. This obviates the need for a password-based login and enforces key-based ``SSH`` authentication. Then ``grader`` will log in with ``ssh -i ~/.ssh/udacity_key.rsa -p 2200 grader@3.94.241.35`` using the Git Bash command line interface.

### Summary of Configuration Changes Made
* In line with the above, all password-based logins have been disabled. Any new user would first need to obtain a private key from the owner to pair up with the public key that has been placed on the server.
* UFW (Uncomplicated firewall) is used to enhance security by disabling default port 22 for logging in via ``SSH``. Port 2200 has been enabled in its place.
* To further enhance security, root login has been disabled.
* The ``grader`` user has been given ``sudo`` permissions to evaluate this project. As with logging in, no password is needed to perform ``sudo`` operations.
* All packages have been updated and are set to auto-update.
* Used UFW to open port 80 for ``HTTP`` connections and port 123 for ``NTP``. Apart from port 2200 these are the *only* open ports.
* All packages needed to make the application code work properly have been installed: ``python-pip, postgresql, psycopg2, flask, Flask-SQLAlchemy, requests, httplib2`` and ``oauth2client``.
* PostgreSQL has been substituted in place of SQLite for more robust security. A special user named ``catalog`` has been created to effect proper creation of the database. Only the ``catalog`` user has power over the database; all public access has been revoked. Additionally, the original Python application code has been modified to initialize the database via PostgreSQL.
* Apache is used for the server and Web Server Gateway Interface (WSGI) is used for calling the application code. These have been installed via the ``apache2`` and ``libapache2-mod-wsgi python-dev`` packages.

### Sources Consulted
Building this server required resources that went significantly beyond the content covered in Udacity's [Full Stack Web Development](https://www.udacity.com/course/full-stack-web-developer-nanodegree--nd004) course, and I am grateful for the following:
* https://stackoverflow.com/questions/7210011/amazon-ec2-ssh-timeout-due-inactivity
* https://www.linode.com/docs/security/firewalls/configure-firewall-with-ufw/
* https://www.digitalocean.com/community/tutorials/ufw-essentials-common-firewall-rules-and-commands
* https://www.liquidweb.com/kb/changing-the-ssh-port/
* https://askubuntu.com/questions/147241/execute-sudo-without-password
* https://medium.com/coding-blocks/creating-user-database-and-adding-access-on-postgresql-8bfcd2f4a91e
* https://serverfault.com/questions/520195/how-does-servername-and-serveralias-work
* https://askubuntu.com/questions/391184/but-is-referred-to-by-another-package-finding-that-package
* https://www.a2hosting.com/kb/developer-corner/apache-web-server/viewing-apache-log-files
* https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps
* https://github.com/daphnetull/linux-sever-config
* https://github.com/iliketomatoes/linux_server_configuration
* https://github.com/boisalai/udacity-linux-server-configuration
* https://github.com/kongling893/Linux-Server-Configuration-UDACITY
* https://github.com/kbongco/Udacity-Linux-Server-Configuration
