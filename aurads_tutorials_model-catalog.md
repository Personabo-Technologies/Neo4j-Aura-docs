<div>

<div>

# Persisting and sharing machine learning models

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

This example shows how to train, save, publish, and drop a machine
learning model using the Model Catalog.

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
        MERGE (dan:Person:ExampleData   {name: 'Dan',   age: 20, heightAndWeight: [185, 75]})
        MERGE (annie:Person:ExampleData {name: 'Annie', age: 12, heightAndWeight: [124, 42]})
        MERGE (matt:Person:ExampleData  {name: 'Matt',  age: 67, heightAndWeight: [170, 80]})
        MERGE (jeff:Person:ExampleData  {name: 'Jeff',  age: 45, heightAndWeight: [192, 85]})
        MERGE (brie:Person:ExampleData  {name: 'Brie',  age: 27, heightAndWeight: [176, 57]})
        MERGE (elsa:Person:ExampleData  {name: 'Elsa',  age: 32, heightAndWeight: [158, 55]})
        MERGE (john:Person:ExampleData  {name: 'John',  age: 35, heightAndWeight: [172, 76]})

        MERGE (dan)-[:KNOWS {relWeight: 1.0}]->(annie)
        MERGE (dan)-[:KNOWS {relWeight: 1.6}]->(matt)
        MERGE (annie)-[:KNOWS {relWeight: 0.1}]->(matt)
        MERGE (annie)-[:KNOWS {relWeight: 3.0}]->(jeff)
        MERGE (annie)-[:KNOWS {relWeight: 1.2}]->(brie)
        MERGE (matt)-[:KNOWS {relWeight: 10.0}]->(brie)
        MERGE (brie)-[:KNOWS {relWeight: 1.0}]->(elsa)
        MERGE (brie)-[:KNOWS {relWeight: 2.2}]->(jeff)
        MERGE (john)-[:KNOWS {relWeight: 5.0}]->(jeff)

        RETURN True AS exampleDataCreated
    """)View all (6 more lines)

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

    MERGE (dan:Person:ExampleData   {name: 'Dan',   age: 20, heightAndWeight: [185, 75]})
    MERGE (annie:Person:ExampleData {name: 'Annie', age: 12, heightAndWeight: [124, 42]})
    MERGE (matt:Person:ExampleData  {name: 'Matt',  age: 67, heightAndWeight: [170, 80]})
    MERGE (jeff:Person:ExampleData  {name: 'Jeff',  age: 45, heightAndWeight: [192, 85]})
    MERGE (brie:Person:ExampleData  {name: 'Brie',  age: 27, heightAndWeight: [176, 57]})
    MERGE (elsa:Person:ExampleData  {name: 'Elsa',  age: 32, heightAndWeight: [158, 55]})
    MERGE (john:Person:ExampleData  {name: 'John',  age: 35, heightAndWeight: [172, 76]})

    MERGE (dan)-[:KNOWS {relWeight: 1.0}]->(annie)
    MERGE (dan)-[:KNOWS {relWeight: 1.6}]->(matt)
    MERGE (annie)-[:KNOWS {relWeight: 0.1}]->(matt)
    MERGE (annie)-[:KNOWS {relWeight: 3.0}]->(jeff)
    MERGE (annie)-[:KNOWS {relWeight: 1.2}]->(brie)
    MERGE (matt)-[:KNOWS {relWeight: 10.0}]->(brie)
    MERGE (brie)-[:KNOWS {relWeight: 1.0}]->(elsa)
    MERGE (brie)-[:KNOWS {relWeight: 2.2}]->(jeff)
    MERGE (john)-[:KNOWS {relWeight: 5.0}]->(jeff)

    RETURN True AS exampleDataCreatedView all (5 more lines)

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
        MERGE (dan:Person:ExampleData   {name: 'Dan',   age: 20, heightAndWeight: [185, 75]})
        MERGE (annie:Person:ExampleData {name: 'Annie', age: 12, heightAndWeight: [124, 42]})
        MERGE (matt:Person:ExampleData  {name: 'Matt',  age: 67, heightAndWeight: [170, 80]})
        MERGE (jeff:Person:ExampleData  {name: 'Jeff',  age: 45, heightAndWeight: [192, 85]})
        MERGE (brie:Person:ExampleData  {name: 'Brie',  age: 27, heightAndWeight: [176, 57]})
        MERGE (elsa:Person:ExampleData  {name: 'Elsa',  age: 32, heightAndWeight: [158, 55]})
        MERGE (john:Person:ExampleData  {name: 'John',  age: 35, heightAndWeight: [172, 76]})

        MERGE (dan)-[:KNOWS {relWeight: 1.0}]->(annie)
        MERGE (dan)-[:KNOWS {relWeight: 1.6}]->(matt)
        MERGE (annie)-[:KNOWS {relWeight: 0.1}]->(matt)
        MERGE (annie)-[:KNOWS {relWeight: 3.0}]->(jeff)
        MERGE (annie)-[:KNOWS {relWeight: 1.2}]->(brie)
        MERGE (matt)-[:KNOWS {relWeight: 10.0}]->(brie)
        MERGE (brie)-[:KNOWS {relWeight: 1.0}]->(elsa)
        MERGE (brie)-[:KNOWS {relWeight: 2.2}]->(jeff)
        MERGE (john)-[:KNOWS {relWeight: 5.0}]->(jeff)

        RETURN True AS exampleDataCreated
    """

    # Create the driver session
    with driver.session() as session:
        # Run query
        result = session.run(create_example_graph_on_disk_query).data()

        # Prettify the result
        print(json.dumps(result, indent=2, sort_keys=True))View all (15 more lines)

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
        "example_graph_for_graphsage",
        {
            "Person": {
                "label": "ExampleData",
                "properties": ["age", "heightAndWeight"]
            }
        },
        {
            "KNOWS": {
                "type": "KNOWS",
                "orientation": "UNDIRECTED",
                "properties": ["relWeight"]
            }
        }
    )

    print(result)View all (3 more lines)

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
      'example_graph_for_graphsage',
      {
        Person: {
          label: 'ExampleData',
          properties: ['age', 'heightAndWeight']
        }
      },
      {
        KNOWS: {
          type: 'KNOWS',
          orientation: 'UNDIRECTED',
          properties: ['relWeight']
        }
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
          'example_graph_for_graphsage',
          {
            Person: {
              label: 'ExampleData',
              properties: ['age', 'heightAndWeight']
            }
          },
          {
            KNOWS: {
              type: 'KNOWS',
              orientation: 'UNDIRECTED',
              properties: ['relWeight']
            }
          }
        )
    """

    # Create the driver session
    with driver.session() as session:
        # Run query
        result = session.run(create_example_graph_in_memory_query).data()

        # Prettify the result
        print(json.dumps(result, indent=2, sort_keys=True))View all (12 more lines)

</div>

</div>

</div>

</div>

</div>

</div>

</div>

</div>

<div>

## Train a model

<div>

<div>

Machine learning algorithms that support the `train` mode produce
trained models which are stored in the Model Catalog. Similarly,
`predict` procedures can use such trained models to produce predictions.
In this example we train a model for the GraphSAGE algorithm using the
`train` mode.

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

    model, result = gds.beta.graphSage.train(
        g,
        modelName="example_graph_model_for_graphsage",
        featureProperties=["age", "heightAndWeight"],
        aggregator="mean",
        activationFunction="sigmoid",
        sampleSizes=[25, 10]
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

      CALL gds.beta.graphSage.train(
        'example_graph_for_graphsage',
        {
          modelName: 'example_graph_model_for_graphsage',
          featureProperties: ['age', 'heightAndWeight'],
          aggregator: 'mean',
          activationFunction: 'sigmoid',
          sampleSizes: [25, 10]
        }
      )
      YIELD modelInfo as info
      RETURN
        info.name as modelName,
        info.metrics.didConverge as didConverge,
        info.metrics.ranEpochs as ranEpochs,
        info.metrics.epochLosses as epochLosses

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
    train_graph_sage_on_in_memory_graph_query  = """
        CALL gds.beta.graphSage.train(
          'example_graph_for_graphsage',
          {
            modelName: 'example_graph_model_for_graphsage',
            featureProperties: ['age', 'heightAndWeight'],
            aggregator: 'mean',
            activationFunction: 'sigmoid',
            sampleSizes: [25, 10]
          }
        )
        YIELD modelInfo as info
        RETURN
          info.name as modelName,
          info.metrics.didConverge as didConverge,
          info.metrics.ranEpochs as ranEpochs,
          info.metrics.epochLosses as epochLosses
    """

    # Create the driver session
    with driver.session() as session:
        # Run query
        result = session.run(train_graph_sage_on_in_memory_graph_query).data()

        # Prettify the result
        print(json.dumps(result, indent=2, sort_keys=True))View all (12 more lines)

</div>

</div>

</div>

</div>

</div>

</div>

</div>

</div>

<div>

## View the model catalog

<div>

<div>

We can use the `gds.beta.model.list` procedure to get information on all
the models currently available in the catalog. Along with information on
the graph schema, the model name, and the training configuration, the
result of the call contains the following fields:

</div>

<div>

-   `loaded`: flag denoting if the model is in memory (`true`) or
    available on disk (`false`)

-   `stored`: flag denoting whether the model has been persisted to disk

-   `shared`: flag denoting whether the model has been published, making
    it accessible to all users

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

    results = gds.beta.model.list()

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

    CALL gds.beta.model.list()

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
    list_model_catalog_query  = """
        CALL gds.beta.model.list()
    """

    # Create the driver session
    with driver.session() as session:
        # Run query
        results = session.run(list_model_catalog_query).data()

        # Prettify the results
        print(json.dumps(results, indent=2, sort_keys=True, default=default))

</div>

</div>

</div>

</div>

</div>

</div>

</div>

</div>

<div>

## Save a model to disk

<div>

<div>

The `gds.alpha.model.store` procedure can be used to persist a model to
disk. This is useful both to keep models for later reuse and to free up
memory.

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
<p>Not all the models can be saved to disk. A list of the supported models can be found on the <a>GDS manual</a>.</p>
</div>
<div>
<p><strong>If a model cannot be saved to disk, it will be lost when the AuraDS instance is restarted.</strong></p>
</div>
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

    result = gds.alpha.model.store(model)

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

    CALL gds.alpha.model.store("example_graph_model_for_graphsage")

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
    save_graph_sage_model_to_disk_query = """
        CALL gds.alpha.model.store("example_graph_model_for_graphsage")
    """

    # Create the driver session
    with driver.session() as session:
        # Run query
        result = session.run(save_graph_sage_model_to_disk_query).data()

        # Prettify the result
        print(json.dumps(result, indent=2, sort_keys=True))

</div>

</div>

</div>

</div>

</div>

</div>

<div>

If we list the model catalog again after persisting a model, we can see
that the `stored` flag for that model has been set to `true`.

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

    results = gds.beta.model.list()

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

    CALL gds.beta.model.list()

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
    list_model_catalog_query  = """
        CALL gds.beta.model.list()
    """

    # Create the driver session
    with driver.session() as session:
        # Run query
        results = session.run(list_model_catalog_query).data()

        # Prettify the results
        print(json.dumps(results, indent=2, sort_keys=True, default=default))

</div>

</div>

</div>

</div>

</div>

</div>

</div>

</div>

<div>

## Share a model with other users

<div>

<div>

After a model has been created, it can be useful to make it available to
other users for different use cases.

</div>

<div>

<div>

<table>
<tbody><tr>
<td>
<i></i>
</td>
<td>
A model can only be shared with other users of the same AuraDS instance.
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

### Create a new user

<div>

In order to see how this works in practice on AuraDS, we first of all
need to create another user to share the model with.

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

    # Switch to the "system" database to run the
    # "CREATE USER" admin command
    gds.set_database("system")

    gds.run_cypher("""
        CREATE USER testUser IF NOT EXISTS
        SET PASSWORD 'password'
        SET PASSWORD CHANGE NOT REQUIRED
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

    :connect system

    CREATE USER testUser IF NOT EXISTS
    SET PASSWORD 'password'
    SET PASSWORD CHANGE NOT REQUIRED

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
    create_a_new_user_query = """
        CREATE USER testUser IF NOT EXISTS
        SET PASSWORD 'password'
        SET PASSWORD CHANGE NOT REQUIRED
    """

    # Create the driver session using the "system" database
    with driver.session(database="system") as session:
        # Run query
        result = session.run(create_a_new_user_query).data()

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

