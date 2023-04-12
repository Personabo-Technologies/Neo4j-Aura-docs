<div>

<div>

# Executing the different algorithm modes

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

This example explains execution modes for GDS algorithms and how to use
each one of them.

</div>

</div>

</div>

<div>

## Setup

<div>

<div>

-   GDS client
-   Cypher
-   Python driver

<div>

<div>

<div>

<div>

For more information on how to get started using Python, refer to the
Connecting with Python tutorial.

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

    pip install graphdatascience

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

    # Import the client
    from graphdatascience import GraphDataScience

    # Replace with the actual URI, username, and password
    AURA_CONNECTION_URI = "neo4j+s://xxxxxxxx.databases.neo4j.io"
    AURA_USERNAME = "neo4j"
    AURA_PASSWORD = ""

    # Configure the client with AuraDS-recommended settings
    gds = GraphDataScience(
        AURA_CONNECTION_URI,
        auth=(AURA_USERNAME, AURA_PASSWORD),
        aura_ds=True
    )

</div>

</div>

<div>

In the following code examples we use the `print` function to print
Pandas `DataFrame` and `Series` objects. You can try different ways to
print a Pandas object, for instance via the `to_string` and `to_json`
methods; if you use a JSON representation, in some cases you may need to
include a default handler to handle Neo4j `DateTime` objects. Check the
Python connection section for some examples.

</div>

</div>

</div>

<div>

<div>

<div>

For more information on how to get started using the Cypher Shell, refer
to the Neo4j Cypher Shell tutorial.

</div>

<div>

<div>

<table>
<tbody><tr>
<td>
<i></i>
</td>
<td>
Run the following commands from the directory where the Cypher shell is installed.
</td>
</tr>
</tbody></table>

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

    export AURA_CONNECTION_URI="neo4j+s://xxxxxxxx.databases.neo4j.io"
    export AURA_USERNAME="neo4j"
    export AURA_PASSWORD=""

    ./cypher-shell -a $AURA_CONNECTION_URI -u $AURA_USERNAME -p $AURA_PASSWORD

</div>

</div>

</div>

</div>

<div>

<div>

<div>

For more information on how to get started using Python, refer to the
Connecting with Python tutorial.

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

<div>

<div>

<div>

<div>

<div>

Copied!

</div>

</div>

</div>

    # Import the driver
    from neo4j import GraphDatabase

    # Replace with the actual URI, username, and password
    AURA_CONNECTION_URI = "neo4j+s://xxxxxxxx.databases.neo4j.io"
    AURA_USERNAME = "neo4j"
    AURA_PASSWORD = ""

    # Instantiate the driver
    driver = GraphDatabase.driver(
        AURA_CONNECTION_URI,
        auth=(AURA_USERNAME, AURA_PASSWORD)
    )

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

    # Import to prettify results
    import json

    # Import for the JSON helper function
    from neo4j.time import DateTime

    # Helper function for serializing Neo4j DateTime in JSON dumps
    def default(o):
        if isinstance(o, (DateTime)):
            return o.isoformat()

</div>

</div>

</div>

</div>

</div>

</div>

</div>

</div>

<div>

## Create an example graph

<div>

<div>

We start by creating some basic graph data first.

</div>

<div>

