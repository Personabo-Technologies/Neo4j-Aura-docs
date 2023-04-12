<div>

<div>

# Spring Boot

</div>

<div>

## Prerequisites

<div>

<div>

-   Java 1.8+

-   Maven/Gradle

</div>

</div>

</div>

<div>

## Maven project setup

<div>

<div>

Create a Spring boot application to use the example provided below. To
do this, define the necessary dependencies and the project layout in
Maven or Gradle. This example focuses on the Maven-based solution.

</div>

<div>

Your `pom.xml` file should match the following:

</div>

<div>

<div>

<div>

<div>

<div>

Copied!

</div>

</div>

</div>

    <?xml version="1.0" encoding="UTF-8"?>
    <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
             xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
        <modelVersion>4.0.0</modelVersion>

        <parent>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-parent</artifactId>
            <version>2.6.4</version>
            <relativePath/> <!-- lookup parent from repository -->
        </parent>
        <groupId>com.neo4j.examples</groupId>
        <artifactId>spring-boot-read-write-transactions</artifactId>
        <version>0.0.1-SNAPSHOT</version>
        <packaging>jar</packaging>

        <name>Neo4j Spring Boot Example</name>
        <description>Example showing how to use Spring Boot and do write and read transactions</description>

        <properties>
            <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
            <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
            <java.version>11</java.version>
        </properties>

        <dependencies>
            <dependency>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-starter</artifactId>
            </dependency>
            <dependency>
                <groupId>org.neo4j.driver</groupId>
                <artifactId>neo4j-java-driver</artifactId>
            </dependency>
        </dependencies>

        <build>
            <plugins>
                <plugin>
                    <groupId>org.springframework.boot</groupId>
                    <artifactId>spring-boot-maven-plugin</artifactId>
                </plugin>
            </plugins>
        </build>
    </project>View all (30 more lines)

</div>

</div>

</div>

</div>

<div>

## Code example

<div>

<div>

<div>

<div>

<div>

<div>

Copied!

</div>

</div>

</div>

    package org.neo4j.examples;

    import java.util.Collections;
    import java.util.HashMap;
    import java.util.List;
    import java.util.Map;

    import org.neo4j.driver.Driver;
    import org.neo4j.driver.Record;
    import org.neo4j.driver.Result;
    import org.neo4j.driver.Session;
    import org.neo4j.driver.SessionConfig;
    import org.neo4j.driver.TransactionWork;
    import org.neo4j.driver.exceptions.Neo4jException;
    import org.slf4j.Logger;
    import org.slf4j.LoggerFactory;
    import org.springframework.boot.CommandLineRunner;
    import org.springframework.boot.SpringApplication;
    import org.springframework.boot.autoconfigure.SpringBootApplication;
    import org.springframework.context.ConfigurableApplicationContext;
    import org.springframework.stereotype.Component;


    @SpringBootApplication
    public class Example {

        public static void main(String[] args) {
            SpringApplication.run(Example.class, args);
        }

    }

    @Component
    class ExampleCommandLineRunner implements CommandLineRunner {
        private static final Logger LOGGER = LoggerFactory.getLogger(ExampleCommandLineRunner.class.getName());

        private final Driver driver;

        private final ConfigurableApplicationContext applicationContext;

        // Autowire the Driver bean by constructor injection
        public ExampleCommandLineRunner(Driver driver, ConfigurableApplicationContext applicationContext) {
            this.driver = driver;
            this.applicationContext = applicationContext;
        }

        @Override
        public void run(String... args) throws Exception {
            try (Session session = driver.session(SessionConfig.forDatabase("neo4j"))) {
                // Using transaction functions allows the driver to handle retries and transient errors for you

                // The first examples indicates a write transaction that must go through the leader of a cluster
                Record peopleCreated = session.writeTransaction(createRelationshipToPeople("Alice", "David"));
                System.out.println("Create successful: " + peopleCreated.get("p1") + ", " + peopleCreated.get("p2"));

                // The second examples indicates a read transaction, that can be answered by a follower
                session
                    .readTransaction(readPersonByName("Alice"))
                    .forEach(System.out::println);
            }

            // Shutdown the application context to simulate application end.
            // This closes all managed beans as well. The driver is one of those and its resources will be released.
            applicationContext.close();
        }

        private static TransactionWork<Record> createRelationshipToPeople(String person1, String person2) {

            return tx -> {
                // To learn more about the Cypher syntax, see https://neo4j.com/docs/cypher-manual/current/
                // The Reference Card is also a good resource for keywords https://neo4j.com/docs/cypher-refcard/current/

                String createRelationshipToPeopleQuery = "MERGE (p1:Person { name: $person1_name }) \n" +
                    "MERGE (p2:Person { name: $person2_name })\n" +
                    "MERGE (p1)-[:KNOWS]->(p2)\n" +
                    "RETURN p1, p2";

                Map<String, Object> params = new HashMap<>();
                params.put("person1_name", person1);
                params.put("person2_name", person2);

                try {
                    Result result = tx.run(createRelationshipToPeopleQuery, params);
                    // You should not return the result itself outside of the scope of the transaction.
                    // The result will be closed when the transaction closes and it won't be usable afterwards.
                    // As we know that the query can only return one row, we can use the single method of the Result and
                    // return the record.
                    return result.single();

                    // You should capture any errors along with the query and data for traceability
                } catch (Neo4jException ex) {
                    LOGGER.error(createRelationshipToPeopleQuery + " raised an exception", ex);
                    throw ex;
                }
            };
        }

        private static TransactionWork<List<String>> readPersonByName(String name) {

            return tx -> {
                String readPersonByNameQuery = "MATCH (p:Person)\n" +
                    "    WHERE p.name = $person_name\n" +
                    "    RETURN p.name AS name";

                Map<String, Object> params = Collections.singletonMap("person_name", name);

                try {
                    Result result = tx.run(readPersonByNameQuery, params);
                    return result.list(row -> row.get("name").asString());
                } catch (Neo4jException ex) {
                    LOGGER.error(readPersonByNameQuery + " raised an exception", ex);
                    throw ex;
                }
            };
        }

    }View all (102 more lines)

