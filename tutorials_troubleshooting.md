<div>

<div>

# Troubleshooting

</div>

<div>

<div>

<div>

This page provides possible solutions to several common issues you may
encounter when using Neo4j Aura.

</div>

<div>

Regardless of the issue, viewing the Aura query log is always
recommended to monitor processes and verify any problems.

</div>

</div>

</div>

<div>

## Query performance

<div>

<div>

### `MemoryLimitExceededException`

<div>

During regular operations of your Aura instance, you may at times see
that some of your queries fail with the error:

</div>

<div>

<div>

MemoryLimitExceededException error

</div>

<div>

<div>

<div>

MemoryLimitExceededException error

</div>

</div>

    org.neo4j.memory.MemoryLimitExceededException: The allocation of an extra 8.3 MiB would use more than the limit 278.0 MiB.
    Currently using 275.1 MiB. dbms.memory.transaction.global_max_size threshold reached

</div>

</div>

<div>

The `org.neo4j.memory.MemoryLimitExceededException` configuration acts
as a safeguard, limiting the quantity of memory allocated to all
transactions while preserving the regular operations of the Aura
instance. Similarly, the property
`dbms.memory.transaction.global_max_size` also aims to protect the Aura
Instance from experiencing any OOMs (OutOfMemory exceptions) and
increase resiliency. It is enabled in Aura and cannot be disabled.

</div>

<div>

However, the measured heap usage of all transactions is only an estimate
and may differ from the actual number. The estimation algorithm relies
on a conservative approach, which can lead to overestimations of memory
usage. In such cases, all contributing objects\' identities are unknown
and cannot be assumed to be shared.

</div>

<div>

Solution

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
<p>We recommend handling this error in your application code, as it may be intermittent.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

Overestimations are most likely to happen when using `UNWIND` on long
lists or when expanding a variable length or shortest path pattern. The
many relationships shared between the computed result paths could be the
cause of a lack of precision in the estimation algorithm.

</div>

<div>

To avoid this scenario, try running the same query without using a
sorting operation like `ORDER BY` or `DISTINCT`. Additionally, if
possible, handle this ordering or uniqueness in your application.

</div>

<div>

If removing the `ORDER BY` or `DISTINCT` clauses does not solve the
issue, the primary mitigation for this error is to perform one or more
of these actions:

</div>

<div>

-   Handle this exception in your code and be prepared to retry if this
    is an intermittent error. Keep in mind that the query can succeed
    regardless.

-   Rework the relevant query to optimize it.

    <div>

    -   Use `EXPLAIN` or `PROFILE` to review the plans (see more about
        query tuning).

    -   Use `PROFILE` in cypher-shell to check the overall memory
        footprint of a query. The output will include memory consumption
        information, the query's result, if any, and the execution plan.
        In the following example, the memory consumed is 11,080 Bytes:

        <div>

        <div>

        </div>

        </div>

    </div>

-   Increase the instance size of your Aura deployment to get more
    resources.

-   Reduce the concurrency of queries heavy on resources to get a better
    chance of success.

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
<p>If this error occurs while loading data from CSV files, use <code>apoc.periodic.iterate</code> to import the data and use a relatively small number for the <code>batch_size</code> parameter.
Read more information about <a>Using apoc to conditional loading large scale data set from JSON or CSV files</a>.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

See Considerations on memory configuration for further reading on memory
management.

</div>

</div>

</div>

</div>

<div>

## Neo4j Admin database upload errors

<div>

<div>

The `database upload` command was introduced in Neo4j Admin version 5,
replacing the `push-to-cloud` command that was present in Neo4j Admin
version 4.4 and earlier. The following solutions are relevant to both
commands.

</div>

<div>

### `LegacyIndexes`

<div>

When attempting to use `database upload` where there are native
`LegacyIndexes` present, the request might fail with the following
error:

</div>

<div>

<div>

LegacyIndexes error

</div>

<div>

<div>

<div>

