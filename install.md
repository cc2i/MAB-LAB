Requirements
HTTP server
PHP 5
MySQL database
Installation
Get the last version from GitHub here. Then extract zip file onto your Web server using FTP client or any provider upload tool.


Configuration file

Open the file /path/to/mab-lab/includes/config.php with your favorite editor and update the database parameters described below :

db.host
The hostname of the MySQL server. Possible values are:
'hostname', e.g., localhost or mydb.test.org
'IP address', e.g., 127.0.0.1 or 192.168.10.1
db.name
The database name.
db.user
The username used to connect to the database.
db.pwd
The password associated with the username.
You can change the table prefix but don't forget to update the SQL install script.


SQL install script

The script is located at /path/to/mab-lab/install/db-install.sql. You can copy/paste the content or use the file directly, as your convenience.


This script will create the tables and insert the first user. You may want to update the user name and or password at the end of the file. And if you changed the table prefix you must update the table names


Installation script

To finialize the database installation run the following PHP script: /path/to/mab-lab/install/db-install.php.

Display custom data
Follow this part if you send custom data from you application to the backend.


To show your custom data the only thing to do is to implement the format method from the CustomDataFormatter class. You wil find it at /path/to/mab-lab/includes/customdataformatter.php


A first step would be to output the $data content like that

  public static function format($data) {

     return print_r($data, true);
 }
A new tab will be displayed under the report details view if CustomDataFormatter::format() return a not null or not empty string.

Configure your app

MAB-LAB support GET, POST and PUT method. We chose to use the third and then the most tested by us.


 @ReportsCrashes (
formKey = "", // This is required for backward compatibility but not used
formUri = "http://your-web-server/path/to/mab-lab/report/report.php",
httpMethod = org.acra.sender.HttpSender.Method.PUT,
reportType = org.acra.sender.HttpSender.Type.JSON,
...
HTTP basic authentication

Depending on you server configuration, PHP method may not working. That the reason why you can use the htaccess/htpasswd method.

PHP Method

First of all, go to the settings tab and check the Enable HTTP basic auth checkbox. Then set your login and password.

You can choose to use obfuscated password. In this case, type the clear password under MAB-LAB settings and under you application, use the obfuscated password.




For the example above, your application configuration should look like that :


 @ReportsCrashes (
formKey = "", // This is required for backward compatibility but not used
formUri = "http://your-web-server/path/to/mab-lab/report/report.php",
httpMethod = org.acra.sender.HttpSender.Method.PUT,
reportType = org.acra.sender.HttpSender.Type.JSON,
formUriBasicAuthLogin = "testlogin",
formUriBasicAuthPassword = "5f4dcc3b5aa765d61d8327deb882cf99",
...
Htaccess/htpasswd method

How to is coming soon...

Update MABL
Backup your data
Edit the configuration file /includes/config.php from the new release
Upload new files on your server
Launch script file at /install/update-to-VERSION_CODE/update.php
Remove install directory
Current version code is 9.
