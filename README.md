# set-up-Chinook-Database-on-MariaDB-Server
This project provides a step-by-step guide to installing Chinook Database on a MariaDB Server.

The Chinook Database is a sample database widely used for learning, practising SQL, and testing database management tools. It is commonly used in tutorials, technical interviews, and courses that teach SQL querying, database normalisation, and relational database design.


**What Is Inside the Chinook Database?**
The Chinook database mimics a digital media store. It contains data about music, customers, and purchases, structured to reflect real-world business scenarios. 

This is a step-by-step guide to installing the Chinook Database on a MariaDB server.

The Linux commands and SQL statements are highlighted in yellow colour for clarity and effective comprehension.

MariaDB was originally developed as a fork of MySQL, and it shares a high degree of compatibility, including its command-line interface. In many Linux distributions, when you install MariaDB, the command to start the MariaDB shell is still MySQL for compatibility and familiarity, even though we are using MariaDB. However, you can often also use mariadb instead of mysql in the terminal. Both commands typically work interchangeably for MariaDB on most systems.

Step 1: Install MariaDB Server on Linux.
The 1st arrow points to the username agbuenoch, and the 2nd arrow points to the host or the machine DESKTOP-H57G709, the user agbuenoch is currently logged in.

The command
```
sudo apt update
```
is used to run an update on our Ubuntu Linux distro, and this is highly recommended to do from time to time to have updated versions, patches and security features that are released.<br>
**[View step1A](screenshots/step1A)**

The command
```
sudo apt install mariadb-server
```
 will install the MariaDB server on our machine/host. The MariaDB server is a Relational Database Management System (RDBMS) that will host our Chinook database. You will be notified of the storage space to be used as pointed to by 1st arrow. If you wish to continue, enter yes, i.e. “y” as pointed to by 2nd arrow. The 3rd arrow points to the download progress in percentage.<br>
 **[View step1B](screenshots/step1B)**

After installing MariaDB, start and enable the MariaDB server. The command
```
sudo systemctl start mariadb
```
will start the MariaDB server. You will be prompted to enter your password to be able to run the specified command and start the server as pointed to by the 1st arrow. For any wrong password you enter, you will be prompted to re-enter the password as pointed to by the 2nd arrow. If successful, you will be redirected to the next prompt as pointed to by the 4th arrow.
>Always remember to “start” the MariaDB server if you previously “stopped” it.
 **[View step1C](screenshots/step1C)**

The command
```
sudo systemctl enable mariadb
```
will enable the MariaDB server. The 1st arrow below points to the successful execution message.

You can stop and disable the MariaDB server by running the command below, respectively.<br>
```
sudo systemctl stop mariadb

udo systemctl disable mariadb
```
 **[View step1D](screenshots/step1D)**

STEP 2: Secure the MariaDB Server.
Run the command 
```
sudo mysql_secure_installation
```
to secure and provide settings for the MariaDB server we installed.

The 1st arrow points to the prompts requesting the root user's (i.e agbuenoch) password. But if you have no password for the root user, just press the Enter key on your keyboard.

The 2nd arrow points to the prompt that says Setting root user password or unix_socket can be used to secure access to the MariaDB server. In the scenario below, I already have a root user password set up, and this is recognised; for this reason, I declined to set up a “unix_socket authentication” by answering no, i.e. “n”. You will be prompted to provide the password before you can log in as a root user to the MariaDB server.

The 3rd arrow points to the prompt asking if I want to change/update my already existing root user password, therefore I answer the prompt question with no, i.e. “n”.  I do not want to change it.<br>
 **[View step2A1](screenshots/step2A1)**

The screenshot below is the continuation of the screenshot immediately above. From the screenshot below:

The 1st arrow points to the prompt asking if we want to remove the default anonymous user that comes preinstalled with the MariaDB server. Because this installation is for a production environment setting, the database administrator will be responsible for creating and adding new users. Let’s answer with yes, i.e. “y” to remove the anonymous user.

The 2nd arrow points to the prompts asking to disallow root login remotely. If we disallow root login remotely, the root user can only log in to the database locally, which is highly recommended for security reasons and will reduce the attack surface. The root user's remote login can be allowed for troubleshooting or other valid reasons so that the root user can log in to the database from any host/machine.

The 3rd arrow points to the prompt asking to remove test database and access to it, and we agreed to remove it by inputting yes, i.e. “y”.

We then agreed to reload the privilege table to affect all the settings, as this is pointed to by the 4th arrow. We got a success message below confirming that our MariaDB server is now secure and can only be accessed by authorised users.<br>
 **[View step2A2](screenshots/step2A2)**
 **[View step2A3](screenshots/step2A3)**

## STEP 3: Download the Chinook Database SQL Script for MySQL.
Download the Chinook_MySql.sql file, as the MariaDB server is compatible with MySQL SQL scripts, using the command wget to download it directly from the command line.

