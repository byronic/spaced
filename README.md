## I can't make Spring Boot 2 just-work out-of-the-box.

Now you (kind of) can. Have you ever been in a position where a 404 is the happiest thing you've seen all day? This project is for you.

Make sure to write some controllers or add Spring Boot logic to make it a Real Thing.


### Dependencies

- Java 17
- Maven 3.9.2
- A [mariaDB server (or container)](https://hub.docker.com/_/mariadb) running on port 3306; with a database named `spacedb`; with a user/password configured in `src/main/resources/application.properties` 
(note that you can change the database, port, et. al configuration within the same file). If possible, separate the root user and the application user -- 

#### Sidebar: Creating a `mariadb` database

If you have already got a mariadb database server running on port 3306 -- including server, database, user, password, and privileges, skip this step and continue to Running the Application.

Otherwise, you can set up a local database with the following steps (as of mariadb 11.0.2):

```
docker run --detach --name MEMORABLE_CONTAINER_NAME --env MARIADB_USER=someuser --env MARIADB_PASSWORD=password_for_someuser --env MARIADB_ROOT_PASSWORD=password_for_root_user -p 3306:3306 mariadb:11.0.2-jammy
docker exec -it MEMORABLE_CONTAINER_NAME mariadb -u root -p
# you enter the root password set during the docker run command...
```
Then, to complete database creation run the following mariadb commands, replacing `someuser` with the `MARIADB_USER` you created in the prior `docker run` step:

```
CREATE DATABASE spacedb;
GRANT ALL PRIVILEGES on `spacedb`.* TO 'someuser'@'%';
```

### Running the Application

If you're on Linux/MacOS, the following commands should work to run this out-of-the-box. For Windows, you may need to swap up file paths.

```
mvn clean verify 
mvn dependency:copy-dependencies -DincludeScope="runtime" 
cp target/spaced-0.0.1-SNAPSHOT.jar target/dependency
java -cp "target/dependency/*" org.nerdsofprey.spaced.SpacedApplication
```

If all goes well, you may now browse to localhost:8080 and view the running application.

To sign in, use the username 'user' and the generated security password visible in the log **of your running application**. The one from this example will (probably) never work.

```
2021-06-23 16:11:58.698  WARN 13662 --- [           main] JpaBaseConfiguration$JpaWebConfiguration : spring.jpa.open-in-view is enabled by default. Therefore, database queries may be performed during view rendering. Explicitly configure spring.jpa.open-in-view to disable this warning
2021-06-23 16:11:58.996  INFO 13662 --- [           main] .s.s.UserDetailsServiceAutoConfiguration :

Using generated security password: 01505461-27c3-4f8c-bedb-00547dcf4912
```

