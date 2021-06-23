## I can't make Spring Boot 2 just-work out-of-the-box.

Now you (kind of) can. Have you ever been in a position where a 404 is the happiest thing you've seen all day? This project is for you.

Make sure to write some controllers or add Spring Boot logic to make it a Real Thing.


### Dependencies

- Java 11
- Maven 3.8.1
- A mySQL server (or container) running on port 3306; with a database named `spacedb`; with a user/password configured in `src/main/resources/application.properties` 
(note that you can change the database, port, et. al configuration within the same file)

If you're on Linux/MacOS, the following commands should work to run this out-of-the-box. For Windows, you may need to swap up file paths.

```
mvn clean verify 
mvn dependency:copy-dependencies -DincludeScope="runtime" 
cp target/spaced-0.0.1-SNAPSHOT.jar target/dependency
java -cp "target/dependency/*" org.nerdsofprey.spaced.SpacedApplication
```

If all goes well, you may now browse to localhost:8080 and view the running application.

To sign in, use the "generated security password" visible in the log **of your running application**. The one from this example will (probably) never work.

```
2021-06-23 16:11:58.698  WARN 13662 --- [           main] JpaBaseConfiguration$JpaWebConfiguration : spring.jpa.open-in-view is enabled by default. Therefore, database queries may be performed during view rendering. Explicitly configure spring.jpa.open-in-view to disable this warning
2021-06-23 16:11:58.996  INFO 13662 --- [           main] .s.s.UserDetailsServiceAutoConfiguration :

Using generated security password: 01505461-27c3-4f8c-bedb-00547dcf4912
```

