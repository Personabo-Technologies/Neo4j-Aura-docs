<div>

<div>

# Neo4j Connector for BI

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
<p>Tutorial: <a>Using the BI Connector with Aura</a></p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

The Neo4j Connector for Business Intelligence (BI) delivers access to
Neo4j graph data from BI tools such as Tableau, Power BI, Looker, TIBCO,
Spotfire Server, Microstrategy, and more. It can be used to run SQL
queries on a Neo4j graph and retrieve data in tabular format.

</div>

<div>

The connection to Aura requires the usage of the `SSL` parameter in the
connection string. For example, if the connection URI of the Aura
instance is `neo4j+s://xxxxxxxx.databases.neo4j.io`, the following
connection strings must be used:

</div>

<div>

-   **With JDBC**: `jdbc:neo4j://xxxxxxxx.databases.neo4j.io?SSL=true`
    (note the usage of the `neo4j` protocol instead of `neo4j+s`)

-   **With ODBC**: `Host=xxxxxxxx.databases.neo4j.io;SSL=1`

</div>

<div>

The Neo4j Connector for BI can be downloaded from the Download Center.

</div>

</div>
