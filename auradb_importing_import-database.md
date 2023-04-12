<div>

<div>

# Importing an existing database

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

There are two ways you can import data from an existing Neo4j database
into an Aura instance.

</div>

<div>

The easiest way is to export a Neo4j database as a ***.dump*** file and
use the Import database process. This process, however, only works for
***.dump*** files under 4GB.

</div>

<div>

If the size of the ***.dump*** file exported from a database is greater
than 4GB, you must use the Neo4j Admin `database upload` method.

</div>

</div>

</div>

<div>

## Import database

<div>

<div>

To import a ***.dump*** file under 4GB:

</div>

<div>

1.  Navigate to the Neo4j Aura Console in your browser.

2.  Select the instance you want to import the data.

3.  Select the **Import Database** tab.

4.  Drag and drop your ***.dump*** file into the provided window or
    select **Select a .dump file** and select your file.

5.  Select **Upload**.

</div>

<div>

When the upload is complete, the instance goes into a `Loading` state as
the dump is applied. Once this has finished, the instance returns to its
`Running` state; and the data is ready.

</div>

</div>

</div>

<div>

## Neo4j Admin `database upload`

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
<p>This command does not currently support <a>private linking</a>. Please <a>raise a support ticket</a> if you have public traffic disabled and need to use this command.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

`database upload` is a Neo4j Admin command that you can run to upload
the contents of a Neo4j database into an Aura instance, regardless of
the database's size.

</div>

<div>

For details of how to use the `neo4j-admin database upload` command,
along with a full list of options, see Upload to Neo4j Aura.

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
<p>The <code>database upload</code> command was introduced in Neo4j Admin version 5, replacing the <code>push-to-cloud</code> command that was present in Neo4j Admin version 4.4 and earlier. If you have an earlier version of the Neo4j Admin tool, please see the <a>Neo4j Admin push-to-cloud documentation</a>.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

</div>

</div>

</div>
