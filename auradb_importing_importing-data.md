<div>

<div>

# Importing data

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
<div>
<p>The process of importing or loading data requires you to <a>create an AuraDB instance</a> beforehand.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

There are two ways you can import data from a ***.csv*** file into an
AuraDB instance:

</div>

<div>

-   Load CSV - A Cypher statement that you run from Neo4j Browser or
    Neo4j Cypher Shell.

-   Neo4j Data Importer - A visual application that you launch from the
    Console.

</div>

</div>

</div>

<div>

## Load CSV

<div>

<div>

The `LOAD CSV` Cypher statement can be used from within Neo4j Browser
and Cypher Shell. For instructions on how to open an AuraDB instance
with Browser or Cypher Shell, see Connecting to an instance.

</div>

<div>

There are some limitations to consider when using this method to load a
***.csv*** file into an AuraDB instance:

</div>

<div>

-   For security reasons, you must host your ***.csv*** file on a
    publicly accessible HTTP or HTTPS server. Examples of such servers
    include GitHub, Google Drive, and Dropbox.

-   The `LOAD CSV` command is built to handle small to medium-sized data
    sets, such as anything up to 10 million nodes and relationships. You
    should avoid using this command for any data sets exceeding this
    limit.

</div>

</div>

</div>

<div>

## Neo4j Data Importer

<div>

<div>

Neo4j Data Importer is a no-code tool that lets you:

</div>

<div>

1.  Load data from flat files (`.csv` and `.tsv`).

2.  Define a graph model and map data to it.

3.  Import the data into an AuraDB instance.

</div>

<div>

To load data with Neo4j Data Importer:

</div>

<div>

1.  Navigate to the Neo4j Aura Console in your browser.

2.  Select the **Import** button on the instance you want to open.

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
<p>You must provide your AuraDB instance password before importing from the Neo4j Data Importer.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

</div>

</div>

</div>
