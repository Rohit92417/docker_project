Introduction:-
WordPress is one of the most popular content management software (CMS) due to its multitude of features and ease of use. However, setting up a new web host environment can be time-consuming especially if you need to do it often. Simplifying the installation process to a few fast commands greatly reduce the time and effort required, this is where Docker comes in. Installing WordPress with Docker is a breeze, read ahead to find out more.

Running WordPress And MySQL On Docker Containers
Download Images
To get started, I’ll download the official WordPress and MYSQL Container Images using the lines below.
docker pull wordpress
docker pull mysql
docker images

Create a MySQL Database Container
docker run --name mysql01 -e MYSQL_ROOT_PASSWORD=Password1234 -d mysql

Create WordPress Container
docker run --name wordpress01 --link mysql01 -p 8080:80 -e WORDPRESS_DB_HOST=mysql01:3306 -e WORDPRESS_DB_USER=root -e WORDPRESS_DB_PASSWORD=Password1234 -e WORDPRESS_DB_NAME=wordpress -e WORDPRESS_TABLE_PREFIX=wp_ -d wordpress

Start WordPress
http://hostipaddrsss:8080
