<div>

<div>

# Go

</div>

<div>

## Prerequisites

<div>

<div>

-   Go runtime at supported version (see Go release policy)

</div>

</div>

</div>

<div>

## Initializing the project

<div>

<div>

Use the following command to initialize the Go module, replacing
`<project-url>` with the URL of your project:

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

    go mod init <project-url>
    go get

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

    package main

    import (
        "context"
        "fmt"

        "github.com/neo4j/neo4j-go-driver/v5/neo4j"
    )

    func main() {
        // Aura requires you to use "neo4j+s" protocol
        // (You need to replace your connection details, username and password)
        uri := "neo4j+s://<Bolt url for Neo4j Aura instance>"
        auth := neo4j.BasicAuth("<Username for Neo4j Aura instance>", "<Password for Neo4j Aura instance>", "")
        // You typically have one driver instance for the entire application. The
        // driver maintains a pool of instance connections to be used by the sessions.
        // The driver is thread safe.
        driver, err := neo4j.NewDriverWithContext(uri, auth)
        if err != nil {
            panic(err)
        }
        // You can specify custom contexts to control the execution of the driver operations
        // This one never cancels, never times out and is used in subsequent calls
        // You can instead specify different contexts for different operations
        // Read more about contexts in https://pkg.go.dev/context
        ctx := context.Background()
        // Don't forget to close the driver connection when you are finished with it
        defer driver.Close(ctx)
        // Create a session to run transactions in. Sessions are lightweight to
        // create and use. Sessions are NOT thread safe.
        session := driver.NewSession(ctx, neo4j.SessionConfig{DatabaseName: "neo4j"})
        defer session.Close(ctx)
        // WriteTransaction retries the operation in case of transient errors by
        // invoking the anonymous function multiple times until it succeeds.
        records, err := session.ExecuteWrite(ctx,
            func(tx neo4j.ManagedTransaction) (any, error) {
                // To learn more about the Cypher syntax, see https://neo4j.com/docs/cypher-manual/current/
                // The Reference Card is also a good resource for keywords https://neo4j.com/docs/cypher-refcard/current/
                createRelationshipBetweenPeopleQuery := `
                    MERGE (p1:Person { name: $person1_name })
                    MERGE (p2:Person { name: $person2_name })
                    MERGE (p1)-[:KNOWS]->(p2)
                    RETURN p1, p2`
                result, err := tx.Run(ctx, createRelationshipBetweenPeopleQuery, map[string]any{
                    "person1_name": "Alice",
                    "person2_name": "David",
                })
                if err != nil {
                    // Return the error received from driver here to indicate rollback,
                    // the error is analyzed by the driver to determine if it should try again.
                    return nil, err
                }
                // Collects all records and commits the transaction (as long as
                // Collect doesn't return an error).
                // Beware that Collect will buffer the records in memory.
                return result.Collect(ctx)
            })
        if err != nil {
            panic(err)
        }
        for _, record := range records.([]*neo4j.Record) {
            firstPerson := record.Values[0].(neo4j.Node)
            fmt.Printf("First: '%s'\n", firstPerson.Props["name"].(string))
            secondPerson := record.Values[1].(neo4j.Node)
            fmt.Printf("Second: '%s'\n", secondPerson.Props["name"].(string))
        }

        // Now read the created persons. By using ReadTransaction method a connection
        // to a read replica can be used which reduces load on writer nodes in cluster.
        _, err = session.ExecuteRead(ctx, func(tx neo4j.ManagedTransaction) (any, error) {
            // Code within this function might be invoked more than once in case of
            // transient errors.
            readPersonByName := `
                MATCH (p:Person)
                WHERE p.name = $person_name
                RETURN p.name AS name`
            result, err := tx.Run(ctx, readPersonByName, map[string]any{
                "person_name": "Alice",
            })
            if err != nil {
                return nil, err
            }
            // Iterate over the result within the transaction instead of using
            // Collect (just to show how it looks...). Result.Next returns true
            // while a record could be retrieved, in case of error result.Err()
            // will return the error.
            for result.Next(ctx) {
                fmt.Printf("Person name: '%s' \n", result.Record().Values[0].(string))
            }
            // Again, return any error back to driver to indicate rollback and
            // retry in case of transient error.
            return nil, result.Err()
        })
        if err != nil {
            panic(err)
        }
    }View all (82 more lines)

</div>

</div>

<div>

### Running the example

<div>

Follow the steps below to run the example code:

</div>

<div>

1.  Copy and paste the code above into a file named `example.go`.

2.  Enter the information for the AuraDB instance you want to connect to
    by replacing:

    <div>

    -   `<Bolt url for Neo4j Aura instance>` with the URI.

    -   `<Username for Neo4j Aura instance>` with the username.

    -   `<Password for Neo4j Aura instance>` with the password.

    </div>

3.  Use the following command to update any unused or missing
    dependencies:

    <div>

    <div>

    <div>

    <div>

    <div>

    Copied!

    </div>

    </div>

    </div>

        go mod tidy

    </div>

    </div>

4.  Use the following command to run the example code:

    <div>

    <div>

    <div>

    <div>

    <div>

    Copied!

    </div>

    </div>

    </div>

        go run example.go

    </div>

    </div>

</div>

</div>

<div>

### Example walkthrough

<div>

The example imports `neo4j-go-driver` to connect to the Neo4j AuraDB
instance.

</div>

<div>

Within the `main` function, a write transaction creates two \'Person\'
nodes, Alice and David, and a \'KNOWS\' relationship between them, and a
read transaction finds Alice.

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

-   Neo4j Go Driver Documentation

</div>

</div>

</div>

</div>