The command wget is followed by the web address URL where the Chinook_MySql.sql file is located. The arrow below points to the download progress and afterwards shows that the file has been saved as shown with the underline in red.<br>
 **[View step3A](screenshots/step3A)**

This is how to get the web address for the “Chinook_MySql.sql”:

Click on the Chinook Database GitHub Repository and follow the screenshot below. Click just once on the file that the green-coloured arrow points to.<br>
 **[View step3B1](screenshots/step3B1)**
 **[View step3B2](screenshots/step3B2)**
 **[View step3B3](screenshots/step3B3)**

At the top right-hand corner, click on Raw.<br>
 **[View step3B4](screenshots/step3B4)**

You will be presented with the Chinook_MySql.sql raw file. Highlight the URL in the web browser address bar as shown below, highlighted in yellow and copy it.<br>
 **[View step3B5](screenshots/step3B5)**

You will be presented with the Chinook_MySql.sql raw file. Highlight the URL in the web browser address bar as shown below, highlighted in yellow and copy it.

Minimize image
Edit image
Delete image


Paste the URL immediately after the wget command on the Linux console, as illustrated above.

## STEP 4: Log in to MariaDB.
When prompted for a password, enter your root password. If it was the unix_socket authentication you chose, provide the required details as expected.

The command 
```
sudo mariadb

or

sudo mariadb -u root -p
```
can be used to log in to the MariaDB server. Because we previously secured the database, you are prompted to enter a password as pointed to by the 1st arrow. If the authentication is successful, you will be granted access to the MariaDB server as pointed to by the 2nd and 3rd arrows. The 2nd arrow points to the Relational Database Management System (RDBMS) we are using, which is MariaDB and the 3rd arrow points to the current Database residing in the MariaDB server, at this stage no database has been mounted on the MariaDB server, which is why you see the [(none)].
 **[View step4A](screenshots/step4A)**

## STEP 5: Create a new Database for Chinook (OPTIONAL).
Create a new database called Chinook. Then switch to the new database Chinook, by so doing, the [(none)] will be replaced by Chinook. Make sure the new database name we are creating matches the exact name of the database found in the Chinook_MySql.sql file.

Let’s take a look at the file and have a look at what I mean. From this screenshot, click on the file pointed by the green arrow below.
 **[View step5A](screenshots/step5A)**

The 1st arrow points to the SQL statement 
```
DROP DATABASE IF EXISTS `Chinook`;
```
This will replace and overwrite any existing database with the exact database name Chinook when we upload the SQL file to our MariaDB server. But note that this SQL statement is CONDITIONAL, it will only run if there is a database named Chinook found in the MariaDB server; otherwise, it will not execute but jump to the next line of the statement. Therefore,  the Chinook database we will create will be replaced or dropped as a result of this line of SQL statement. In essence, the Chinook database in the Chinook_MySql.sql file will replace the empty Chinook database we are going to create.

The 2nd arrow points to 
```
CREATE DATABASE `Chinook`
```
If the CONDITIONAL SQL statement above did not execute, a new database Chinook will be created.

The 3rd arrow points to 
```
CREATE TABLE `Album`
```
This statement will create a new table called Album and populate the table with values as specified inside the parentheses ( … ). When you scroll down, you will see more of the other statements that will build the Chinook database for us.<br>
 **[View step5B](screenshots/step5B)**

Before creating the Chinook database and loading the Chinook_MySql.sql file, we run the statement 
```
SHOW DATABASES;
```
to view the current databases in the MariaDB server. The 1st arrow points to the Database column, and within the column is the list of preinstalled databases that come with the MariaDB server, which hold important files and configuration settings.
 **[View step5C](screenshots/step5C)**

The command
```
CREATE DATABASE Chinook;
```
will create a new database, Chinook. The database was created successfully, and we got the message Query OK as pointed to by the 1st arrow. If we execute the 
```
SHOW DATABASES;
```
again, we can now see the newly created database Chinook in the MariaDB server as pointed to by the 2nd arrow.

Mount the Chinook database by executing 
```
USE Chinook;
```
If successfully mounted, we got the message Database changed, i.e. from [(none)] to Chinook as pointed to by the 3rd arrow. View the tables in the Chinook database by executing 
```
SHOW TABLES;
```
Note that the Chinook database we created is empty; it has no tables. This is why when we execute SHOW TABLES; we get the message Empty set (0.001 sec) as pointed to by the 4th arrow. We will later upload the Chinook_MySql.sql file to the Chinook database and populate the Chinook database with tables and values in the next step below.<br>
 **[View step5D](screenshots/step5D)**

