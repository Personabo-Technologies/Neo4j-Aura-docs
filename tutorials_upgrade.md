<div>

<div>

# Upgrade to Neo4j 5 within Aura

</div>

<div>

<div>

<div>

This tutorial describes how to upgrade an Aura instance running Neo4j
version 4 to Neo4j version 5.

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
<p>New AuraDS and AuraDB Free instances use Neo4j 5 as standard, while all others give the option to choose between Neo4j 4 and 5 during creation.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

</div>

</div>

<div>

## Prepare for the upgrade

<div>

<div>

### Drivers

<div>

Neo4j's official drivers have some significant and breaking changes
between versions you need to be aware of. For a smooth migration:

</div>

<div>

1.  Check the breaking changes for each driver you use, for example in
    the Python driver and in the GDS client.

2.  Make sure you switch to the latest version of the driver in line
    with the version of the Neo4j database. This can be done before
    upgrading the version of Neo4j that you are using with Aura, as 5.x
    drivers are backward compatible.

</div>

<div>

The Update and migration guide contains all information and lists all
the breaking changes.

</div>

</div>

<div>

### Indexes

<div>

In Neo4j 5, BTREE indexes are replaced by RANGE, POINT, and TEXT
indexes. Before migrating a database, in Neo4j 4, you should create a
matching RANGE, POINT, or TEXT index for each BTREE index (or
index-backed constraint). You can run `SHOW INDEXES` on your Neo4j 4
database to display its indexes.

</div>

<div>

In most cases, RANGE indexes can replace BTREE. However, there might be
occasions when a different index type is more suitable, such as:

</div>

<div>

-   Use POINT indexes if the property value type is `point` and
    `distance` or `bounding box` queries are used for the property.

-   Use TEXT indexes if the property value type is `text` and the values
    can be larger than 8Kb.

-   Use TEXT indexes if the property value type is `text` and `CONTAINS`
    and `ENDS WITH` are used in queries for the property.

</div>

<div>

After creating the new index, the old index should be dropped. The
following example shows how to create a new RANGE index and drop an
existing `index_name` index:

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

    CREATE RANGE INDEX range_index_name FOR (n:Label) ON (n.prop1);
    DROP INDEX index_name;

</div>

</div>

<div>

The following example instead shows how to create a constraint backed by
a RANGE index:

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

    CREATE CONSTRAINT constraint_with_provider FOR (n:Label) REQUIRE (n.prop1) IS UNIQUE OPTIONS {indexProvider: 'range-1.0'}

</div>

</div>

<div>

For more information about creating indexes, see Cypher Manual →
Creating indexes.

</div>

</div>

<div>

### Cypher updates

<div>

Neo4j 5 introduces some changes to the Cypher syntax and error handling.

</div>

<div>

#### Cypher syntax

<div>

All changes in the Cypher language syntax are detailed in Cypher Manual
→ Removals, deprecations, additions and extensions. Thoroughly review
this section in the version you are moving to and make the necessary
changes in your code.

</div>

<div>

Here is a short list of the main changes introduced in Neo4j 5:

</div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th><strong>Deprecated feature</strong></th>
<th><strong>Details</strong></th>
</tr>
</thead>
<tbody>
<tr>
<td><div><div>
<div>
<div><div><span></span><div><span>Copied!</span></div></div></div><pre><code><span>MATCH</span> (n)-[r:<span>REL</span>]-&gt;(m) <span>SET</span> n=r</code></pre>
</div>
</div></div></td>
<td><div><div>
<p>Use the <code>properties()</code> function instead to get the map of properties of nodes/relationships that can then be used in a <code>SET</code> clause:</p>
</div>
<div>
<div>
<div><div><span></span><div><span>Copied!</span></div></div></div><pre><code><span>MATCH</span> (n)-[r:<span>REL</span>]-&gt;(m) <span>SET</span> n=properties(r)</code></pre>
</div>
</div></div></td>
</tr>
<tr>
<td><div><div>
<div>
<div><div><span></span><div><span>Copied!</span></div></div></div><pre><code><span>MATCH</span> (a), (b),<span> allShortestPaths((a)</span>-[r]-&gt;(b)) <span>RETURN</span> b

<span>MATCH</span> (a), (b),<span> shortestPath((a)</span>-[r]-&gt;(b)) <span>RETURN</span> b</code></pre>
</div>
</div></div></td>
<td><div><div>
<p><code>shortestPath</code> and <code>allShortestPaths</code> without <a>variable-length relationship</a> are deprecated. Instead, use a <code>MATCH</code> with a <code>LIMIT</code> of 1 or:</p>
</div>
<div>
<div>
<div><div><span></span><div><span>Copied!</span></div></div></div><pre><code><span>MATCH</span> (a), (b),<span> shortestPath((a)</span>-[r*<span>1.</span><span>.1</span>]-&gt;(b)) <span>RETURN</span> b</code></pre>
</div>
</div></div></td>
</tr>
<tr>
<td><div><div>
<div>
<div><div><span></span><div><span>Copied!</span></div></div></div><pre><code><span>CREATE</span> DATABASE databaseName.withDot ...</code></pre>
</div>
</div></div></td>
<td><div><div>
<p>Creating a database with unescaped dots in the name has been deprecated, instead escape the database name:</p>
</div>
<div>
<div>
<div><div><span></span><div><span>Copied!</span></div></div></div><pre><code><span>CREATE</span> DATABASE <span>`databaseName.withDot`</span> ...</code></pre>
</div>
</div></div></td>
</tr>
</tbody>
</table>

</div>

</div>

<div>

#### Error/Warning/Info handling in Cypher