### Publish the model

<div>

A model can be *published* (made accessible to other users) using the
`gds.alpha.model.publish` procedure. Upon publication, the model name is
updated by appending `_public` to its original name.

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

    # Switch back to the default "neo4j" database
    # to publish the model
    gds.set_database("neo4j")

    model_public = gds.alpha.model.publish(model)

    print(model_public)

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

    :connect neo4j

    CALL gds.alpha.model.publish('example_graph_model_for_graphsage')

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
    publish_graph_sage_model_to_disk_query  = """
        CALL gds.alpha.model.publish('example_graph_model_for_graphsage')
    """

    # Create the driver session
    with driver.session() as session:
        # Run query
        result = session.run(publish_graph_sage_model_to_disk_query).data()

        # Prettify the result
        print(json.dumps(result, indent=2, sort_keys=True, default=default))

</div>

</div>

</div>

</div>

</div>

</div>

</div>

<div>

### View the model as a different user

<div>

In order to verify that the published model is visible to the user we
have just created, we need to create a new client (or driver) session.
We can then use it to run the `gds.beta.model.list` procedure again
under the new user and verify that the model is included in the list.

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

    test_user_gds = GraphDataScience(
        AURA_CONNECTION_URI,
        auth=("testUser", "password"),
        aura_ds=True
    )

    results = test_user_gds.beta.model.list()

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

    // First, open a new Cypher shell with the following command:
    //
    // ./cypher-shell -a $AURA_CONNECTION_URI -u testUser -p password

    CALL gds.beta.model.list()

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

    test_user_driver = GraphDatabase.driver(
        AURA_CONNECTION_URI,
        auth=("testUser", "password")
    )

    # Create the driver session
    with test_user_driver.session() as session:
        # Run query
        results = session.run(list_model_catalog_query).data()

        # Prettify the results
        print(json.dumps(results, indent=2, sort_keys=True, default=default))

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

