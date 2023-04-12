<div>

<div>

# Neo4j Connector for Apache Kafka

</div>

<div>

Many users and customers want to integrate Kafka and other streaming
solutions with Neo4j, either to ingest data into the graph from other
sources or to send update events to the event log for later consumption.
Aura supports the use of the Kafka Connect Neo4j Connector, which allows
you to ingest data into Neo4j from Kafka topics or send change events
from Neo4j into Kafka topics.

</div>

<div>

Connecting to Aura only requires to make a few changes to the source and
sink configuration examples:

</div>

<div>

-   Replace the `bolt` URI in the examples (the value of the
    `neo4j.server.uri` configuration parameter) with the `neo4j+s://`
    connection URI from the Aura instance detail page

-   Update the username and password configuration parameters as
    appropriate

</div>

<div>

For more information check the Kafka Connect Neo4j Connector user guide.

</div>

</div>
