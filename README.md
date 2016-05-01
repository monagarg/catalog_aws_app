Project: Linux Server Configuration - Mona Garg 
Version: 1.0 04/30/2016
================================

Overview
------------------
The Linux Server Configuration project requires to configure the assigned aws server and to deploy the web application that was development as part of the third project (Item Catalog) 


Required Libraries and Dependencies
-----------------------------------
Please refer to requirements.tx


AWS Server Details
------------------------
IP Address: 52.37.1.25
SSH Port: 2200
Complete URL: http://52.37.1.25/ and http://ec2-52-37-1-25.us-west-2.compute.amazonaws.com/


Summary of Configurations Changes 
----------------------------------

/#  connect to the server
ssh -i ~/.ssh/udacity_key.rsa root@52.37.1.25


 # add a new user 
 sudo adduser grader

 # provide password and complete the request

 <password>

 # copy the public key from the root to the grader user
 mkdir .ssh
 chmod 700 .ssh
 chmod 655 .ssh/authorized_keys
 cp .ssh/authorized_keys /home/grader/.ssh/authorized_keys

 # give root permissions to grader
 cd /etc/sudoers.d
 vi grader
 grader ALL=(ALL:ALL) ALL

 # login with grader user
 ssh -i ~/.ssh/udacity_key.rsa grader@52.37.1.25

 # disable root login
 PermitRootLogin no
 sudo service ssh restart

 # update packages
 sudo apt-get update
 sudo apt-get upgrade

 # change the ssh port from 22 to 2200
 sudo vi /etc/ssh/sshd_config
 reload ssh
 ssh -p 2200 -i ~/.ssh/udacity_key.rsa grader@52.37.1.25

 # setup ports
 sudo ufw status
 sudo ufw allow www
 sudo ufw allow 2200
 sudo ufw allow ntp
 sudo ufw enable
 sudo ufw status

 # add the hostname to the /etc/hosts file
 127.0.0.1 ip-10-20-29-146

 # install apache
 sudo apt-get install apache2
 sudo apt-get install libapache2-mod-wsgi

 # install dependencies
 sudo apt-get install postgresql
 sudo apt-get install python-pip
 sudo pip install Flask==0.9
 sudo pip install Flask-HTTPAuth==2.7.0
 sudo pip install Flask-Login==0.1.3
 sudo pip install SQLAlchemy==0.8.4
 sudo pip install Werkzeug==0.8.3
 sudo pip install oauth==1.0.1
 sudo pip install oauth2client==1.5.1
 sudo pip install psycopg2==2.4.5
 sudo apt-get install libpq-dev python-dev

 # set password for postgres user
 sudo -u postgres psql postgres
 \password postgres
 \q
 
 # allow local connections as specified in the following link
 http://suite.opengeo.org/opengeo-docs/dataadmin/pgGettingStarted/firstconnect.html
 
 # set up the flask application using the following link
 https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps

 # set up git and download the code from git repository to the aws server
 
 # set up the postgres server by running the database scripts
 sudo python database_setup_shared.py
 sudo python lotsofstuff.py

 # configure the catalog.wsgi file

 # create and configure the /etc/apache2/sites-enabled/catalog.conf file

 # disable to apache default conf

 # make changes to the application_sharedstuff.py to reflect the correct location of the client_secrets file

 # make changes to the client_secrets file to add the aws ip address and the url

 # make changes to the application oauth credentials to add the aws ip address and the url

 # restart the apache service
 sudo apache2ctl restart

 # reboot the system
 sudo reboot

 # navigate to the following urls
 http://52.37.1.25/
 http://ec2-52-37-1-25.us-west-2.compute.amazonaws.com/


List of third party resources 
---------------------------------- 
http://suite.opengeo.org/opengeo-docs/dataadmin/pgGettingStarted/firstconnect.html
https://discussions.udacity.com/t/markedly-underwhelming-and-potentially-wrong-resource-list-for-p5/8587
https://www.phusionpassenger.com/library/walkthroughs/deploy/python/aws/apache/enterprise/tarball/deploy_app.html
http://suite.opengeo.org/opengeo-docs/dataadmin/pgGettingStarted/firstconnect.html
https://discussions.udacity.com/c/nd004-p7-linux-based-server-configuration












