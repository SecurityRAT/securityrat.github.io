---
title: Production Deployment
#keywords: sample
summary: "Description of steps necessary for taking SecurityRAT into production."
sidebar: home_sidebar
permalink: depl_production.html
#simple_map: true
#map_name: usermap
#box_number: 1
folder: product2
---


## Prerequisities

Before installing SecurityRAT, you have to have the following components installed:

* JAVA 8
* Maven
* MySQL
* (recommended) Apache Web Server serving as a reverse proxy and terminating TLS


## Installation & Configuration:

- download the latest [release](https://github.com/SecurityRAT/SecurityRAT/releases) of SecurityRAT (either as a .zip or a .tar.gz archive)
- unpack the downloaded archive to a desired location
- log into your mysql server and create an empty database for this application
- edit the database in the file `src/main/resources/config/application-prod.yml` according to the examples

```
databaseName: $YourDatabase
username: $DBUserName
password: $DBUserPassword
```

- enable TLS for spring boot if you don't use a separate web server:
   - e.g. generate a self-signed certificate in the root directory of SecurityRAT: `keytool -genkey -alias tomcat -storetype PKCS12 -keyalg RSA -keysize 2048 -keystore keystore.p12 -validity 3650`
   - add the following lines into `application-prod.yml`:
   
```
server:
  ssl:
    key-store: keystore.p12
    key-store-password: $MyPassword
    keyStoreType: PKCS12
    keyAlias: tomcat
```

- edit the authentication type and the Mail server configurarion in the file `src/main/resources/config/application.yml`.

```
authentication:
  type: FORM
	
mail:
  host: localhost # mail server
  port: 25
  username:	#might be needed depending on your mail server
  password:	#might be needed depending on your mail server
  protocol: smtp
  tls: false
  auth: false
  from: securityRAT@localhost # from email address
```

## Running the Application
- switch to your SecurityRAT directory and fire `java -jar securityRAT-${version}.war --spring.profiles.active=prod`
- go to the URL of your server and log in using the default credentials admin/admin
- Edit the constants in the application (under Administration -> constants) to the desired values.

## Notes
- **it is important to change the `admin` password in `prod mode`.**
- it is recommended to use a web server (e.g. [Apache](https://httpd.apache.org/) as a proxy, with a proper TLS configuration set etc).


{% include links.html %}
