# Hello JDBC

I want to kick off the discussion by taking a trip down memory lane. We are going to take a look at an example
application to see how we can use JDBC (Java DataBase Connectivity) to connect to a database in Java and execute queries.

## Running this application

You need to have Docker run and run `docker/docker-compose.yml` by executing the command 

```bash
docker-compose up
```

When you run `docker-compose` the `docker/sql/schema.sql` script will be run and 3 records will be inserted into the 
database. 

Next you can run the main application class located in `src/main/java/org/codemash/Application` from your IDE or by 
running the following Maven command: 

```bash
mvn compile exec:java
```

The main application class will read all of the rows from the `Run` table and print them to standard out: 

```java
PreparedStatement preparedStatement = conn.prepareStatement("select * from run");
ResultSet rs = preparedStatement.executeQuery();

while(rs.next()) {
    String title = rs.getString("title");
    int miles = rs.getInt("miles");
    System.out.println(title + ": " + miles);
}
```

```bash
hello-jdbc on  main [!?] 🚀 mvn compile exec:java
[INFO] Scanning for projects...
[INFO]
[INFO] ----------------------< org.codemash:hello-jdbc >-----------------------
[INFO] Building hello-jdbc 0.1-SNAPSHOT
[INFO] --------------------------------[ jar ]---------------------------------
[INFO]
[INFO] --- maven-resources-plugin:2.6:resources (default-resources) @ hello-jdbc ---
[INFO] Using 'UTF-8' encoding to copy filtered resources.
[INFO] skip non existing resourceDirectory /Users/vega/dev/presentations/codemash-2023/hello-jdbc/src/main/resources
[INFO]
[INFO] --- maven-compiler-plugin:3.1:compile (default-compile) @ hello-jdbc ---
[INFO] Nothing to compile - all classes are up to date
[INFO]
[INFO] --- exec-maven-plugin:3.0.0:java (default-cli) @ hello-jdbc ---
Monday Morning Run: 3
Wednesday Afternoon Run: 5
Saturday Morning Run: 8
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  0.821 s
[INFO] Finished at: 2022-12-21T15:53:48-05:00
[INFO] ------------------------------------------------------------------------
```
