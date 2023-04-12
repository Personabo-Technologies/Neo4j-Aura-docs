<div>

<div>

# Migrate from self-managed Neo4j to Aura

</div>

<div>

<div>

<div>

This tutorial describes how to migrate from a self-managed Neo4j
database to Aura.

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
<p>If your local Neo4j version is older than 4.3, you need to upgrade to at least Neo4j 4.3 first as explained in <a>Upgrade and Migration Guide → Neo4j 4 upgrades and migration</a>.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

</div>

</div>

<div>

## Preparation

<div>

<div>

### Migrating to Neo4j 5

<div>

If you are migrating from self-managed Neo4j 4.3 or 4.4 to Neo4j 5 on
Aura, carefully read the Preparation section in the Upgrade tutorial to
ensure you are well prepared for the migration.

</div>

</div>

<div>

### Aura instance size

<div>

Before starting, verify that the Aura instance you are migrating to is
sized accordingly. The instance must be at least as large as your
self-managed database to accommodate the data. The Aura RAM-to-storage
ratio is 1:2, which means, for example, that a 32 GB Aura instance
provides 64 GB of storage.

</div>

</div>

<div>

### APOC compatibility

<div>

If you are using any APOC procedures and functions, make sure they are
all available in Aura by checking the APOC support page.

</div>

</div>

</div>

</div>

<div>

## Creating and uploading a database dump

<div>

<div>

In order to move data from your self-managed database to Aura, you need
to create a dump of the existing database.

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
<p>This process requires a short downtime for your self-managed database.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

The following admin commands must be invoked with the same user as your
self-managed Neo4j database. This guarantees that Neo4j has full rights
to start and work with the database files you use.

</div>

<div>

1.  Stop your self-managed Neo4j database. If you are running an
    Enterprise Edition, you can stop only the database you want to dump
    using the command `STOP DATABASE neo4j` in Cypher Shell or Browser.

2.  Ensure the target directory to store the database dumps (for
    instance `/dumps/neo4j`) exists.

3.  Depending on your self-managed Neo4j version, create a dump of your
    database (e.g., `neo4j`) using one of the following options:

    <div>

    -   From Neo4j 4
    -   From Neo4j 5

    <div>

    <div>

    <div>

    <div>

    Use the `neo4j-admin dump` command.

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

        bin/neo4j-admin dump --database=neo4j --to=/dumps/neo4j

    </div>

    </div>

    </div>

    </div>

    <div>

    <div>

    <div>

    Use the `neo4j-admin database dump` command.

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

        bin/neo4j-admin database dump neo4j --to-path=/dumps/neo4j

    </div>

    </div>

    </div>

    </div>

    </div>

    </div>

4.  Depending on your self-managed Neo4j version, upload the database
    dump (e.g., `neo4j`) to your Aura instance using one of the
    following options:

    <div>

    -   From Neo4j 4
    -   From Neo4j 5

    <div>

    <div>

    <div>

    <div>

    Use the `neo4j-admin push-to-cloud` command.

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

        bin/neo4j-admin push-to-cloud --dump=/dumps/neo4j/file.dump --bolt-uri=neo4j+s://xxxxxxxx.databases.neo4j.io --overwrite

    </div>

    </div>

    </div>

    </div>

    <div>

    <div>

    <div>

    Use the `neo4j-admin database upload` command.

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

        bin/neo4j-admin database upload neo4j --from-path=/dumps/neo4j --to-uri=neo4j+s://xxxxxxxx.databases.neo4j.io --overwrite-destination=true

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
