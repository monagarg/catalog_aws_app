 
Project: Linux Server Configuration - Mona Garg
================================================


Version
--------
1.0 04/30/2016


Overview
------------------
The Linux Server Configuration project requires to configure an aws server and to deploy the web application that was developed as part of the Item Catalog project.
 

Required Libraries and Dependencies
-----------------------------------
Please refer to requirements.txt


AWS Server Details
------------------------
IP Address: 52.37.1.25 <br>
SSH Port: 2200 <br>
Complete URL: http://52.37.1.25/ and <br>
http://ec2-52-37-1-25.us-west-2.compute.amazonaws.com/


Summary of Configurations Changes 
----------------------------------

\#  connect to the server <br>
ssh -i ~/.ssh/udacity_key.rsa root@52.37.1.25


\# add a new user <br> 
sudo adduser grader

\# provide password and complete the request <br>
<password>

\# copy the public key from the root to the grader user <br>
mkdir .ssh <br>
chmod 700 .ssh <br>
chmod 655 .ssh/authorized_keys <br>
cp .ssh/authorized_keys /home/grader/.ssh/authorized_keys

\# give root permissions to grader <br>
cd /etc/sudoers.d <br>
vi grader <br>
grader ALL=(ALL:ALL) ALL

\# login with grader user <br>
ssh -i ~/.ssh/udacity_key.rsa grader@52.37.1.25

\# disable root login <br>
PermitRootLogin no <br>
sudo service ssh restart

\# update packages <br>
sudo apt-get update <br>
sudo apt-get upgrade

\# change the ssh port from 22 to 2200 <br>
sudo vi /etc/ssh/sshd_config <br>
reload ssh <br>
ssh -p 2200 -i ~/.ssh/udacity_key.rsa grader@52.37.1.25

\# setup ports <br>
sudo ufw status <br>
sudo ufw allow www <br> 
sudo ufw allow 2200 <br>
sudo ufw allow ntp <br>
sudo ufw enable <br>
sudo ufw status

\# add the hostname to the /etc/hosts file <br>
127.0.0.1 ip-10-20-29-146

\# install apache <br>
sudo apt-get install apache2 <br>
sudo apt-get install libapache2-mod-wsgi <br>

\# install dependencies <br>
sudo apt-get install postgresql <br>
sudo apt-get install python-pip <br>
sudo pip install Flask==0.9 <br>
sudo pip install Flask-HTTPAuth==2.7.0 <br>
sudo pip install Flask-Login==0.1.3 <br>
sudo pip install SQLAlchemy==0.8.4 <br>
sudo pip install Werkzeug==0.8.3 <br>
sudo pip install oauth==1.0.1 <br>
sudo pip install oauth2client==1.5.1 <br>
sudo pip install psycopg2==2.4.5 <br>
sudo apt-get install libpq-dev python-dev <br>

\# set password for postgres user <br>
sudo -u postgres psql postgres <br>
\password postgres <br>
\q 
 
\# allow local connections as specified in the following link <br>
http://suite.opengeo.org/opengeo-docs/dataadmin/pgGettingStarted/firstconnect.html
 
\# set up the flask application using the following link <br>
https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps

\# set up git and download the code from git repository to the aws server
 
\# set up the postgres server by running the database scripts <br>
sudo python database_setup_shared.py <br>
sudo python lotsofstuff.py

\# configure the catalog.wsgi file

\# create and configure the /etc/apache2/sites-enabled/catalog.conf file

\# disable to apache default conf

\# make changes to the application_sharedstuff.py to reflect the correct location of the client_secrets file

\# make changes to the client_secrets file to add the aws ip address and the url

\# make changes to the application oauth credentials to add the aws ip address and the url

\# restart the apache service <br>
sudo apache2ctl restart

\# reboot the system <br>
sudo reboot

\# navigate to the following urls <br>
http://52.37.1.25/ <br>
http://ec2-52-37-1-25.us-west-2.compute.amazonaws.com/


List of third party resources 
---------------------------------- 
http://suite.opengeo.org/opengeo-docs/dataadmin/pgGettingStarted/firstconnect.html
https://discussions.udacity.com/t/markedly-underwhelming-and-potentially-wrong-resource-list-for-p5/8587
https://www.phusionpassenger.com/library/walkthroughs/deploy/python/aws/apache/enterprise/tarball/deploy_app.html
http://suite.opengeo.org/opengeo-docs/dataadmin/pgGettingStarted/firstconnect.html
https://discussions.udacity.com/c/nd004-p7-linux-based-server-configuration