The in-memory graphs, the data in the Neo4j database, the models, and
the test user can now all be deleted.

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

    # Delete the example dataset
    gds.run_cypher("""
        MATCH (example:ExampleData)
        DETACH DELETE example
    """)

    # Delete the projected graph from memory
    gds.graph.drop(g)

    # Drop the model from memory
    gds.beta.model.drop(model_public)

    # Delete the model from disk
    gds.alpha.model.delete(model_public)

    # Switch to the "system" database to delete the example user
    gds.set_database("system")

    gds.run_cypher("""
        DROP USER testUser
    """)View all (6 more lines)

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

    // Delete the example dataset from the database
    MATCH (example:ExampleData)
    DETACH DELETE example;

    // Delete the projected graph from memory
    CALL gds.graph.drop("example_graph_for_graphsage");

    // Drop the model from memory
    CALL gds.beta.model.drop("example_graph_model_for_graphsage_public");

    // Delete the model from disk
    CALL gds.alpha.model.delete("example_graph_model_for_graphsage_public");

    // Delete the example user
    DROP USER testUser;

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

    # Delete the example dataset from the database
    delete_example_graph_query = """
        MATCH (example:ExampleData)
        DETACH DELETE example
    """

    # Delete the projected graph from memory
    drop_in_memory_graph_query = """
        CALL gds.graph.drop("example_graph_for_graphsage")
    """

    # Drop the model from memory
    drop_example_models_query = """
        CALL gds.beta.model.drop("example_graph_model_for_graphsage_public")
    """

    # Delete the model from disk
    delete_example_models_query = """
        CALL gds.alpha.model.delete("example_graph_model_for_graphsage_public")
    """

    # Delete the example user
    drop_example_user_query = """
        DROP USER testUser
    """

    # Create the driver session
    with driver.session() as session:
        # Run queries
        print(session.run(delete_example_graph_query).data())
        print(session.run(drop_in_memory_graph_query).data())
        print(session.run(drop_example_models_query).data())
        print(session.run(delete_example_models_query).data())

    # Create another driver session on the system database
    # to drop the test user
    with driver.session(database='system') as session:
        print(session.run(drop_example_user_query).data())

    driver.close()
    test_user_driver.close()View all (26 more lines)

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
