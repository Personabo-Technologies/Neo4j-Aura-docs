<div>

<div>

# Python

</div>

<div>

## Prerequisites

<div>

<div>

-   Python 3.7 and above

</div>

</div>

</div>

<div>

## Installation

<div>

<div>

Use the following command to install the Neo4j Python Driver using pip:

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

    pip install neo4j

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

    import logging

    from neo4j import GraphDatabase
    from neo4j.exceptions import Neo4jError

    class App:

        def __init__(self, uri, user, password):
            self.driver = GraphDatabase.driver(uri, auth=(user, password))

        def close(self):
            # Don't forget to close the driver connection when you are finished with it
            self.driver.close()

        def create_friendship(self, person1_name, person2_name):
            with self.driver.session(database="neo4j") as session:
                # Write transactions allow the driver to handle retries and transient errors
                result = session.execute_write(
                    self._create_and_return_friendship, person1_name, person2_name)
                for record in result:
                    print("Created friendship between: {p1}, {p2}"
                          .format(p1=record['p1'], p2=record['p2']))

        @staticmethod
        def _create_and_return_friendship(tx, person1_name, person2_name):
            # To learn more about the Cypher syntax, see https://neo4j.com/docs/cypher-manual/current/
            # The Reference Card is also a good resource for keywords https://neo4j.com/docs/cypher-refcard/current/
            query = (
                "CREATE (p1:Person { name: $person1_name }) "
                "CREATE (p2:Person { name: $person2_name }) "
                "CREATE (p1)-[:KNOWS]->(p2) "
                "RETURN p1, p2"
            )
            result = tx.run(query, person1_name=person1_name, person2_name=person2_name)
            try:
                return [{"p1": record["p1"]["name"], "p2": record["p2"]["name"]}
                        for record in result]
            # Capture any errors along with the query and data for traceability
            except Neo4jError as exception:
                logging.error("{query} raised an error: \n {exception}".format(
                    query=query, exception=exception))
                raise

        def find_person(self, person_name):
            with self.driver.session(database="neo4j") as session:
                result = session.execute_read(self._find_and_return_person, person_name)
                for record in result:
                    print("Found person: {record}".format(record=record))

        @staticmethod
        def _find_and_return_person(tx, person_name):
            query = (
                "MATCH (p:Person) "
                "WHERE p.name = $person_name "
                "RETURN p.name AS name"
            )
            result = tx.run(query, person_name=person_name)
            return [record["name"] for record in result]


    if __name__ == "__main__":
        # Aura queries use an encrypted connection using the "neo4j+s" URI scheme
        uri = "neo4j+s://<Bolt url for Neo4j Aura instance>"
        user = "<Username for Neo4j Aura instance>"
        password = "<Password for Neo4j Aura instance>"
        app = App(uri, user, password)
        app.create_friendship("Alice", "David")
        app.find_person("Alice")
        app.close()View all (54 more lines)

</div>

</div>

<div>

### Running the example

<div>

Follow the steps below to run the example code:

</div>

<div>

1.  Copy and paste the code above into a file named `example.py`:

2.  Enter the information for the AuraDB instance you want to connect to
    by replacing:

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

        python example.py

    </div>

    </div>

</div>

</div>

<div>

### Example walkthrough

<div>

The example imports `GraphDatabase` and `basic_auth` to connect to the
Neo4j AuraDB instance and `ServiceUnavailable` for error handling.

</div>

<div>

The `Main` function calls the following two functions:

</div>

<div>

-   `create_friendship` creates two \'Person\' nodes, Alice and David,
    and a \'KNOWS\' relationship between them using a write transaction.

-   `find_person` finds Alice using a read transaction.

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

-   Neo4j Python Driver Documentation

</div>

</div>

</div>

</div>
