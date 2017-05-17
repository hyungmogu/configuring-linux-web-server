# udacity-configuring-linux-web-server
Final project for the course 'Linux Server Configuration'.

## Table of Contents
- Demo
- Dependencies
- Accessing the Application
- Summary of Configuration Changes
- References 

## Demo
- Click [here]('http://item-catalog.hyungmogu.ca') to view application

## Dependencies
### Packages
- Python (v2.7.12)
- Apache2 (v2.4.18)
- PostgreSQL (v9.5.6)
- tcptrack (v.1.4.2)
### Python Libraries
- SQLAlchemy (v1.1.9)
- Flask (v0.12.1)
- httplib2 (v0.10.3)
- psycopg2 (v2.7.1)
- requests (v2.14.2)
- oauth2client (v4.1.0) 

## Server Details
- URL: http://item-catalog.hyungmogu.ca
- IP Address: 54.166.228.141
- Port: 2200

## Summary of Configuration Changes
### ~/.ssh
- Added the public key `LightSail`

### /etc/ssh/sshd_config
- Enabled ssh login only through port 2200
- Disabled password authentication 

### /etc/sudoers.d/
- Added 'grader' to the list of users with root authorization

### /etc/apache2/sites-available/
- Disabled default VirtualHost (000-default.conf)
- Enabled VirtualHost for item catalog (flaskapp.conf)
- Made VirtualHost to accept requests from `item-catalog.hyungmogu.ca`, `54.166.228.141` (flaskapp.conf)
- Made to run the flask app by executing `/var/www/FlaskApp/flaskapp.wsgi` (flaskapp.conf)  
- Allowed the access of `/var/www/FlaskApp/item_catalog/` by all (flaskapp.conf)
- Allowed the access of static directory `/var/www/FlaskApp/item_catalog/static` by all through the address `item-catalog.hyungmogu.ca/static` (flaskapp.conf)

### ufw
- Enabled port for NPT (123)
- Enabled port for SSH (2200)
- Enabled port for HTTP (80)
- Disabled every other ports
- Enabled all ports with outgoing response / requests

### Google Oauth
- Added `item-catalog.hyungmogu.ca` to `Authorized Javascript Origins`  
- Added `item-catalog.hyungmogu.ca/welcome` to `Authorized Redirect URIs`

### Facebook Oauth
- Changed SiteURL to `http://item-catalog.hyungmogu.ca`  
- Added `http://item-catalog.hyungmogu.ca/welcome` to `Valid Oauth Redirect URIs`, and deleted the rest

### Amazon Lightsail
- Added custom tcp port 2200
- Added custom tcp port 123

### Godaddy
- Made the DNS to point the domain name `hyungmogu.ca` and its subdomain `item-catalog.hyungmogu.ca` to `54.166.228.141` 

## References

### Changing ssh Port from 22 to 2200
- https://discussions.udacity.com/t/change-port-from-22-to-2200/32469 

### Configuring Apache2
- https://httpd.apache.org/docs/2.4/configuring.html 
- https://serverfault.com/questions/682282/what-is-the-difference-between-000-default-conf-and-just-default 
- https://httpd.apache.org/docs/2.4/mod/mod_access_compat.html
- https://httpd.apache.org/docs/2.4/vhosts/examples.html

### Running Flask App on Apache2
- https://www.digitalocean.com/community/tutorials/how-to-deploy-a-flask-application-on-an-ubuntu-vps 
- http://flask.pocoo.org/docs/0.12/deploying/mod_wsgi/ 
- http://modwsgi.readthedocs.io/en/develop/configuration-directives/WSGIScriptAlias.html 

### Accessing PostgreSQL Commandline
- http://stackoverflow.com/questions/28213929/psql-fatal-role-does-not-exist 

### Creating a User in PostgreSQL with Superuser Previlege
- https://www.tutorialspoint.com/postgresql/postgresql_privileges.htm
- https://www.postgresql.org/docs/8.0/static/sql-createuser.html 
- https://www.postgresql.org/docs/9.0/static/sql-grant.html

### Resolving Google Oauth's `Permission Denied` Error
- https://stackoverflow.com/questions/36020374/google-permission-denied-to-generate-login-hint-for-target-domain-not-on-localh/43644795 

### Removing Default Apache2 page
- https://pressable.com/blog/2014/12/23/dns-record-types-explained/ 
- http://www.networksolutions.com/support/what-is-a-domain-name-server-dns-and-how-does-it-work/
- http://stackoverflow.com/questions/21812360/what-is-the-difference-between-sites-enabled-and-sites-available-directory 
- https://superuser.com/questions/629683/ping-retrieves-an-ip-from-dns-but-loses-all-packets 
- https://www.digitalocean.com/community/questions/how-do-i-remove-apache2-ubuntu-default-page
- https://www.digitalocean.com/community/tutorials/how-to-set-up-a-host-name-with-digitalocean  

### Monitoring Network Traffic
- https://askubuntu.com/questions/257263/how-to-display-network-traffic-in-terminal 
- https://superuser.com/questions/629683/ping-retrieves-an-ip-from-dns-but-loses-all-packets 


