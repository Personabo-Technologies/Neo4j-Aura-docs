<div>

<div>

# Projecting graphs and using the Graph Catalog

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

-   load Neo4j on-disk data into in-memory projected graphs;

-   use the Graph Catalog to manage projected graphs.

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

## Load data from Neo4j with native projections

<div>

<div>

Native projections are used to load into memory a graph stored on disk.
The `gds.graph.project` procedure allows to project a graph by selecting
the node labels, relationship types and properties to be projected.

</div>

<div>

The `gds.graph.project` procedure can use a \"shorthand syntax\", where
the nodes and relationships projections are simply passed as single
values or arrays, or an \"extended syntax\", where each node or
relationship projection has its own configuration. The extended syntax
is especially useful if additional transformation of the data or the
graph structure are needed. Both methods are shown in this section,
using the following graph as an example.

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

    # Cypher query to create an example graph on disk
    gds.run_cypher("""
        MERGE (a:EngineeringManagement {name: 'Alistair'})
        MERGE (j:EngineeringManagement {name: 'Jennifer'})
        MERGE (d:Developer {name: 'Leila'})
        MERGE (a)-[:MANAGES {start_date: 987654321}]->(d)
        MERGE (j)-[:MANAGES {start_date: 123456789, end_date: 987654321}]->(d)
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

    MERGE (a:EngineeringManagement {name: 'Alistair'})
    MERGE (j:EngineeringManagement {name: 'Jennifer'})
    MERGE (d:Developer {name: 'Leila'})
    MERGE (a)-[:MANAGES {start_date: 987654321}]->(d)
    MERGE (j)-[:MANAGES {start_date: 123456789, end_date: 987654321}]->(d)

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

    # Cypher query to create an example graph on disk
    write_example_graph_query = """
        MERGE (a:EngineeringManagement {name: 'Alistair'})
        MERGE (j:EngineeringManagement {name: 'Jennifer'})
        MERGE (d:Developer {name: 'Leila'})
        MERGE (a)-[:MANAGES {start_date: 987654321}]->(d)
        MERGE (j)-[:MANAGES {start_date: 123456789, end_date: 987654321}]->(d)
    """

    # Create the driver session
    with driver.session() as session:
        session.run(write_example_graph_query)

</div>

</div>

</div>

</div>

</div>

</div>

<div>

### Project using the shorthand syntax

<div>

In this example we use the shorthand syntax to simply project all node
labels and relationship types.

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

    # Project a graph using the shorthand syntax
    shorthand_graph, result = gds.graph.project(
        "shorthand-example-graph",
        ["EngineeringManagement", "Developer"],
        ["MANAGES"]
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
      'shorthand-example-graph',
      ['EngineeringManagement', 'Developer'],
      ['MANAGES']
    )
    YIELD graphName, nodeCount, relationshipCount
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

    shorthand_graph_create_call = """
        CALL gds.graph.project(
          'shorthand-example-graph',
          ['EngineeringManagement', 'Developer'],
          ['MANAGES']
        )
        YIELD graphName, nodeCount, relationshipCount
        RETURN *
    """

    # Create the driver session
    with driver.session() as session:
        # Call to project a graph using the shorthand syntax
        result = session.run(shorthand_graph_create_call).data()

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

### Project using the extended syntax

<div>

In this example we use the extended syntax for node and relationship
projections to:

</div>

<div>

-   transform the `EngineeringManagement` and `Developer` labels to
    `PersonEM` and `PersonD` respectively;

-   transform the *directed* `MANAGES` relationship into the `KNOWS`
    *undirected* relationship;

-   keep the `start_date` and `end_date` relationship properties, adding
    a default value of `999999999` to `end_date`.

</div>

<div>

The projected graph becomes the following:

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

    (:PersonEM {first_name: 'Alistair'})-
      [:KNOWS {start_date: 987654321, end_date: 999999999}]-
      (:PersonD {first_name: 'Leila'})-
      [:KNOWS {start_date: 123456789, end_date: 987654321}]-
      (:PersonEM {first_name: 'Jennifer'})

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

    # Project a graph using the extended syntax
    extended_form_graph, result = gds.graph.project(
        "extended-form-example-graph",
        {
            "PersonEM": {
                "label": "EngineeringManagement"
            },
            "PersonD": {
                "label": "Developer"
            }
        },
        {
            "KNOWS": {
                "type": "MANAGES",
                "orientation": "UNDIRECTED",
                "properties": {
                    "start_date": {
                        "property": "start_date"
                    },
                    "end_date": {
                        "property": "end_date",
                        "defaultValue": 999999999
                    }
                }
            }
        }
    )

    print(result)View all (14 more lines)

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
      'extended-form-example-graph',
      {
        PersonEM: {
          label: 'EngineeringManagement'
        },
        PersonD: {
          label: 'Developer'
        }
      },
      {
        KNOWS: {
          type: 'MANAGES',
          orientation: 'UNDIRECTED',
          properties: {
            start_date: {
              property: 'start_date'
            },
            end_date: {
              property: 'end_date',
              defaultValue: 999999999
            }
          }
        }
      }
    )
    YIELD graphName, nodeCount, relationshipCount
    RETURN *View all (13 more lines)

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

    extended_form_graph_create_call = """
        CALL gds.graph.project(
          'extended-form-example-graph',
          {
            PersonEM: {
              label: 'EngineeringManagement'
            },
            PersonD: {
              label: 'Developer'
            }
          },
          {
            KNOWS: {
              type: 'MANAGES',
              orientation: 'UNDIRECTED',
              properties: {
                start_date: {
                  property: 'start_date'
                },
                end_date: {
                  property: 'end_date',
                  defaultValue: 999999999
                }
              }
            }
          }
        )
        YIELD graphName, nodeCount, relationshipCount
        RETURN *
    """

    # Create the driver session
    with driver.session() as session:
        # Call to project a graph using the extended syntax
        result = session.run(extended_form_graph_create_call).data()

        # Prettify the results
        print(json.dumps(result, indent=2, sort_keys=True))View all (23 more lines)

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

## Use the Graph Catalog

<div>

<div>

The Graph Catalog can be used to retrieve information on and manage the
projected graphs.

</div>

<div>

### List all the graphs

<div>

The `gds.graph.list` procedure can be used to list all the graphs
currently stored in memory.

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

    # List all in-memory graphs
    all_graphs = gds.graph.list()

    print(all_graphs)

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

    CALL gds.graph.list()

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

    show_in_memory_graphs_call = """
        CALL gds.graph.list()
    """

    # Create the driver session
    with driver.session() as session:
        # Run the Cypher procedure
        results = session.run(show_in_memory_graphs_call).data()

        # Prettify the results
        print(json.dumps(results, indent=2, sort_keys=True, default=default))

</div>

</div>

</div>

</div>

</div>

</div>

</div>

<div>

### Check that a graph exists

<div>

The `gds.graph.exists` procedure can be called to check for the
existence of a graph by its name.

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

    # Check whether the "shorthand-example-graph" graph exists in memory
    graph_exists = gds.graph.exists("shorthand-example-graph")

    print(graph_exists)

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

    CALL gds.graph.exists('example-graph')

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

    check_graph_exists_call = """
        CALL gds.graph.exists('example-graph')
    """

    # Create the driver session
    with driver.session() as session:
        # Run the Cypher procedure and print the result
        print(session.run(check_graph_exists_call).data())

</div>

</div>

</div>

</div>

</div>

</div>

</div>

<div>

### Drop a graph

<div>

When a graph is no longer needed, it can be dropped to free up memory
using the `gds.graph.drop` procedure.

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

    # Drop a graph object and keep the result of the call
    result = gds.graph.drop(shorthand_graph)

    # Print the result
    print(result)

    # Drop a graph object and just print the result of the call
    gds.graph.drop(extended_form_graph)

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

    CALL gds.graph.drop('shorthand-example-graph');

    CALL gds.graph.drop('extended-form-example-graph');

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

    delete_shorthand_graph_call = """
        CALL gds.graph.drop('shorthand-example-graph')
    """

    delete_extended_form_graph_call = """
        CALL gds.graph.drop('extended-form-example-graph')
    """

    # Create the driver session
    with driver.session() as session:
        # Drop a graph and keep the result of the call
        result = session.run(delete_shorthand_graph_call).data()

        # Prettify the result
        print(json.dumps(result, indent=2, sort_keys=True, default=default))

        # Drop a graph discarding the result of the call
        session.run(delete_extended_form_graph_call).data()View all (3 more lines)

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

When the projected graphs are dropped, the underlying data on the disk
are not deleted. If such data are no longer needed, they need to be
deleted manually via a Cypher query.

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

    # Delete on-disk data
    gds.run_cypher("""
        MATCH (example)
        WHERE example:EngineeringManagement OR example:Developer
        DETACH DELETE example
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

    MATCH (example)
    WHERE example:EngineeringManagement OR example:Developer
    DETACH DELETE example;

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

    delete_example_graph_query = """
        MATCH (example)
        WHERE example:EngineeringManagement OR example:Developer
        DETACH DELETE example
    """

    # Create the driver session
    with driver.session() as session:
        # Run Cypher call
        print(session.run(delete_example_graph_query).data())

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
