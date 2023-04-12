<div>

<div>

# Monitoring the progress of a running algorithm

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

Running algorithms on large graphs can be computationally expensive.
This example shows how to use the `gds.beta.listProgress` procedure to
monitor the progress of an algorithm, both to get an idea of the
processing speed and to determine when the computation is completed.

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

`(:1000000_Nodes)-[:REL]→(:1000000_Nodes)`

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
        1000000,
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
      1000000,
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
          1000000,
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

</div>

</div>

<div>

## Run an algorithm and check the progress

<div>

<div>

We need to run an algorithm that takes some time to converge. In this
example we use the Label Propagation algorithm, which we start in a
separate thread so that we can check its progress in the same Python
process.

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

    # Import to run the long-running algorithm in a thread
    import threading
    # Import to use the sleep method
    import time


    # Method to call the label propagation algorithm from a thread
    def run_label_prop():
        print("Running label propagation")

        result = gds.labelPropagation.mutate(
            g,
            mutateProperty="communityID"
        )

        print(result)


    # Method to get and pretty-print the algorithm progress
    def run_list_progress():
        result = gds.beta.listProgress()

        print(result)


    # Create a thread for the label propagation algorithm and start it
    label_prop_query_thread = threading.Thread(target=run_label_prop)
    label_prop_query_thread.start()

    # Sleep for a few seconds so the label propagation query has time to get going
    print('Sleeping for 5 seconds')
    time.sleep(5)

    # Check the algorithm progress
    run_list_progress()

    # Sleep for a few more seconds
    print('Sleeping for 10 more seconds')
    time.sleep(10)

    # Check the algorithm progress again
    run_list_progress()

    # Block and wait for the algorithm thread to finish
    label_prop_query_thread.join()View all (30 more lines)

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

    // The following query has to be run in another Cypher shell, so run this command
    // in a different terminal first:
    //
    // ./cypher-shell -a $AURA_CONNECTION_URI -u $AURA_USERNAME -p $AURA_PASSWORD

    CALL gds.beta.listProgress()
    YIELD jobId, taskName, progress, progressBar
    RETURN *View all (9 more lines)

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

    # Import to run the long-running algorithm in a thread
    import threading
    # Import to use the sleep method
    import time


    # Method to call the label propagation algorithm from a thread
    def run_label_prop():
        label_prop_mutate_example_graph_query = """
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
            print("Running label propagation")
            results = session.run(label_prop_mutate_example_graph_query).data()
            # Prettify the first result
            print(json.dumps(results[0], indent=2, sort_keys=True))


    # Method to get and pretty-print the algorithm progress
    def run_list_progress():
        gds_list_progress_query = """
            CALL gds.beta.listProgress()
            YIELD jobId, taskName, progress, progressBar
            RETURN *
        """

        # Create the driver session
        with driver.session() as session:
            # Run query
            print('running list progress')
            results = session.run(gds_list_progress_query).data()
            # Prettify the first result
            print('list progress results: ')
            print(json.dumps(results[0], indent=2, sort_keys=True))


    # Create a thread for the label propagation algorithm and start it
    label_prop_query_thread = threading.Thread(target=run_label_prop)
    label_prop_query_thread.start()

    # Sleep for a few seconds so the label propagation query has time to get going
    print('Sleeping for 5 seconds')
    time.sleep(5)

    # Check the algorithm progress
    run_list_progress()

    # Sleep for a few more seconds
    print('Sleeping for 10 more seconds')
    time.sleep(10)

    # Check the algorithm progress again
    run_list_progress()

    # Block and wait for the algorithm thread to finish
    label_prop_query_thread.join()View all (58 more lines)

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