-   GDS client
-   Cypher
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

    gds.run_cypher("""
        CREATE
          (home:Page {name:'Home'}),
          (about:Page {name:'About'}),
          (product:Page {name:'Product'}),
          (links:Page {name:'Links'}),
          (a:Page {name:'Site A'}),
          (b:Page {name:'Site B'}),
          (c:Page {name:'Site C'}),
          (d:Page {name:'Site D'}),

          (home)-[:LINKS {weight: 0.2}]->(about),
          (home)-[:LINKS {weight: 0.2}]->(links),
          (home)-[:LINKS {weight: 0.6}]->(product),
          (about)-[:LINKS {weight: 1.0}]->(home),
          (product)-[:LINKS {weight: 1.0}]->(home),
          (a)-[:LINKS {weight: 1.0}]->(home),
          (b)-[:LINKS {weight: 1.0}]->(home),
          (c)-[:LINKS {weight: 1.0}]->(home),
          (d)-[:LINKS {weight: 1.0}]->(home),
          (links)-[:LINKS {weight: 0.8}]->(home),
          (links)-[:LINKS {weight: 0.05}]->(a),
          (links)-[:LINKS {weight: 0.05}]->(b),
          (links)-[:LINKS {weight: 0.05}]->(c),
          (links)-[:LINKS {weight: 0.05}]->(d)
    """)View all (12 more lines)

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

    CREATE
      (home:Page {name:'Home'}),
      (about:Page {name:'About'}),
      (product:Page {name:'Product'}),
      (links:Page {name:'Links'}),
      (a:Page {name:'Site A'}),
      (b:Page {name:'Site B'}),
      (c:Page {name:'Site C'}),
      (d:Page {name:'Site D'}),

      (home)-[:LINKS {weight: 0.2}]->(about),
      (home)-[:LINKS {weight: 0.2}]->(links),
      (home)-[:LINKS {weight: 0.6}]->(product),
      (about)-[:LINKS {weight: 1.0}]->(home),
      (product)-[:LINKS {weight: 1.0}]->(home),
      (a)-[:LINKS {weight: 1.0}]->(home),
      (b)-[:LINKS {weight: 1.0}]->(home),
      (c)-[:LINKS {weight: 1.0}]->(home),
      (d)-[:LINKS {weight: 1.0}]->(home),
      (links)-[:LINKS {weight: 0.8}]->(home),
      (links)-[:LINKS {weight: 0.05}]->(a),
      (links)-[:LINKS {weight: 0.05}]->(b),
      (links)-[:LINKS {weight: 0.05}]->(c),
      (links)-[:LINKS {weight: 0.05}]->(d)View all (9 more lines)

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
    create_example_graph_on_disk_query = """
        CREATE
          (home:Page {name:'Home'}),
          (about:Page {name:'About'}),
          (product:Page {name:'Product'}),
          (links:Page {name:'Links'}),
          (a:Page {name:'Site A'}),
          (b:Page {name:'Site B'}),
          (c:Page {name:'Site C'}),
          (d:Page {name:'Site D'}),

          (home)-[:LINKS {weight: 0.2}]->(about),
          (home)-[:LINKS {weight: 0.2}]->(links),
          (home)-[:LINKS {weight: 0.6}]->(product),
          (about)-[:LINKS {weight: 1.0}]->(home),
          (product)-[:LINKS {weight: 1.0}]->(home),
          (a)-[:LINKS {weight: 1.0}]->(home),
          (b)-[:LINKS {weight: 1.0}]->(home),
          (c)-[:LINKS {weight: 1.0}]->(home),
          (d)-[:LINKS {weight: 1.0}]->(home),
          (links)-[:LINKS {weight: 0.8}]->(home),
          (links)-[:LINKS {weight: 0.05}]->(a),
          (links)-[:LINKS {weight: 0.05}]->(b),
          (links)-[:LINKS {weight: 0.05}]->(c),
          (links)-[:LINKS {weight: 0.05}]->(d)
    """

    # Create the driver session
    with driver.session() as session:
        # Run query
        result = session.run(create_example_graph_on_disk_query).data()

        # Prettify the result
        print(json.dumps(result, indent=2, sort_keys=True))View all (20 more lines)

</div>

</div>

</div>

</div>

</div>

</div>

<div>

We then project an in-memory graph from the data just created.

</div>

<div>

-   GDS client
-   Cypher
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

    g, result = gds.graph.project(
        "example-graph",
        "Page",
        "LINKS",
        relationshipProperties="weight"
    )

    print(result)

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

    CALL gds.graph.project(
      'example-graph',
      'Page',
      'LINKS',
      {
        relationshipProperties: 'weight'
      }
    )

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
    create_example_graph_in_memory_query = """
        CALL gds.graph.project(
          'example-graph',
          'Page',
          'LINKS',
          {
            relationshipProperties: 'weight'
          }
        )
    """

    # Create the driver session
    with driver.session() as session:
        # Run query
        result = session.run(create_example_graph_in_memory_query).data()

        # Prettify the result
        print(json.dumps(result, indent=2, sort_keys=True))View all (5 more lines)

