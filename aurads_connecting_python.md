<div>

<div>

# Connecting with Python

</div>

<div>

<div>

<div>

<div>

<table>
<tbody><tr>
<td>
<i></i>
</td>
<td>
Follow along with a notebook in <a><span><img/></span> Google Colab</a>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

This tutorial shows how to interact with AuraDS using the Graph Data
Science (GDS) client or the Python Driver. In the following sections you
can switch between client and driver code clicking on the appropriate
tab.

</div>

<div>

A running AuraDS instance must be available along with access
credentials (generated in the Creating an AuraDS instance section) and
its connection URI (found in the instance detail page, starting with
`neo4j+s://`).

</div>

</div>

</div>

<div>

## Installation

<div>

<div>

Both the GDS client and the Python driver can be installed using `pip`.

</div>

<div>

-   GDS client
-   Python driver

<div>

<div>

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

    pip install graphdatascience

</div>

</div>

<div>

The latest stable version of the client can be found on PyPI.

</div>

</div>

</div>

<div>

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

    pip install neo4j

</div>

</div>

<div>

The latest stable version of the driver can be found on PyPI.

</div>

</div>

</div>

</div>

</div>

<div>

If `pip` is not available, you can try replacing it with `python -m pip`
or `python3 -m pip`.

</div>

</div>

</div>

<div>

## Import and setup

<div>

<div>

Both the GDS client and the Python driver require the connection URI and
the credentials as shown in the introduction.

</div>

<div>

-   GDS client
-   Python driver

<div>

<div>

<div>

<div>

The client is imported as the `GraphDataScience` class:

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

    # Client import
    from graphdatascience import GraphDataScience

</div>

</div>

<div>

The `aura_ds=True` constructor argument should be used to have the
recommended non-default configuration settings of the Python Driver
applied automatically.

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

    # Replace with the actual URI, username, and password
    AURA_CONNECTION_URI = "neo4j+s://xxxxxxxx.databases.neo4j.io"
    AURA_USERNAME = "neo4j"
    AURA_PASSWORD = "..."

    # Client instantiation
    gds = GraphDataScience(
        AURA_CONNECTION_URI,
        auth=(AURA_USERNAME, AURA_PASSWORD),
        aura_ds=True
    )

</div>

</div>

</div>

</div>

<div>

<div>

<div>

The driver is imported as the `GraphDatabase` class:

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

    # Driver import
    from neo4j import GraphDatabase

</div>

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

    # Replace with the actual URI, username and password
    AURA_CONNECTION_URI = "neo4j+s://xxxxxxxx.databases.neo4j.io"
    AURA_USERNAME = "neo4j"
    AURA_PASSWORD = "..."

    # Driver instantiation
    driver = GraphDatabase.driver(
        AURA_CONNECTION_URI,
        auth=(AURA_USERNAME, AURA_PASSWORD)
    )

</div>

</div>

</div>

</div>

</div>

</div>

</div>

</div>

<div>

## Running a query

<div>

<div>

Once created, the client (or the driver) can be used to run Cypher
queries and call Cypher procedures. In this example the `gds.version`
procedure can be used to retrieve the version of GDS running on the
instance.

</div>

<div>

-   GDS client
-   Python driver

<div>

<div>

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

    # Call a GDS method directly
    print(gds.version())

</div>

</div>

</div>

</div>

<div>

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

    # Cypher query
    gds_version_query = """
        RETURN gds.version() AS version
    """

    # Create a driver session
    with driver.session() as session:
        # Use .data() to access the results array
        results = session.run(gds_version_query).data()
        print(results)

</div>

</div>

</div>

</div>

</div>

</div>

<div>

The following code retrieves all the procedures available in the library
and shows the details of five of them.

</div>

<div>

-   GDS client
-   Python driver

<div>

<div>

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

    # Assign the result of the client call to a variable
    results = gds.list()

    # Print the result (a Pandas DataFrame)
    print(results[:5])

</div>

</div>

<div>

