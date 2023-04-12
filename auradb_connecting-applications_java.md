<div>

<div>

# Java

</div>

<div>

## Prerequisites

<div>

<div>

-   Java 17+

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
<p>The Java Driver 5.x series requires Java 17+ and the Java Driver 4.4 LTS requires Java 1.8+. This example uses the Java Driver 5.x series.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

</div>

</div>

<div>

## Installation

<div>

<div>

Download the latest version of the Neo4j Java Driver along with the
compatible version of Reactive Streams into your working directory.

</div>

<div>

To download the latest version of the Neo4j Java Driver:

</div>

<div>

1.  Navigate to the Neo4j Java Driver page of Maven Central.

2.  Select the latest version at the top of the list.

3.  Select **Downloads** from the top right of the page and then select
    **jar** to download the jar file.

</div>

<div>

To download the compatible version of Reactive Streams:

</div>

<div>

1.  Navigate to the Neo4j Java Driver Parent page of Maven Central.

2.  Select the same version as the downloaded driver.

3.  Find the `reactive-streams` version in the pom.xml file on the left
    side of the page.

4.  Navigate to the Reactive Streams page of Maven Central.

5.  Select the same version as the one present in the pom.xml file
    previously.

6.  Select **Downloads** from the top right of the page and then select
    **jar** to download the jar file.

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

    import org.neo4j.driver.AuthTokens;
    import org.neo4j.driver.Config;
    import org.neo4j.driver.Driver;
    import org.neo4j.driver.GraphDatabase;
    import org.neo4j.driver.Query;
    import org.neo4j.driver.SessionConfig;
    import org.neo4j.driver.exceptions.Neo4jException;

    import java.util.Map;
    import java.util.logging.Level;
    import java.util.logging.Logger;

    public class DriverIntroductionExample implements AutoCloseable {
        private static final Logger LOGGER = Logger.getLogger(DriverIntroductionExample.class.getName());
        private final Driver driver;

        public DriverIntroductionExample(String uri, String user, String password, Config config) {
            // The driver is a long living object and should be opened during the start of your application
            driver = GraphDatabase.driver(uri, AuthTokens.basic(user, password), config);
        }

        @Override
        public void close() {
            // The driver object should be closed before the application ends.
            driver.close();
        }

        public void createFriendship(final String person1Name, final String person2Name) {
            // To learn more about the Cypher syntax, see https://neo4j.com/docs/cypher-manual/current/
            // The Reference Card is also a good resource for keywords https://neo4j.com/docs/cypher-refcard/current/
            var query = new Query(
                    """
                    CREATE (p1:Person { name: $person1_name })
                    CREATE (p2:Person { name: $person2_name })
                    CREATE (p1)-[:KNOWS]->(p2)
                    RETURN p1, p2
                    """,
                    Map.of("person1_name", person1Name, "person2_name", person2Name));

            try (var session = driver.session(SessionConfig.forDatabase("neo4j"))) {
                // Write transactions allow the driver to handle retries and transient errors
                var record = session.executeWrite(tx -> tx.run(query).single());
                System.out.printf(
                        "Created friendship between: %s, %s%n",
                        record.get("p1").get("name").asString(),
                        record.get("p2").get("name").asString());
                // You should capture any errors along with the query and data for traceability
            } catch (Neo4jException ex) {
                LOGGER.log(Level.SEVERE, query + " raised an exception", ex);
                throw ex;
            }
        }

        public void findPerson(final String personName) {
            var query = new Query(
                    """
                    MATCH (p:Person)
                    WHERE p.name = $person_name
                    RETURN p.name AS name
                    """,
                    Map.of("person_name", personName));

            try (var session = driver.session(SessionConfig.forDatabase("neo4j"))) {
                var record = session.executeRead(tx -> tx.run(query).single());
                System.out.printf("Found person: %s%n", record.get("name").asString());
                // You should capture any errors along with the query and data for traceability
            } catch (Neo4jException ex) {
                LOGGER.log(Level.SEVERE, query + " raised an exception", ex);
                throw ex;
            }
        }

        public static void main(String... args) {
            // Aura queries use an encrypted connection using the "neo4j+s" protocol
            var uri = "neo4j+s://<Bolt url for Neo4j Aura instance>";
            var user = "<Username for Neo4j Aura instance>";
            var password = "<Password for Neo4j Aura instance>";

            try (var app = new DriverIntroductionExample(uri, user, password, Config.defaultConfig())) {
                app.createFriendship("Alice", "David");
                app.findPerson("Alice");
            }
        }
    }View all (69 more lines)

</div>

</div>

<div>

### Running the example

<div>

Follow the steps below to run the example code:

</div>

<div>

1.  Copy and paste the code above into a file named
    `DriverIntroductionExample.java`.

2.  Enter the information for the AuraDB instance you want to connect to
    by replacing:

    <div>

    -   `<Bolt url for Neo4j Aura instance>` with the URI.

    -   `<Username for Neo4j Aura instance>` with the username.

    -   `<Password for Neo4j Aura instance>` with the password.

    </div>

3.  Use the following command to compile the java file, replacing
    `<driver-version>` with your installed driver version:

    <div>

    <div>

    <div>

    <div>

    <div>

    Copied!

    </div>

    </div>

    </div>

        javac -cp neo4j-java-driver-all-<driver-version>.jar DriverIntroductionExample.java

    </div>

    </div>

4.  Use the following command to run the example code, replacing
    `<driver-version>` with your installed driver version and
    `<rs-version>` with your installed Reactive Streams version:

    <div>

    <div>

    <div>

    <div>

    <div>

    Copied!

    </div>

    </div>

    </div>

        java -cp neo4j-java-driver-all-<driver-version>.jar:reactive-streams-<rs-version>.jar:. DriverIntroductionExample

    </div>

    </div>

</div>

</div>

<div>

### Example walkthrough

<div>

The example imports `neo4j.driver` to connect to the Neo4j AuraDB
instance.

</div>

<div>

The `main` function calls the following two functions:

</div>

<div>

-   `createFriendship` creates two \'Person\' nodes, Alice and David,
    and a \'KNOWS\' relationship between them using a write transaction.

-   `findPerson` finds Alice using a read transaction.

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
<p>Developing with Neo4j Aura requires the handling of transient errors and retry management. One of the ways you can meet this requirement is by using <a>Transaction Functions</a>.</p>
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

-   Neo4j Java Driver Documentation

</div>

</div>

</div>

</div>