</div>

</div>

<div>

### Running the example

<div>

Follow the steps below to run the example code:

</div>

<div>

1.  Copy and paste the code above into a file named `Example.java`
    within a package/folder like `org.neo4j.examples` in the
    `main/java/src` folder.

2.  Enter the information for the AuraDB instance you want to connect to
    by adding the following to the `application.properties` file:

    <div>

    <div>

    <div>

    <div>

    <div>

    Copied!

    </div>

    </div>

    </div>

        spring.neo4j.uri=neo4j+s://<Bolt url for Neo4j Aura instance>
        spring.neo4j.authentication.username=<Username for Neo4j Aura instance>
        spring.neo4j.authentication.password=<Password for Neo4j Aura instance>

    </div>

    </div>

    <div>

    and replace:

    </div>

    <div>

    -   `<Bolt url for Neo4j Aura instance>` with the URI.

    -   `<Username for Neo4j Aura instance>` with the username.

    -   `<Password for Neo4j Aura instance>` with the password.

    </div>

3.  Use the following command to run the example code:

    <div>

    <div>

    <div>

    <div>

    <div>

    Copied!

    </div>

    </div>

    </div>

        ./mvnw spring-boot:run

    </div>

    </div>

</div>

</div>

<div>

### Example walkthrough

<div>

This example creates an `ExampleCommandLineRunner`, an implementation of
Spring's `CommandLineRunner`. This bean's run method executes after the
Spring context is successfully created.

</div>

<div>

There are two methods called from the implemented run method:

</div>

<div>

-   `createRelationshipToPeople` creates two \'Person\' nodes, Alice and
    David, and a \'KNOWS\' relationship between them using a write
    transaction.

-   `readPersonByName` finds Alice using a read transaction.

</div>

<div>

<div>

<table>
<tbody><tr>
<td>
<i></i>
</td>
<td>
<div>
<p>Developing with Neo4j Aura requires the use of <a>Transaction Functions</a>. Transaction Functions enable automatic recovery from transient network errors and enable load balancing.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

Make sure to log queries and data sent from your application as it is
useful when you encounter errors and can help with debugging.

</div>

</div>

</div>

</div>

<div>

## References

<div>

<div>

-   Spring Data Neo4j Documentation

</div>

</div>

</div>

</div>
