<div>

<div>

# Neo4j Connector for Apache Spark

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
<p>Tutorial: <a>Using the Apache Spark Connector with Aura</a></p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

The Neo4j Connector for Apache Spark is intended to make integrating
graphs with Spark easy. There are two ways to use the connector:

</div>

<div>

-   As a data source: read any set of nodes or relationships as a
    `DataFrame` in Spark

-   As a sink: write any `DataFrame` to Neo4j as a collection of nodes
    or relationships, or use a Cypher statement to process records
    contained in a `DataFrame` into the graph pattern of your choice

</div>

<div>

Connecting to Aura only requires to make a few changes to the Neo4j
driver configuration:

</div>

<div>

1.  Replace the `bolt` URI (the value of the `neo4j.server.uri`
    configuration parameter) with the `neo4j+s://` connection URI from
    the Aura instance detail page

2.  Update the username and password configuration parameters as
    appropriate

</div>

<div>

For more information check the Neo4j Apache Spark Connector page.

</div>

</div>
