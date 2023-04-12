<div>

<div>

# JavaScript

</div>

<div>

## Prerequisites

<div>

<div>

-   Node.js

-   npm/yarn

</div>

</div>

</div>

<div>

## Installation

<div>

<div>

Use the following command to install the Neo4j JavaScript Driver using
npm:

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

    npm install neo4j-driver

</div>

</div>

<div>

Use the following command to install the Neo4j JavaScript Driver using
yarn:

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

    yarn add neo4j-driver

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

    (async() => {
        const neo4j = require('neo4j-driver');

        const uri = 'neo4j+s://<Bolt url for Neo4j Aura instance>';
        const user = '<Username for Neo4j Aura instance>';
        const password = '<Password for Neo4j Aura instance>';

        // To learn more about the driver: https://neo4j.com/docs/javascript-manual/current/client-applications/#js-driver-driver-object
        const driver = neo4j.driver(uri, neo4j.auth.basic(user, password));

        try {
            const person1Name = 'Alice';
            const person2Name = 'David';

            await createFriendship(driver, person1Name, person2Name);

            await findPerson(driver, person1Name);
            await findPerson(driver, person2Name);
        } catch (error) {
            console.error(`Something went wrong: ${error}`);
        } finally {
            // Don't forget to close the driver connection when you're finished with it.
            await driver.close();
        }

        async function createFriendship (driver, person1Name, person2Name) {

            // To learn more about sessions: https://neo4j.com/docs/javascript-manual/current/session-api/
            const session = driver.session({ database: 'neo4j' });

            try {
                // To learn more about the Cypher syntax, see: https://neo4j.com/docs/cypher-manual/current/
                // The Reference Card is also a good resource for keywords: https://neo4j.com/docs/cypher-refcard/current/
                const writeQuery = `MERGE (p1:Person { name: $person1Name })
                                    MERGE (p2:Person { name: $person2Name })
                                    MERGE (p1)-[:KNOWS]->(p2)
                                    RETURN p1, p2`;

                // Write transactions allow the driver to handle retries and transient errors.
                const writeResult = await session.executeWrite(tx =>
                    tx.run(writeQuery, { person1Name, person2Name })
                );

                // Check the write results.
                writeResult.records.forEach(record => {
                    const person1Node = record.get('p1');
                    const person2Node = record.get('p2');
                    console.info(`Created friendship between: ${person1Node.properties.name}, ${person2Node.properties.name}`);
                });

            } catch (error) {
                console.error(`Something went wrong: ${error}`);
            } finally {
                // Close down the session if you're not using it anymore.
                await session.close();
            }
        }

        async function findPerson(driver, personName) {

            const session = driver.session({ database: 'neo4j' });

            try {
                const readQuery = `MATCH (p:Person)
                                WHERE p.name = $personName
                                RETURN p.name AS name`;

                const readResult = await session.executeRead(tx =>
                    tx.run(readQuery, { personName })
                );

                readResult.records.forEach(record => {
                    console.log(`Found person: ${record.get('name')}`)
                });
            } catch (error) {
                console.error(`Something went wrong: ${error}`);
            } finally {
                await session.close();
            }
        }
    })();View all (66 more lines)

</div>

</div>

<div>

### Running the example

<div>

Follow the steps below to run the example code:

</div>

<div>

1.  Copy and paste the code above into a file named `example.js`.

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

        node example.js

    </div>

    </div>

</div>

</div>

<div>

### Example walkthrough

<div>

The example imports `neo4j-driver` to connect to the Neo4j AuraDB
instance.

</div>

<div>

Two functions are then called:

</div>

<div>

-   `createFriendship` creates two *`Person`* nodes and a *`KNOWS`*
    relationship between them using a write transaction.

-   `findPerson` finds the *`Person`* nodes using a read transaction.

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

-   Neo4j JavaScript Driver Documentation

</div>

</div>

</div>

</div>
