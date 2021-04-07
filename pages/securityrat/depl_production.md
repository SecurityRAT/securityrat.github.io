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

* JAVA 11
* Mariadb
* (recommended) Apache Web Server serving as a reverse proxy and terminating TLS

## Installation & Configuration

* Download the latest [release](https://github.com/SecurityRAT/SecurityRAT/releases) of SecurityRAT (securityrat.tar.gz archive).
* Unpack the downloaded archive to a desired location.
* Log into your mariadb server and create an empty database for this application.
* Edit the database in the file `config/application-prod.yml` according to the examples.

  ```yaml
    databaseName: $YourDatabase
    username: $DBUserName
    password: $DBUserPassword
  ```

* Enable TLS for spring boot if you don't use a separate web server:
  * e.g. generate a self-signed certificate in the root directory of SecurityRAT: `keytool -genkey -alias tomcat -storetype PKCS12 -keyalg RSA -keysize 2048 -keystore keystore.p12 -validity 3650`
  * add the following lines into `application-prod.yml`:

  ```yaml
  server:
    ssl:
      key-store: keystore.p12
      key-store-password: $MyPassword
      keyStoreType: PKCS12
      keyAlias: tomcat
  ```

* Edit the authentication type and the Mail server configurarion in the file `config/application.yml`.

  ```yaml
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

* Switch to your SecurityRAT directory and run `java -jar securityrat.jar --spring.profiles.active=prod`.
* Go to the URL of your server and log in using the default credentials **admin/admin**.
* Edit the constants in the application (under Administration -> constants) to the desired values.

## Notes

* **It is important to change the `admin` password in `prod mode`**.
* We recommended using a web server (e.g. [Apache](https://httpd.apache.org/) as a proxy, with a proper TLS configuration set etc).


{% include links.html %}
