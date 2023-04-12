<div>

<div>

# Loading CSV files

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

A CSV file can be loaded into an AuraDS instance using the `LOAD CSV`
Cypher clause. For security reasons it is not possible to load local CSV
files, which must be instead publicly accessible on HTTP or HTTPS
servers such as GitHub, Google Drive, and Dropbox. Another way to make
CSV files available is to upload them to a cloud bucket storage (such as
Google Cloud Storage or Amazon S3) and configure the bucket as a static
website.

</div>

<div>

In this example we will load three CSV files:

</div>

<div>

-   `movies.csv`: a list of movies with their title, release year and a
    short description

-   `people.csv`: a list of actors with their year of birth

-   `actors.csv`: a list of acting roles, where actors are matched with
    the movies they had a role in

</div>

<div>

<div>

<table>
<tbody><tr>
<td>
<i></i>
</td>
<td>
<strong>Warning</strong>: The <code>LOAD CSV</code> command is built to handle small to medium-sized data sets, such as anything up to 10 million nodes and relationships. You should avoid using this command for any data sets exceeding this limit.
</td>
</tr>
</tbody></table>

</div>

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

## Create constraints

<div>

<div>

Adding constraints before loading any data usally improves data loading
performance. In fact, besides adding an integrity check, a unique
constraint adds an index on a property at the same time, so that `MATCH`
and `MERGE` operations during loading are faster.

</div>

<div>

<div>

<table>
<tbody><tr>
<td>
<i></i>
</td>
<td>
<strong>Warning</strong>: For best performance when using <code>MERGE</code> or <code>MATCH</code> with <code>LOAD CSV</code>, make sure an index or a unique constraint has been created on the property used for merging. For more information, follow the <a>Import data</a> tutorial in the Cypher documentation.
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