## STEP 6: Load the Chinook SQL Script into MariaDB.
We need to exit the database first before loading the Chinook_MySql.sql file to the MariaDB server. The command `EXIT`; will log you out of the MariaDB server. The 1st arrow points that we are logged out, i.e. Bye. The 2nd and 3rd arrows point to the username and hostname, respectively. The 4th arrows point to the $ symbol, which connotes a regular user where whereas the # symbol connotes a root user.
 **[View step6A](screenshots/step6A)**
 
Load the Chinook_MySql.sql file we downloaded above. First log in to the MariaDB using 
```
sudo mariadb;
```

The command :
```
sudo mariadb -u root -p Chinook < Chinook_MySql.sql
```
will upload the file to the Chinook database we created above. But note that the empty Chinook database we created will be dropped and replaced by the database named Chinook specified inside the Chinook_MySql.sql file. As pointed to by the 1st arrow, you are prompted to enter the root user password for the sudo privilege; meanwhile, the 2nd arrow points to the prompt requesting the root user password for the MariaDB server. Remember from above that a root user password was recognised when I wanted to secure access to the MariaDB Server, and I chose to use the root user password over unix_socket authentication. Therefore, because I am logging into the MariaDB server as a root user, this means I will enter the same password for the root user.

The 3rd arrow points to the command SHOW DATABASE, which will list all databases within the MariaDB server as pointed to by the 4th arrow. The Chinook database is the database we created earlier, which is now replaced with the Chinook database created in the Chinook_MySql.sql file. 

information_schema, mysql, performance_schema and sys are all default databases that come pre-installed with the MariaDB server. They contain important files and configurations like `user privileges` related to the MariaDB server.
 **[View step6B](screenshots/step6B)**

We can skip `STEP 5` and continue from `STEP 6`. We will still achieve the same result, this is because when we load the Chinook_MySql.sql file, it will automatically create the new database Chinook with all the tables inside. On this premise, below is how to load the Chinook_MySql.sql file if you decided to skip the step of creating the Chinook database yourself.

The command 
```
sudo mariadb -u -p < Chinook_MySql.sql
```
will load the SQL script and will automatically create a database named Chinook. Notice that we did NOT insert or pass a database name before the less-than symbol <. The next arrow on the screenshot below shows that the Chinook database has been created automatically as a result of uploading the SQL script Chinook_MySql.sql file.
 **[View step6C](screenshots/step6C)**

## STEP 7: Verify the Installation.
After showing the databases, mount the Chinook database into the MariaDB server to start querying it.

The command 
```
USE Chinook;
```
will mount the Chinook database. The database has been changed as pointed to by the 1st arrow.

The command 
```
SHOW TABLES;
```
will list tables in the Chinook database we just mounted. The 2nd arrow points to the column named Tables_in_Chinook. The 3rd arrow points to the names of the tables inside the Chinook database, like Album, Artist and Track, among others.<br>
 **[View step7A](screenshots/step7A)**

Notice that the SQL statement SHOW TABLE now displays the list of tables in the Chinook database, meanwhile, before the Chinook_MySql.sql file was uploaded into the Chinook database we created, no tables were inside the Chinook database as shown above In step 5, the last screenshot pointed out by the 4th arrow, which reads Empty set (0.001 sec).

Run the following SQL statement for each of the tables inside the Chinook database to view the columns in each table.
```
SELECT * FROM <The table name>.
```
For example:
```
SELECT * FROM Album;
```

## STEP 8: Stop and Disable the Database:
We can stop the MariaDB server and prevent it from starting automatically on subsequent system boots. This implies that we must start the server each time we boot our local device. Let’s exit back to the Linux console and run the commands shown below.

The command 
```
sudo systemctl stop mariadb
```
will stop the MariaDB server, while the command 
```
sudo systemctl disable mariadb
```
will disable the server. You can check the status of the server by executing 
```
sudo systemctl status mariadb
```
 **[View step8A](screenshots/step8A)**

You must restart the database again before you can access and query it, as demonstrated at the beginning of the article. Let’s see what happens when you attempt to access the database without starting it.

As pointed out by the 2nd arrow, you will get an error because the server was stopped, as shown in the screenshot above. Therefore, you will have to start the server before accessing it.<br>
 **[View step8B](screenshots/step8B)**

 The command 

sudo systemctl start mariadb
 will start the server, hence when we run sudo mariadb, we can access it as pointed to by the 1st arrow.<br>
 **[View step8C](screenshots/step8C)**

## Summary:
This setup provides a complete local environment for practising SQL on the Chinook database using a MariaDB server and Linux Bash.

## LinkedIn Article.
- [How to set up “Chinook Database” on MariaDB Server using Linux Bash]()<br>

## Connect with me.
[🔗 LinkedIn](https://www.linkedin.com/in/agbuenoch)<br>
[🔗 X](https://www.x.com/agbuenoch)