LegacyIndexes error

</div>

</div>

    ERROR: Source dumpfile has legacy indexes enabled, which we do not support.
    User needs to manually follow instructions in neo4j logs to upgrade indexes.

</div>

</div>

<div>

Solution

:   To resolve the issue, follow these steps:

    <div>

    1.  Make sure you are at least on Neo4j version 4.4 or later. See
        more information about upgrade and migration.

    2.  In your local graph, use the following commands to get a list of
        the indexes and their types. This will also provide the
        sequential list of commands to drop and then recreate the
        indexes:

        <div>

        <div>

        Return a list of indexes and their types

        </div>

        <div>

        <div>

        <div>

        Return a list of indexes and their types

        </div>

        <div>

        <div>

        Copied!

        </div>

        </div>

        </div>

            CALL db.constraints() YIELD description
            UNWIND ["DROP", "CREATE"] AS command
            RETURN command + " " + description

        </div>

        </div>

    3.  In Neo4j Browser, select the \"Enable multi statement query
        editor\" option under the browser settings.

    4.  Take the list of commands from the 2nd step and copy them in one
        list of multiple queries into Browser and run those queries.

    5.  After the indexes are recreated, attempt the `database upload`
        command again.

    </div>

</div>

</div>

<div>

### `InconsistentData`

<div>

This error message will likely trigger when Neo4j Aura cannot safely
load the data provided due to inconsistencies.

</div>

<div>

Solution

:   If you encounter this error, please raise a ticket with our Customer
    Support team.

</div>

</div>

<div>

### `UnsupportedStoreFormat`

<div>

You may get this error if the store you are uploading is in a Neo4j
version that is not directly supported in Neo4j Aura.

</div>

<div>

Solution

:   <div>

    1.  Upgrade your database. Make sure you are on Neo4j 4.4 or later.

    2.  If you encounter problems upgrading, please raise a ticket with
        our Customer Support team.

    </div>

</div>

</div>

<div>

### `LogicalRestrictions`

<div>

You may get this error when the store you are uploading exceeds the
logical limits of your database.

</div>

<div>

Solution

:   <div>

    1.  Delete nodes and relationships to ensure the data is within the
        specified limits for your instance, and try the upload again.

    2.  If you are confident you have not exceeded these limits, please
        raise a ticket with our Customer Support team.

    </div>

</div>

</div>

<div>

### `Fallback`

<div>

This error can be triggered when the uploaded file is not recognized as
a valid Neo4j dump file.

</div>

<div>

Solution

:   <div>

    1.  Check the file and try again.

    2.  If you are confident the file being uploaded is correct, please
        raise a ticket with our Customer Support team.

    </div>

</div>

</div>

</div>

</div>

<div>

## Driver integration

<div>

<div>

### JavaScript routing table error

<div>

JavaScript driver version 4.4.5 and greater assumes the existence of
database connectivity. When the connection fails, the two most common
error messages are \"Session Expired\" or a routing table error:

</div>

<div>

<div>

Routing table error

</div>

<div>

<div>

<div>

Routing table error

</div>

</div>

    Neo4jError: Could not perform discovery.
    No routing servers available.
    Known routing table: RoutingTable[database=default database, expirationTime=0, currentTime=1644933316983, routers=[], readers=[], writers=[]]

</div>

</div>

<div>

This error can also be encountered when no default database is defined.

</div>

<div>

Solution

:   Verify connectivity before creating a session object, and specify
    the default database in your driver definition.

</div>

<div>

<div>

Verifying connectivity

</div>

<div>

<div>

<div>

Verifying connectivity

</div>

<div>

<div>

Copied!

</div>

</div>

</div>

    const session = driver.session({ database: "neo4j" })
    driver.verifyConnectivity()

    let session = driver.session(....)

</div>

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
<p>Rapid session creation can exceed the database’s maximum concurrent connection limit, resulting in the “Session Expired” error when creating more sessions.</p>
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