<div>

Many semantic errors that Cypher finds are reported as
`Neo.ClientError.Statement.SyntaxError` even though they are semantic
and not syntax errors. In Neo4j 5, the metadata returned by Cypher
queries is improved.

</div>

<div>

-   The severity of some of the Warning codes is moved to Info:

    <div>

    -   `SubqueryVariableShadowingWarning` → `SubqueryVariableShadowing`

    -   `NoApplicableIndexWarning` → `NoApplicableIndex`

    -   `CartesianProductWarning` → `CartesianProduct`

    -   `DynamicPropertyWarning` → `DynamicProperty`

    -   `EagerOperatorWarning` → `EagerOperator`

    -   `ExhustiveShortestPathWarning` → `ExhaustiveShortestPath`

    -   `UnboundedVariableLengthPatternWarning` →
        `UnboundedVariableLengthPattern`

    -   `ExperimentalFeature` → `RuntimeExperimental`

    </div>

</div>

</div>

</div>

<div>

### APOC

<div>

All APOC procedures and functions available in Aura are listed in the
APOC Core library. See the APOC documentation for further details.

</div>

</div>

<div>

### Procedures

<div>

Some procedures have been replaced by commands:

</div>

<div>

<table>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Procedure</th>
<th>Replacement</th>
</tr>
</thead>
<tbody>
<tr>
<td><p><code>db.indexes</code></p></td>
<td><p><code>SHOW INDEXES</code> command</p></td>
</tr>
<tr>
<td><p><code>db.indexDetails</code></p></td>
<td><p><code>SHOW INDEXES YIELD *</code> command</p></td>
</tr>
<tr>
<td><p><code>db.schemaStatements</code></p></td>
<td><p><code>SHOW INDEXES YIELD *</code> command and <code>SHOW CONSTRAINTS YIELD *</code> command</p></td>
</tr>
<tr>
<td><p><code>db.constraints</code></p></td>
<td><p><code>SHOW CONSTRAINTS</code> command</p></td>
</tr>
<tr>
<td><p><code>db.createIndex</code></p></td>
<td><p><code>CREATE INDEX</code> command</p></td>
</tr>
<tr>
<td><p><code>db.createUniquePropertyConstraint</code></p></td>
<td><p><code>CREATE CONSTRAINT …​ IS UNIQUE</code> command</p></td>
</tr>
<tr>
<td><p><code>db.index.fulltext.createNodeIndex</code></p></td>
<td><p><code>CREATE FULLTEXT INDEX</code> command</p></td>
</tr>
<tr>
<td><p><code>db.index.fulltext.createRelationshipIndex</code></p></td>
<td><p><code>CREATE FULLTEXT INDEX</code> command</p></td>
</tr>
<tr>
<td><p><code>db.index.fulltext.drop</code></p></td>
<td><p><code>DROP INDEX</code> command</p></td>
</tr>
<tr>
<td><p><code>dbms.procedures</code></p></td>
<td><p><code>SHOW PROCEDURES</code> command</p></td>
</tr>
<tr>
<td><p><code>dbms.functions</code></p></td>
<td><p><code>SHOW FUNCTIONS</code> command</p></td>
</tr>
<tr>
<td><p><code>dbms.listTransactions</code></p></td>
<td><p><code>SHOW TRANSACTIONS</code> command</p></td>
</tr>
<tr>
<td><p><code>dbms.killTransaction</code></p></td>
<td><p><code>TERMINATE TRANSACTIONS</code> command</p></td>
</tr>
<tr>
<td><p><code>dbms.killTransactions</code></p></td>
<td><p><code>TERMINATE TRANSACTIONS</code> command</p></td>
</tr>
<tr>
<td><p><code>dbms.listQueries</code></p></td>
<td><p><code>SHOW TRANSACTIONS</code> command</p></td>
</tr>
<tr>
<td><p><code>dbms.killQuery</code></p></td>
<td><p><code>TERMINATE TRANSACTIONS</code> command</p></td>
</tr>
<tr>
<td><p><code>dbms.killQueries</code></p></td>
<td><p><code>TERMINATE TRANSACTIONS</code> command</p></td>
</tr>
<tr>
<td><p><code>dbms.scheduler.profile</code></p></td>
<td><p>-</p></td>
</tr>
</tbody>
</table>

</div>

<div>

Refer to the Update and migration guide for a full list of removals and
deprecations.

</div>

</div>

<div>

### Neo4j Connectors

<div>

If you are using a Neo4j Connector for Apache Spark or Apache Kafka,
make sure its version is compatible with Neo4j 5.

</div>

<div>

The Neo4j BI Connectors available on the Download center are compatible
with Neo4j 5.

</div>

</div>

</div>

</div>

<div>

## Perform the upgrade

<div>

<div>

Once you have prepared your Neo4j 4 Aura instance, you are ready to
migrate the instance to a new or existing Neo4j 5 instance.

</div>

<div>

### Clone

<div>

If you have an existing Neo4j 5 instance, you can use the **Clone To
Existing** instance action on your Neo4j 4 AuraDB or AuraDS instance.

</div>

<div>

If you do not have an existing Neo4j 5 instance, you can use the **Clone
To New** instance action on your Neo4j 4 AuraDB or AuraDS instance.

</div>

</div>

<div>

### Export and Import

<div>

Alternatively, you can **Export** a snapshot dump file from your Neo4j 4
AuraDB or AuraDS instance, create a new Neo4j 5 instance manually, and
then import the dump file into your new Neo4j 5 AuraDB or AuraDS
instance.

</div>

</div>

</div>

</div>

</div>