</div>

</div>

</div>

</div>

</div>

</div>

</div>

</div>

<div>

## Execution Modes

<div>

<div>

Every production-tier algorithm can be run in four different modes:

</div>

<div>

-   `stats`

-   `stream`

-   `mutate`

-   `write`

</div>

<div>

An additional `estimate` mode is explained in detail in the Estimating
memory usage and resizing an instance section.

</div>

<div>

In the following we'll use the PageRank algorithm to show the usage of
every execution mode.

</div>

<div>

### Stats

<div>

The `stats` mode can be useful for evaluating an algorithm performance
without mutating the in-memory graph. When running an algorithm in this
mode, a single row containing a summary of the algorithm statistics (for
example, counts or percentile distributions) is returned.

</div>

<div>

-   GDS client
-   Cypher
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

    result = gds.pageRank.stats(
        g,
        maxIterations=20,
        dampingFactor=0.85
    )

    print(result)

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

    CALL gds.pageRank.stats(
      'example-graph',
      {maxIterations: 20, dampingFactor: 0.85}
    )
    YIELD ranIterations,
      didConverge,
      preProcessingMillis,
      computeMillis,
      postProcessingMillis,
      centralityDistribution,
      configuration
    RETURN *

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
    page_rank_stats_example_graph_query = """
        CALL gds.pageRank.stats(
          'example-graph',
          {maxIterations: 20, dampingFactor: 0.85}
        )
        YIELD ranIterations,
          didConverge,
          preProcessingMillis,
          computeMillis,
          postProcessingMillis,
          centralityDistribution,
          configuration
        RETURN *
    """

    # Create the driver session
    with driver.session() as session:
        # Run query
        result = session.run(page_rank_stats_example_graph_query).data()

        # Prettify the result
        print(json.dumps(result, indent=2, sort_keys=True))View all (8 more lines)

</div>

</div>

</div>

</div>

</div>

</div>

<div>

The result contains the estimated time to run the algorithm
(`computeMillis`) along with other details like the centrality
distribution and the configuration parameters.

</div>

</div>

<div>

### Stream

<div>

The `stream` mode returns the results of an algorithm as Cypher result
rows. This is similar to how standard Cypher reading queries operate.

</div>

<div>

With the PageRank example, this mode returns a node ID and the computed
PageRank score for each node. The `gds.util.asNode` procedure can then
be used to find a node from its node ID.

</div>

<div>

-   GDS client
-   Cypher
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

    results = gds.pageRank.stream(
        g,
        maxIterations=20,
        dampingFactor=0.85
    )

    print(results)

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

    CALL gds.pageRank.stream(
      'example-graph',
      {maxIterations: 20, dampingFactor: 0.85}
    )
    YIELD nodeId, score
    RETURN *

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

    # Cypher query to just get internal node ID and score
    page_rank_stream_example_graph_query = """
        CALL gds.pageRank.stream(
          'example-graph',
          {maxIterations: 20, dampingFactor: 0.85}
        )
        YIELD nodeId, score
        RETURN *
    """

    # Create the driver session
    with driver.session() as session:
        # Run query
        results = session.run(page_rank_stream_example_graph_query).data()

        # Prettify the results
        print(json.dumps(results, indent=2, sort_keys=True))

</div>

</div>

</div>

</div>

</div>

</div>

<div>

Since an algorithm can run for a long time and the connection may
suddenly drop, we suggest to use the `mutate` and `write` modes instead
to make sure that the computation completes and the results are saved.

</div>

</div>

<div>

### Mutate

<div>

The `mutate` mode operates on the in-memory graph and updates it with a
new property specified with the `mutateProperty` configuration
parameter. The new property must not already exist in the in-memory
graph.

</div>

<div>

This mode is useful when chaining the execution of several algorithms
each of which relying on the results on the previous.