Since the result is a Pandas DataFrame, you can use methods such as
`to_string` and `to_json` to pretty-print it.

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

    # Print the result (a Pandas DataFrame) as a console-friendly string
    print(results[:5].to_string())

</div>

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

    # Print the result (a Pandas DataFrame) as a prettified JSON string
    print(results[:5].to_json(orient="table", indent=2))

</div>

</div>

</div>

</div>

<div>

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

    # Import the json module for pretty visualization
    import json

    # Cypher query
    list_all_gds_procedures_query = """
        CALL gds.list()
    """

    # Create a driver session
    with driver.session() as session:
        # Use .data() to access the results array
        results = session.run(list_all_gds_procedures_query).data()

        # Print the prettified result
        print(json.dumps(results[:5], indent=2))

</div>

</div>

</div>

</div>

</div>

</div>

<div>

### Serializing Neo4j `DateTime` in JSON dumps

<div>

In some cases the result of a procedure call may contain Neo4j
`DateTime` objects. In order to serialize such objects into JSON, a
default handler must be provided.

</div>

<div>

-   GDS client
-   Python driver

<div>

<div>

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

    # Import for the JSON helper function
    from neo4j.time import DateTime

    # Helper function for serializing Neo4j DateTime in JSON dumps
    def default(o):
        if isinstance(o, (DateTime)):
            return o.isoformat()

    # Run the graph generation algorithm
    g, _ = gds.beta.graph.generate(
        "example-graph", 10, 3, relationshipDistribution="POWER_LAW"
    )

    # Drop the graph keeping the result of the operation, which contains
    # some DateTime fields ("creationTime" and "modificationTime")
    result = gds.graph.drop(g)

    # Print the result as JSON, converting the DateTime fields with
    # the handler defined above
    print(result.to_json(indent=2, default_handler=default))View all (6 more lines)

</div>

</div>

</div>

</div>

<div>

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

    # Import to prettify results
    import json

    # Import for the JSON helper function
    from neo4j.time import DateTime

    # Helper function for serializing Neo4j DateTime in JSON dumps
    def default(o):
        if isinstance(o, (DateTime)):
            return o.isoformat()

    # Example query to run a graph generation algorithm
    create_example_graph_query = """
        CALL gds.beta.graph.generate(
          'example-graph', 10, 3, {relationshipDistribution: 'POWER_LAW'}
        )
    """

    # Example query to delete a graph
    delete_example_graph_query = """
        CALL gds.graph.drop('example-graph')
    """

    # Create the driver session
    with driver.session() as session:
        # Run the graph generation algorithm
        session.run(create_example_graph_query).data()

        # Drop the generated graph keeping the result of the operation
        results = session.run(delete_example_graph_query).data()

        # Prettify the results using the handler defined above
        print(json.dumps(results, indent=2, sort_keys=True, default=default))View all (18 more lines)

</div>

</div>

</div>

</div>

</div>

</div>

</div>

</div>

</div>

<div>

## Closing the connection

<div>

<div>

The connection should always be closed when no longer needed.

</div>

<div>

-   GDS client
-   Python driver

<div>

<div>

<div>

<div>

Although the GDS client automatically closes the connection when the
object is deleted, it is good practice to close it explicitly.

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

    # Close the client connection
    gds.close()

</div>

</div>

</div>

</div>

<div>

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

    # Close the driver connection
    driver.close()

</div>

</div>

</div>

</div>

</div>

</div>

</div>

</div>

<div>

## References

<div>

<div>

### Documentation

<div>

-   Neo4j GDS documentation

-   Neo4j driver documentation

-   Neo4j developer documentation

</div>

</div>

<div>

### Cypher

<div>

-   Learn more about the Cypher syntax

-   The Cypher reference card is also a great resource for understanding
    how to use Cypher keywords

</div>

</div>

<div>

### Modelling

<div>

-   Data modelling guidelines

-   Data modelling design

-   Refactoring a data model

</div>

</div>

</div>

</div>

</div>
