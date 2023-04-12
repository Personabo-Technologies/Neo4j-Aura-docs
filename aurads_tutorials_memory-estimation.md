<div>

<div>

# Estimating memory usage and resizing an instance

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

This example shows how to:

</div>

<div>

-   use the memory estimation mode to estimate the memory requirements
    for an algorithm before running it

-   resize an AuraDS instance to accommodate the algorithm memory
    requirements

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

An easy way to create an in-memory graph is through the GDS
https://neo4j.com/docs/graph-data-science/current/management-ops/projections/graph-generation/
\[graph generation\^\] algorithm. By specifing the number of nodes, the
average number of relationships going out of each node and the
relationship distribution function, the algorithm creates a graph having
the following shape:

</div>

<div>

`(:50000000_Nodes)-[:REL]→(:50000000_Nodes)`

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

    # Run the graph generation algorithm and retrieve the corresponding
    # graph object and call result metadata
    g, result = gds.beta.graph.generate(
        "example-graph",
        50000000,
        3,
        relationshipDistribution="POWER_LAW"
    )

    # Print prettified graph stats
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

    CALL gds.beta.graph.generate(
      'example-graph',
      50000000,
      3,
      {relationshipDistribution: 'POWER_LAW'}
    )
    YIELD name,
      nodes,
      relationships,
      generateMillis,
      relationshipSeed,
      averageDegree,
      relationshipDistribution,
      relationshipProperty
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
    create_example_graph_query = """
        CALL gds.beta.graph.generate(
          'example-graph',
          50000000,
          3,
          {relationshipDistribution: 'POWER_LAW'}
        )
        YIELD name,
          nodes,
          relationships,
          generateMillis,
          relationshipSeed,
          averageDegree,
          relationshipDistribution,
          relationshipProperty
        RETURN *
    """

    # Create the driver session
    with driver.session() as session:
        # Run query
        result = session.run(create_example_graph_query).data()

        # Prettify the result
        print(json.dumps(result, indent=2, sort_keys=True, default=default))View all (12 more lines)

</div>

</div>

</div>

</div>

</div>

</div>

<div>

<div>

<table>
<tbody><tr>
<td>
<i></i>
</td>
<td>
The graph is fairly large, so the generation procedure will take a few minutes to complete.
</td>
</tr>
</tbody></table>

</div>

</div>

</div>

</div>

<div>

## Run the `estimate` mode

<div>

<div>

The estimation of the memory requirements of an algorithm on an
in-memory graph can be useful to determine whether the current AuraDS
instance has enough resources to run the algorithm to completion.

</div>

<div>

The Graph Data Science has guard rails built in: if an algorithm is
estimated to use more RAM than is available, an exception is raised. In
this case, the AuraDS instance can be resized before running the
algorithm again.

</div>

<div>

In the following example we get a memory estimation for the Label
Propagation algorithm to run on the generated graph. The estimated
memory is between 381 MiB and 4477 MiB, which is higher than an 8GB
instance has available (4004 MiB).

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

    result = gds.labelPropagation.mutate.estimate(
        g,
        mutateProperty="communityID"
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

    CALL gds.labelPropagation.mutate.estimate(
      'example-graph',
      {mutateProperty: 'communityID'}
    )
    YIELD nodeCount,
      relationshipCount,
      bytesMin,
      bytesMax,
      requiredMemory
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
    page_rank_mutate_estimate_example_graph_query = """
        CALL gds.labelPropagation.mutate.estimate(
          'example-graph',
          {mutateProperty: 'communityID'}
        )
        YIELD nodeCount,
          relationshipCount,
          bytesMin,
          bytesMax,
          requiredMemory
        RETURN *
    """

    # Create the driver session
    with driver.session() as session:
        # Run query
        results = session.run(page_rank_mutate_estimate_example_graph_query).data()

        # Prettify the result
        print(json.dumps(results, indent=2, sort_keys=True))View all (6 more lines)

</div>

</div>

</div>

</div>

</div>

</div>

<div>

The `mutate` procedure hits the guard rails on an 8GB instance, raising
an exception that suggests to resize the AuraDS instance.

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

    result = gds.labelPropagation.mutate(
        g,
        mutateProperty="communityID"
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

    CALL gds.labelPropagation.mutate(
      'example-graph',
      {mutateProperty: 'communityID'}
    )
    YIELD preProcessingMillis,
      computeMillis,
      mutateMillis,
      postProcessingMillis,
      nodePropertiesWritten,
      communityCount,
      ranIterations,
      didConverge,
      communityDistribution,
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
    page_rank_mutate_example_graph_query = """
        CALL gds.labelPropagation.mutate(
          'example-graph',
          {mutateProperty: 'communityID'}
        )
        YIELD preProcessingMillis,
          computeMillis,
          mutateMillis,
          postProcessingMillis,
          nodePropertiesWritten,
          communityCount,
          ranIterations,
          didConverge,
          communityDistribution,
          configuration
        RETURN *
    """

    # Create the driver session
    with driver.session() as session:
        # Run query
        results = session.run(page_rank_mutate_example_graph_query).data()

        # Prettify the result
        print(json.dumps(results, indent=2, sort_keys=True))View all (12 more lines)

</div>

</div>

</div>

</div>

</div>

</div>

</div>

</div>

<div>

## Resize the AuraDS instance

<div>

<div>

You will need to resize the instance to the next available size (16GB)
in order to continue. An AuraDS instance can be resized from the Neo4j
Aura Console homepage. For more information, check the Instance actions
section.

</div>

<div>

<div>

<table>
<tbody><tr>
<td>
<i></i>
</td>
<td>
Resizing an AuraDS instance incurs a short amount of downtime.
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

After resizing, wait a few seconds until the projected graph is
reloaded, then run the `mutate` step again. This time no exception is
thrown and the step completes successfully.

</div>

</div>

</div>

<div>

## Cleanup

<div>

<div>

The in-memory graph can now be deleted.

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

    CALL gds.graph.drop('example-graph')

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

    with driver.session() as session:
        # Run query
        results = session.run(delete_example_in_memory_graph_query).data()

        # Prettify the results
        print(json.dumps(results, indent=2, sort_keys=True, default=default))

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
