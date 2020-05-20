Introduction
Drupal is a content management system (CMS) written in PHP and distributed under the open-source GNU General Public License. People and organizations around the world use Drupal to power government sites, personal blogs, businesses, and more. What makes Drupal unique from other CMS frameworks is its growing community and a set of features that include secure processes, reliable performance, modularity, and flexibility to adapt.
we will install Drupal using Docker Compose so that we can take advantage of containerization and deploy our Drupal website on servers. We will be running containers for a MySQL database, Nginx webserver, and Drupal. We will also secure our installation by obtaining TLS/SSL certificates with Let’s Encrypt for the domain we want to associate with our site. Finally, we will set up a cron job to renew our certificates so that our domain remains secure.

=> Running Drupal in Docker for the first time
Here is how I started mysql
" docker run --name drupal-mysql -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=drupal -e MYSQL_USER=drupal -e MYSQL_PASSWORD=drupal -d mysql:5.5 "

Here is how I started drupal
" docker run --name drupal-test -p 8080:80 --link drupal-mysql:mysql -d drupal "

=>Installation Drupal with Docker and connect mysql database
Step 1 — Defining the Web Server Configuration
$mkdir drupal 
$cd drupal
$mkdir nginx-conf
$nano nginx-conf/nginx.conf

Step 2 - Defining Environment Variables
MYSQL_ROOT_PASSWORD=root_password
MYSQL_DATABASE=drupal
MYSQL_USER=drupal_database_user
MYSQL_PASSWORD=drupal_database_password

Step 3 Defining Services with Docker Compose
Create a docker-compose.yml file:
$nano docker-compose.yml
Add Mysql database

Step 4 — Obtaining SSL Certificates and Credentials
$docker-compose up -d
Check the status of the services using the " $docker-compose ps " command:

Deploying MySQL with Docker

" docker run --name MYSQL-NAME -e MYSQL_ROOT_PASSWORD=MYSQL-PASSWORD -d mysql:latest "

Deploying and Configuring Drupal with Docker
1. Run the following command. Replace "DRUPAL-NAME" with a name for your Drupal container. Replace "MYSQL-NAME" and "MYSQL-PASSWORD" with the values you used for your MySQL Docker container in the previous section.

" docker run --name DRUPAL-NAME --link MYSQL-NAME:mysql -p 8080:80 -e MYSQL_USER=root -e MYSQL_PASSWORD=MYSQL-PASSWORD -d drupal "

2. Go to http://YOUR.VPS.IP:8080/ in your web browser. Replace "YOUR.VPS.IP" with the IP address of your virtual server.

3. When you reach Set up database, click ADVANCED OPTIONS.
4. In the ADVANCED OPTIONS section, for Database name, enter "drupal ]
5. For Database username, enter "root".
6. For Database host, enter the value of MYSQL-NAME for your MySQL container.
7. For Database password, enter the value of MYSQL-PASSWORD for your MySQL container.
8. Continue with the Drupal setup.
