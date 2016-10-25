# cloud-9-ubuntu-rails-mysql-notes
These are just notes to try to minimize the head scratching the next time I want to create an application in rails using mysql on cloud9 ubuntu

These are by no means best practices, but rather just the notes of how a total nube got things to work.  By "getting things to work" I mean the behavior was consistent with the Ruby on Rails 5 Essential Training course on Lynda.com

At first I created a Cloud9 workspace by selecting a ruby on rails installation.  That proved to be painful because by default the database used is SQLite rather than MySQL and it used an older version of rails.  I tried to backtrack and change the database.yml file along with other settings but I could never get things to work.  I decided to create a new ubuntu only workspace and then used the folowing site to install rails with MySQL.

https://community.c9.io/t/running-a-rails-app/1615

At this point I wasted a great deal of time trying to figure out why I could not even connect to my application via browser.

I would get server log errors like:
#<Mysql2::Error: Can't connect to local MySQL server through socket '/var/run/mysqld/mysqld.sock' (111)>
