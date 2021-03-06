# proman
# Project Title

Proman API serves backend needs for project management application used to manage projects, members and tasks. It has been built on Spring platform using spring-boot framework.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

You need following softwares before running this application.

1. Java 8 SDK
2. Apache Maven 3.3+ build tool
3. Postgresql version 9.6+
4. Popular IDEs such as Intellij/Eclipse (optional)
5. Postman Client for REST APIs testing (optional)

### Installing and Deployment

A step by step guide that helps you get a development env running

1. Checkout https://github.com/rahul10-pu/proman.git
2. Go to the folder where the above project has been checked out
3. Ensure to change the password of postgres.
   - Run `sudo -iu postgres` command
   - Run `psql` in postgres user shell
   - Alter default password by running `ALTER USER postgres WITH ENCRYPTED PASSWORD 'postgres@123'`;
   - Confirm the password by entering the command in user shell `postgres=# \password`

    ```
    Note: If you wish not to change the default password of postgres, then change the password in the following application
    configuration
   1. datasource.password in proman-api/src/main/resources/application.yaml
   2. database.password in proman-db/src/main/config/localhost.properties
   ```
4. Build the project using `mvn clean install -DskipTests`. First time build will consume time as it downloads all dependencies.
5. Go to `proman-db` module and build the project using maven command `mvn install -Psetup,seed,test-data` to setup the database schema called proman, tables, privileges, seed data such as groups, roles and permissions.
Following are the predefined roles:
   - Administrator (101)
   - Project Manager (102)
   - Architect (103)
   - Team Leader (104)
   - Team Member (105) - All signed up users are assigned with this role by default

    ```
    Note: test-data profile is optional but this will setup an admin user with username as admin@proman.io and default password as proman@123
    ```

6. After the db setup, go to `proman-api` module and then run command `mvn spring-boot:run`. If everything is fine, then API backend
application should be up and running on 8080 using the context `api`

    ```
    2018-06-16 16:42:53.806 - [INFO ] - o.s.b.w.e.tomcat.TomcatWebServer - Tomcat started on port(s): 8080 (http) with context path '/api'
    ```

7. Access the following healthcheck url `http://localhost:8080/api/actuator/health` that should result in following
output

    ```
    {
        "status": "UP"
    }
    ```

8. Try accessing implemented API endpoints using swagger-ui, a plugin configured in the application.
Open `http://localhost:8080/api/swagger-ui.html` in a browser and you should see all API endpoint implementation.

> Best wishes!
