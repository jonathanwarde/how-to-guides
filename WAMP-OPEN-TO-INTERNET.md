Opening WAMP sites to the internet (or to specific IPs)


##1. Open CMD type ipconfig

Grab your IP (IPV4 address probably)

##2. For wamp 3 and above

Find \wamp\bin\apache\apache{version}\conf\extra\httpd-vhosts.conf

```
<VirtualHost *:80>
    ServerName localhost
    DocumentRoot c:/wamp/www
    <Directory  "c:/wamp/www/">
        Options +Indexes +FollowSymLinks +MultiViews
        AllowOverride All
        Require local
    </Directory>
</VirtualHost>
```

Edit the above to add...

Require all granted

or

Require local
Require ip 192.168.1  #this for a specific IP

##3. Make sure Firewall isnt blocking wamp apache....

Check if Wamp is published locally if it is, continue;
Access Control Panel
Click "Firewall"
Click "Allow app through firewall"
Click "Allow some app"
Find and choose C:/wamp64/bin/apache2/bin/httpd.exe
Restart Wamp

##4. Emable CORS for wamp

Find C:\wamp\bin\apache\apache2.4.18\conf\httpd.conf

Find section below and add the line "Header set access" etc...

```
<Directory "c:/wamp/www/">
    Options +Indexes +FollowSymLinks
    Header set Access-Control-Allow-Origin "*"
    AllowOverride all
    Require local
</Directory>
```
##5. Also make sure "headers_module" is activated in wamp and restart server

##6. Edit PHP admin db file for wordpress and change options home url from /localhost to whatever your IP is.

Do the same in wp, refresh permalinks.

If you get an issue with "too many redirects", add following to wp-config (IP is local IP):

```
define('WP_HOME','http://155.198.109.209/events');
define('WP_SITEURL','http://155.198.109.209/events');
```