<div>

<div>

# Using the BI Connector

</div>

<div>

<div>

<div>

In this tutorial we use the Neo4j Connector for BI to read graph data
from an Aura instance using some common SQL clients and BI tools.

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
<p>This tutorial includes instructions on the usage of third-party software, which may be subject to changes beyond our control. In case of doubt, please refer to the third-party software documentation.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

</div>

</div>

<div>

## Downloading the connector

<div>

<div>

Download the connector from the Download Center. Depending on the SQL
client or BI tool it will be used with, you will need either the JDBC or
the ODBC connector; see the usage examples for further details.

</div>

</div>

</div>

<div>

## Preparing example data

<div>

<div>

Before trying the connector with any of the listed tools, some data
needs to be loaded on Aura. This can be achieved by running the
following Cypher query in the Neo4j Browser:

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

    CREATE
      (john:Person {name: "John", surname: "Doe", age: 42}),
      (jane:Person {name: "Jane", surname: "Doe", age: 40}),
      (john)-[:KNOWS]->(jane)

</div>

</div>

</div>

</div>

<div>

## Using command-line SQL clients

<div>

<div>

In order to run SQL queries, we need a SQL client that can use a custom
driver. Common JDBC-based command-line SQL clients include sqlline and
jdbcsql.

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
<p>The correct protocol to use for connection via a JDBC driver is <code>neo4j</code> (not <code>neo4j+s</code>). Make sure to add the <code>SSL=true</code> parameter to the URL.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

### sqlline

<div>

`sqlline` is a command-line tool for issuing SQL queries to relational
databases via JDBC. To clone and build it, run the following:

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

    $ git clone https://github.com/julianhyde/sqlline
    $ cd sqlline
    $ ./mvnw package

</div>

</div>

<div>

We now need to make the BI connector driver available to `sqllite`. This
can be done by extracting the `Neo4jJDBC42.jar` file from the downloaded
*JDBC BI connector* into the `sqlline/target` folder.

</div>

<div>

The `sqlline` client can now be run as follows:

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

    $ ./bin/sqlline -d com.simba.neo4j.neo4j.jdbc42.Driver

</div>

</div>

<div>

From the client prompt, it is possible to connect to the Aura instance
by supplying the username and password when prompted to do so:

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

    sqlline> !connect jdbc:neo4j://xxxxxxxx.databases.neo4j.io?SSL=true

</div>

</div>

<div>

When the connection is established, a list of tables can be obtained
with the `!tables` command:

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

    jdbc:neo4j://xxxxxxxx.databases.neo4j.io> !tables

</div>

</div>

<div>

<div>

    +-----------+--------------+---------------------+------------+---------+----------+------------+-----------+--------+
    | TABLE_CAT | TABLE_SCHEM  |     TABLE_NAME      | TABLE_TYPE | REMARKS | TYPE_CAT | TYPE_SCHEM | TYPE_NAME | SELF_R |
    +-----------+--------------+---------------------+------------+---------+----------+------------+-----------+--------+
    | neo4j     | Node         | Person              | TABLE      |         |          |            |           |        |
    | neo4j     | Relationship | Person_KNOWS_Person | TABLE      |         |          |            |           |        |
    +-----------+--------------+---------------------+------------+---------+----------+------------+-----------+--------+

</div>

</div>

<div>

It is also possible to run SQL queries:

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

    jdbc:neo4j://xxxxxxxx.databases.neo4j.io> SELECT * FROM Person;

</div>

</div>

<div>

<div>

    +----------+-----+------+---------+
    | _NodeId_ | age | name | surname |
    +----------+-----+------+---------+
    | 0        | 42  | John | Doe     |
    | 1        | 40  | Jane | Doe     |
    +----------+-----+------+---------+

</div>

</div>

</div>

<div>

### jdbcsql

<div>

jdbcsql is a command-line tool that can be used to connect to a DBMS via
a JDBC driver.

</div>

<div>

After downloading the `jdbcsql-1.0.zip` file from SourceForge, extract
it into the `jdbcsql` folder; then, copy the `Neo4jJDBC42.jar` file from
the downloaded *JDBC BI Connector* into `jdbcsql` and make the following
changes:

</div>

<div>

1.  Add the following lines to `JDBCConfig.properties`

    <div>

    <div>

        # neo4j settings
        neo4j_driver = com.simba.neo4j.neo4j.jdbc42.Driver
        neo4j_url = jdbc:neo4j://host?SSL=true

    </div>

    </div>

2.  Add `Neo4jJDBC42.jar` to `Rsrc-Class-Path` line in
    `META-INF/MANIFEST.MF`

</div>

<div>

Now run the following command (replacing `xxxxxxxx.databases.neo4j.io`
with the Aura connection URI, and `yyyyyyyy` with the actual password):

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

    $ java org.eclipse.jdt.internal.jarinjarloader.JarRsrcLoader -m neo4j -h xxxxxxxx.databases.neo4j.io -d neo4j -U neo4j -P yyyyyyyy 'SELECT * FROM Person'

</div>

</div>

<div>

The result of the query is:

</div>

<div>

<div>

    "_NodeId_" age name    surname
    0   42  John    Doe
    1   40  Jane    Doe

</div>

</div>

</div>

</div>

</div>

<div>

## Using BI tools

<div>

<div>

Commonly used BI tools include Tableau (which uses the JDBC driver) and
Power BI (which uses the ODBC driver).

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
<p>The correct protocol to use for connection via a JDBC driver is <code>neo4j</code> (not <code>neo4j+s</code>). Make sure to add the <code>SSL=true</code> parameter to the URL.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

### Tableau

<div>

<div>

<table>
<tbody><tr>
<td>
<i></i>
</td>
<td>
<div>
<p>This example requires <a>Tableau Desktop</a>.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

After downloading the JDBC Neo4j Connector for BI from the Download
Center:

</div>

<div>

-   Close any running instances of Tableau Desktop.

-   Copy the Neo4j driver to the appropriate Tableau drivers folder
    (e.g. `C:\Program Files\Tableau\Drivers` on Windows, or
    `~/Library/Tableau/Drivers` on macOS).

-   Start Tableau and search for the `Other Databases (JDBC)` option.

-   Insert the Aura URL as
    `jdbc:neo4j://xxxxxxxx.databases.neo4j.io?SSL=true`, leave the SQL
    dialect as `SQL92`, and complete the relevant credentials.

</div>

<div>

After the connection is established, it is possible to select the
`neo4j` database and the `Node` schema to find the `Person` table. The
table can then be explored to find the example data.

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
<p>For more information on how to add a JDBC database to Tableau, please refer to the <a>Tableau documentation</a>.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

</div>

<div>

### Power BI

<div>

<div>

<table>
<tbody><tr>
<td>
<i></i>
</td>
<td>
<div>
<p>This example requires Microsoft Windows and <a>Power BI Desktop</a>.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

After downloading and installing the ODBC Neo4j Connector for BI from
the Download Center:

</div>

<div>

-   Open Power BI Desktop.

-   Search for `ODBC` in the **Get data from another source** panel.

-   Select `Simba Neo4j` in the **DSN dropdown** menu.

-   Insert the connection string
    `Host=xxxxxxxx.databases.neo4j.io;SSL=1` in the **Advanced options**
    section.

</div>

<div>

Once connected, open sequentially `ODBC` → `neo4j` → `Node` → `Person`
in the **Navigator** window to see a preview of the table.

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
<p>For more information on how to add an ODBC database to Power BI, check the <a>Power BI documentation</a>.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

</div>

</div>

</div>

</div>
