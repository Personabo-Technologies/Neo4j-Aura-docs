<div>

<div>

# Using the Apache Spark Connector

</div>

<div>

<div>

<div>

In this tutorial we use the Neo4j Connector for Apache Spark to write to
and read graph data from an Aura instance.

</div>

</div>

</div>

<div>

## Setup

<div>

<div>

1.  Download Spark from the Download page (latest version, for example
    3.3.0, pre-built for Apache Hadoop 3.3 and later).

2.  Download the Spark Neo4j Connector from the GitHub release page.

    <div>

    <div>

    <table>
<tbody><tr>
<td>
<i></i>
</td>
<td>
<div>
<p>Make sure to match both the Spark version and the Scala version.</p>
</div>
</td>
</tr>
</tbody></table>

    </div>

    </div>

3.  Decompress the downloaded file and launch the Spark shell as
    follows:

    <div>

    <div>

    <div>

    <div>

    <div>

    Copied!

    </div>

    </div>

    </div>

        $ spark-3.3.0-bin-hadoop3/bin/spark-shell --jars neo4j-connector-apache-spark_2.12-4.1.3_for_spark_3.jar

    </div>

    </div>

</div>

</div>

</div>

<div>

## Running code in Spark

<div>

<div>

<div>

<table>
<tbody><tr>
<td>
<i></i>
</td>
<td>
<div>
<p>Scala code can be copy-pasted in the Spark shell by activating the <code>paste</code> mode with the <code>:paste</code> command.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

First of all, we need to create a Spark session and set the Aura
connection credentials:

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

    import org.apache.spark.sql.{SaveMode, SparkSession}

    val spark = SparkSession.builder().getOrCreate()

    // Replace with the actual connection URI and credentials
    val url = "neo4j+s://xxxxxxxx.databases.neo4j.io"
    val username = "neo4j"
    val password = ""

</div>

</div>

<div>

Then, we create the `Person` class and a Spark `Dataset` with some
example data:

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

    case class Person(name: String, surname: String, age: Int)

    // Create example Dataset
    val ds = Seq(
        Person("John", "Doe", 42),
        Person("Jane", "Doe", 40)
    ).toDS()

</div>

</div>

<div>

We can now write the data to Aura:

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

    // Write to Neo4j
    ds.write.format("org.neo4j.spark.DataSource")
        .mode(SaveMode.Overwrite)
        .option("url", url)
        .option("authentication.basic.username", username)
        .option("authentication.basic.password", password)
        .option("labels", ":Person")
        .option("node.keys", "name,surname")
        .save()

</div>

</div>

<div>

The written data can be queried and visualized using the Neo4j Browser.
We can also read the data back from Aura:

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

    // Read from Neo4j
    val data = spark.read.format("org.neo4j.spark.DataSource")
        .option("url", url)
        .option("authentication.basic.username", username)
        .option("authentication.basic.password", password)
        .option("labels", "Person")
        .load()

    data.show()

</div>

</div>

<div>

For further information on how to use the connector, check the Neo4j
Spark Connector docs.

</div>

</div>

</div>

</div>
