<div>

<div>

# Architecture

</div>

<div>

<div>

<div>

AuraDS makes it easy to run graph algorithms on Neo4j by integrating two
main components:

</div>

<div>

-   **Neo4j Database**, where graph data are loaded and stored, and
    Cypher queries and all database operations (for example user
    management, query termination, etc.) are executed;

-   **Graph Data Science**, a software component installed in the Neo4j
    Database, whose main purpose is to run graph algorithms on in-memory
    projections of Neo4j Database data.

</div>

</div>

</div>

<div>

## Graph Data Science concepts

<div>

<div>

Graph Data Science (GDS) includes procedures to project and manage
graphs, run algorithms, and train machine learning models.

</div>

<div>

<div>

Graph Catalog

</div>

The graph catalog is used to store and manage projected graphs via GDS
procedures.

</div>

<div>

<div>

Algorithms

</div>

GDS contains many graph algorithms, invoked as Cypher procedures and run
on projected graphs.

</div>

<div>

GDS algorithms are broken down into three tiers of maturity:

</div>

<div>

-   **Alpha**: experimental algorithms that may be changed or removed at
    any time. Algorithms in this tier are prefixed with
    `gds.alpha.<algorithm>`.

-   **Beta**: algorithms promoted from the Alpha tier to candidates for
    the Production tier. Algorithms in this tier are prefixed with
    `gds.beta.<algorithm>`.

-   **Production**: algorithms that have been rigorously tested for
    stability and scalability. Algorithms in this tier are prefixed with
    `gds.<algorithm>`.

</div>

<div>

<div>

Model Catalog

</div>

Some machine learning algorithms (for example Node Classification and
GraphSage) need to use trained models in their computation. The model
catalog is used to store and manage named trained models.

</div>

<div>

<div>

Pipeline Catalog

</div>

The pipeline catalog is used to manage machine learning pipelines. A
pipeline groups together all the stages of a supported machine learning
task (for example Node classification), from graph feature extraction to
model training, in a single end-to-end workflow.

</div>

</div>

</div>

<div>

## Graph data flow

<div>

<div>

Since GDS algorithms can only run in memory, the typical data flow
involves:

</div>

<div>

1.  Reading the graph data from Neo4j Database

2.  Loading (*projecting*) the data into an in-memory graph

3.  Running an algorithm on a projected graph

4.  Writing the results back to Neo4j Database (if the algorithm runs in
    write mode)

</div>

<div>

<div>

</div>

</div>

</div>

</div>

</div>
