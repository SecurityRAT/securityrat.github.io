---
title: Development Deployment
#keywords: sample
summary: "This setup is recommended if you want to customize or further develop the SecurityRAT tool."
sidebar: home_sidebar
permalink: depl_development.html
#simple_map: true
#map_name: usermap
#box_number: 1
folder: product2
---



## Prerequisities

* As this project is originally based on [JHipster](http://jhipster.github.io/), lot of prerequisities are common with this project. The following are necessary:

  * JAVA 11 (JDK)
  * [Maven](https://maven.apache.org/)
  * [Npm](https://www.npmjs.com)
  * [Bower](http://bower.io/)
  * [Grunt](http://gruntjs.com/)
  * [Maria Database](https://mariadb.org/)

## Before starting the application :

* checkout this project
* log into your mariadb server and create an empty database for this application
* edit the database in the file `securityrat-backend/src/main/resources/config/application-dev.yml` according to the examples

  ```yaml
  databaseName: $YourDatabase
  username: $DBUserName
  password: $DBUserPassword
  ```

* edit the authentication type and CAS configurarion in the file `securityrat-backend/src/main/resources/config/application.yml`.

  ```yaml
  authentication:
    type: FORM
  ```

* configure the Mail server in the file `securityrat-backend/src/main/resources/config/application-dev.yml`

  ```yaml
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

## How to run

* if you are going to run SecurityRAT and the CAS server on the same machine at least 6GB of RAM are recommended.
* Run `mvn install` from the project root directory to bundle the frontend and API components. This is needed to start the tool.
* Move to the folder **securityrat-backend** and run `mvn spring-boot:run`. This will automatically create the database structure if it doesnt exist yet.
* log in to your mariadb server and in the `JHI_USER` table rename the `admin` user login to your CAS username **OR** log in with the credentials `admin` for the username and password (in order to get full rights for your user).
* go to https://localhost:9000. You should be verified by your previously setup CAS server *OR* FORM login and can start using the application.
* The constants (under Administration -> constants) must be edited accordingly.
{% include links.html %}