</div>

<div>

In the case of PageRank, the result of this mode is a score for each
node. In this example we add the calculated score to each node of the
in-memory graph as the value of a new property called `pageRankScore`.

</div>

<div>

-   GDS client
-   Cypher
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

    result = gds.pageRank.mutate(
        g,
        mutateProperty="pageRankScore",
        maxIterations=20,
        dampingFactor=0.85
    )

    print(result)

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

    CALL gds.pageRank.mutate(
      'example-graph',
      {mutateProperty: 'pageRankScore', maxIterations: 20, dampingFactor: 0.85}
    )
    YIELD nodePropertiesWritten, ranIterations
    RETURN *

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

    # Cypher query to just get mutate the graph
    page_rank_mutate_example_graph_query = """
        CALL gds.pageRank.mutate(
          'example-graph',
          {mutateProperty: 'pageRankScore', maxIterations: 20, dampingFactor: 0.85}
        )
        YIELD nodePropertiesWritten, ranIterations
        RETURN *
    """

    # Create the driver session
    with driver.session() as session:
        # Run query
        result = session.run(page_rank_mutate_example_graph_query).data()

        # Prettify the result
        print(json.dumps(result, indent=2, sort_keys=True))

</div>

</div>

</div>

</div>

</div>

</div>

</div>

<div>

### Write

<div>

The `write` mode writes the results of the algorithm computation back to
the Neo4j database. The written data can be node properties (such as
PageRank scores), new relationships (such as Node Similarity
similarities), or relationship properties (only for newly created
relationships).

</div>

<div>

Similarly to the previous example, here we add the calculated score of
the PageRank algorithm to each node of the Neo4j database as the value
of a new property called `pageRankScore`.

</div>

<div>

<div>

<table>
<tbody><tr>
<td>
<i></i>
</td>
<td>
To use the result of a <code>write</code> mode computation with another algorithm, a new in-memory graph must be created from the Neo4j database.
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

-   GDS client
-   Cypher
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

    result = gds.pageRank.write(
        g,
        writeProperty="pageRankScore",
        maxIterations=20,
        dampingFactor=0.85
    )

    print(result)

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

    CALL gds.pageRank.write(
      'example-graph',
      {writeProperty: 'pageRankScore', maxIterations: 20, dampingFactor: 0.85}
    )
    YIELD nodePropertiesWritten, ranIterations
    RETURN *

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

    # Cypher query to write the graph
    page_rank_write_example_graph_query = """
        CALL gds.pageRank.write(
          'example-graph',
          {writeProperty: 'pageRankScore', maxIterations: 20, dampingFactor: 0.85}
        )
        YIELD nodePropertiesWritten, ranIterations
        RETURN *
    """

    # Create the driver session
    with driver.session() as session:
        # Run query
        result = session.run(page_rank_write_example_graph_query).data()

        # Prettify the result
        print(json.dumps(result, indent=2, sort_keys=True))

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

## Cleanup

<div>

<div>

After going through the example, both the in-memory graphs and the data
in the Neo4j database can be deleted.

</div>

<div>

-   GDS client
-   Cypher
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

    result = gds.graph.drop(g)
    print(result)

    gds.run_cypher("""
        MATCH (n)
        DETACH DELETE n
    """)

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

    CALL gds.graph.drop('example-graph');

    MATCH (n)
    DETACH DELETE n;

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

    delete_example_in_memory_graph_query = """
        CALL gds.graph.drop('example-graph')
    """

    delete_example_graph = """
        MATCH (n)
        DETACH DELETE n
    """

    with driver.session() as session:
        # Delete in-memory graph
        result = session.run(delete_example_in_memory_graph_query).data()

        # Prettify the result
        print(json.dumps(result, indent=2, sort_keys=True, default=default))

        # Delete data from Neo4j
        result = session.run(delete_example_graph).data()

        # Prettify the result
        print(json.dumps(result, indent=2, sort_keys=True, default=default))View all (6 more lines)

</div>

</div>

</div>

</div>

</div>

</div>

<div>

### Closing the connection

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