In this example we add uniqueness constraints on both movie titles and
actors\' names.

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

    # Make movie titles unique
    gds.run_cypher("""
        CREATE CONSTRAINT FOR (movie:Movie) REQUIRE movie.title IS UNIQUE
    """)

    # Make person names unique
    gds.run_cypher("""
        CREATE CONSTRAINT FOR (person:Person) REQUIRE person.name IS UNIQUE
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

    CREATE CONSTRAINT FOR (movie:Movie) REQUIRE movie.title IS UNIQUE;
    CREATE CONSTRAINT FOR (person:Person) REQUIRE person.name IS UNIQUE;

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

    movie_title_constraint = """
        CREATE CONSTRAINT FOR (movie:Movie) REQUIRE movie.title IS UNIQUE
    """

    person_name_constraint = """
        CREATE CONSTRAINT FOR (person:Person) REQUIRE person.name IS UNIQUE
    """

    # Create the driver session
    with driver.session() as session:
        # Make movie titles unique
        session.run(movie_title_constraint).data()
        # Make person names unique
        session.run(person_name_constraint).data()

</div>

</div>

</div>

</div>

</div>

</div>

</div>

</div>

<div>

## Add nodes from CSV files

<div>

<div>

We are now ready to load the CSV files from their URIs and create nodes
from the data they contain. In the following examples, `LOAD CSV` is
used with `WITH HEADERS` to access `row` fields by their corresponding
column name. Furthermore:

</div>

<div>

-   `MERGE` is used with the indexed properties to take advantage of the
    constraints created in the Create constraints section.

-   `ON CREATE SET` is used to set the value of a node property when a
    new one is created.

-   `RETURN count(*)` is used to show the number of processed rows.

</div>

<div>

Note that the CSV files in this example are curated, so some assumptions
are made for simplicity. In a real-world scenario, for example, a CSV
file could contain multiple rows that would attempt to assign different
property values to the same node; in this case, an `ON MATCH SET` clause
must be added to ensure this case is dealt with appropriately.

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
        LOAD CSV
          WITH HEADERS
          FROM 'https://data.neo4j.com/intro/movies/movies.csv' AS row
        MERGE (m:Movie {title: row.title})
          ON CREATE SET m.released = toInteger(row.released), m.tagline = row.tagline
        RETURN count(*)
    """)

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

    gds.run_cypher("""
        LOAD CSV
          WITH HEADERS
          FROM 'https://data.neo4j.com/intro/movies/people.csv' AS row
        MERGE (p:Person {name: row.name})
          ON CREATE SET p.born = toInteger(row.born)
        RETURN count(*)
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

    LOAD CSV
      WITH HEADERS
      FROM 'https://data.neo4j.com/intro/movies/movies.csv' AS row
    MERGE (m:Movie {title: row.title})
      ON CREATE SET m.released = toInteger(row.released), m.tagline = row.tagline
    RETURN count(*);

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

    LOAD CSV
      WITH HEADERS
      FROM 'https://data.neo4j.com/intro/movies/people.csv' AS row
    MERGE (p:Person {name: row.name})
      ON CREATE SET p.born = toInteger(row.born)
    RETURN count(*);

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

    load_movies_csv = """
        LOAD CSV
          WITH HEADERS
          FROM 'https://data.neo4j.com/intro/movies/movies.csv' AS row
        MERGE (m:Movie {title: row.title})
          ON CREATE SET m.released = toInteger(row.released), m.tagline = row.tagline
        RETURN count(*)
    """

    # Create the driver session
    with driver.session() as session:
        # Load the CSV file
        session.run(load_movies_csv).data()

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

    load_people_csv = """
        LOAD CSV
          WITH HEADERS
          FROM 'https://data.neo4j.com/intro/movies/people.csv' AS row
        MERGE (p:Person {name: row.name})
          ON CREATE SET p.born = toInteger(row.born)
        RETURN count(*)
    """

    # Create the driver session
    with driver.session() as session:
        # Load the CSV file
        session.run(load_people_csv).data()

</div>

</div>

</div>

</div>

</div>

</div>

</div>

</div>

<div>

## Add relationships from CSV files

<div>

<div>

Similarly to what we have done for nodes, we now create relationships
from the `actors.csv` file. In the following examples, `LOAD CSV` is
used with:

</div>

<div>

-   `WITH HEADERS` to access `row` fields by their corresponding column
    name;

-   `USING PERIODIC COMMIT` is used to control memory usage by creating
    a commit every *n* processed rows rather than after processing the
    whole file. This is especially useful when loading large files;

-   `FIELDTERMINATOR` is used to explicitly set the field terminator
    character (although the comma is the default).

</div>

<div>

Furthermore:

</div>

<div>

-   `MATCH` and `MERGE` are used to find nodes (taking advantage of the
    constraints created in the Create constraints section) and create a
    relationship between them.

-   `ON CREATE SET` is used to set the value of a relationship property
    when a new one is created.

-   `RETURN count(*)` is used to show the number of processed rows.

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
        USING PERIODIC COMMIT 50
        LOAD CSV
          WITH HEADERS
          FROM 'https://data.neo4j.com/intro/movies/actors.csv' AS row
          FIELDTERMINATOR ','
        MATCH (p:Person {name: row.person})
        MATCH (m:Movie {title: row.movie})
        MERGE (p)-[actedIn:ACTED_IN]->(m)
          ON CREATE SET actedIn.roles = split(row.roles, ';')
        RETURN count(*)
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

    USING PERIODIC COMMIT 50
    LOAD CSV
      WITH HEADERS
      FROM 'https://data.neo4j.com/intro/movies/actors.csv' AS row
      FIELDTERMINATOR ','
    MATCH (p:Person {name: row.person})
    MATCH (m:Movie {title: row.movie})
    MERGE (p)-[actedIn:ACTED_IN]->(m)
      ON CREATE SET actedIn.roles = split(row.roles, ';')
    RETURN count(*)

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

    load_actors_csv = """
        USING PERIODIC COMMIT 50
        LOAD CSV
          WITH HEADERS
          FROM 'https://data.neo4j.com/intro/movies/actors.csv' AS row
          FIELDTERMINATOR ','
        MATCH (p:Person {name: row.person})
        MATCH (m:Movie {title: row.movie})
        MERGE (p)-[actedIn:ACTED_IN]->(m)
          ON CREATE SET actedIn.roles = split(row.roles, ';')
        RETURN count(*)
    """

    # Create the driver session
    with driver.session() as session:
        # Load the CSV file
        session.run(load_actors_csv).data()

</div>

</div>

</div>

</div>

</div>

</div>

</div>

</div>

<div>

## Run a Cypher query

<div>

<div>

Once all the nodes and relationships have been created, we can run a
query to check that the data have been inserted correctly. The following
query looks for movies with Keanu Reeves, orders them by release date
and groups their titles.

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
        MATCH (person:Person {name: "Keanu Reeves"})-[:ACTED_IN]->(movie)
        RETURN movie.released, COLLECT(movie.title) AS movies
        ORDER BY movie.released
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

    MATCH (person:Person {name: "Keanu Reeves"})-[:ACTED_IN]->(movie)
    RETURN movie.released, COLLECT(movie.title) AS movies
    ORDER BY movie.released

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

    query = """
        MATCH (person:Person {name: "Keanu Reeves"})-[:ACTED_IN]->(movie)
        RETURN movie.released, COLLECT(movie.title) AS movies
        ORDER BY movie.released
    """

    # Create the driver session
    with driver.session() as session:
        # Run the Cypher query
        session.run(query).data()

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

When the data are no longer useful, the database can be cleaned up.

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

    # Delete data
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

    MATCH (n)
    DETACH DELETE n

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

    delete_data = """
        MATCH (n)
        DETACH DELETE n
    """

    # Create the driver session
    with driver.session() as session:
        # Delete the data
        session.run(delete_data).data()

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

</div>
