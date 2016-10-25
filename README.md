# cloud-9-ubuntu-rails-mysql-notes
These are just notes to try to minimize the head scratching the next time I want to create an application in rails using mysql on cloud9 ubuntu

These are by no means best practices, but rather just the notes of how a total nube got things to work.  By "getting things to work" I mean the behavior was consistent with the Ruby on Rails 5 Essential Training course on Lynda.com

At first I created a Cloud9 workspace by selecting a ruby on rails installation.  That proved to be painful because by default the database used is SQLite rather than MySQL and it used an older version of rails.  I tried to backtrack and change the database.yml file along with other settings but I could never get things to work.  I decided to create a new ubuntu only workspace and then used the folowing site to install rails with MySQL.

https://community.c9.io/t/running-a-rails-app/1615

The most important things I learned here were (1) to specify MYSQL as the database in step 2 when creating a new rails project/app and (2) to specify the environment variables of $PORT and $IP when launching the webserver.

At this point I wasted a great deal of time trying to figure out why I could not even connect to my application via browser.

I would get long server logs and I keyed in on this error:
#<Mysql2::Error: Can\t connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (111)>'

I spent a ridiculous amount of time trying to find these socket files in my rails project, trying to see if mysql was installed and running, etc.

I finally discovered this page on stack overflow that helped me understand why I could not find any of these folders or files in my cloud9 workspace.

http://stackoverflow.com/questions/9863325/where-is-my-database-located-when-using-mysql-in-rails

The below advice from Michael Berkowski turned out to be my golden ticket:

# Connect from the command line
$ mysql -usomeusername -p

# Execute  MySQL commands
mysql> SHOW DATABASES;

Once I ran this I realized that the databases identified in my database.yml file had not been created in my new instance of MySQL.

I then went back to the earlier chapters in the Lynda tutorial to redo the database set ups.

These were the commands I sent through the terminal from the mysql folder:

mysql> CREATE DATABASE example_development;
Query OK, 1 row affected (0.00 sec)

mysql> CREATE DATABASE example_test;                                                                                                                             
Query OK, 1 row affected (0.00 sec)

mysql> GRANT ALL PRIVILEGES ON example_development.* TO 'rails_user'@'localhost' IDENTIFIED BY 'some_password';
Query OK, 0 rows affected (0.00 sec)

mysql> GRANT ALL PRIVILEGES ON example_test.* TO 'rails_user'@'localhost' IDENTIFIED BY 'some_password';                                                       
Query OK, 0 rows affected (0.00 sec)

mysql> exit

I then went back to the database.yml file to ensure the development and test databases shown there had the correct names and to change the default username and password settings to require this user to login for access.





