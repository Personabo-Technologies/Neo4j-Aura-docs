<div>

<div>

# Logs

</div>

<div>

<div>

<div>

Aura allows you to request and download security and query logs.

</div>

<div>

You can access logs from an Aura instance via the **Logs** tab.

</div>

<div>

To access the **Logs** tab:

</div>

<div>

1.  Navigate to the Neo4j Aura Console in your browser.

2.  Select the instance you want to export the logs from.

3.  Select the **Logs** tab.

</div>

</div>

</div>

<div>

## Query logs

<div>

<div>

A query log provides a log of queries executed on an instance within a
specified time range.

</div>

<div>

### Requesting query logs

<div>

To request a query log from the **Logs** tab:

</div>

<div>

1.  Click **Request log**.

2.  Select the **Query Log** option under **Type**.

3.  Select a **Range** option.

4.  Click **Request**.

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
<p>Requested logs will appear for up to 7 days, at which point they will expire and be removed.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

You can select from the following time ranges when requesting a query
log:

</div>

<div>

-   Last 15 minutes

-   Last hour

-   Custom range - Any range up to one hour from the previous 30 days

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
<p>We recommend shorter time ranges for busy, read/write heavy instances to reduce request time.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

Aura will generate a query log for your selected time range, available
to download once the **Status** shows **Completed**.

</div>

</div>

<div>

### Downloading query logs

<div>

You can download query logs by selecting the download icon on the
right-hand side of the log entry.

</div>

<div>

Downloaded query logs take the form of a zipped JSON file that, when
extracted, contains the following information:

</div>

<div>

<table>
<caption>Table 1. Query log entries</caption>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><p><code>allocatedBytes</code></p></td>
<td><p>The number of bytes allocated by the query.</p></td>
</tr>
<tr>
<td><p><code>annotationData</code></p></td>
<td><p>The metadata attached to the transaction.</p></td>
</tr>
<tr>
<td><p><code>authenticatedUser</code></p></td>
<td><p>The name of the user who executed the query (whose credentials were used to log in).</p></td>
</tr>
<tr>
<td><p><code>database</code></p></td>
<td><p>The name of the database the query was executed on.</p></td>
</tr>
<tr>
<td><p><code>dbid</code></p></td>
<td><p>The ID of the instace the query was executed on.</p></td>
</tr>
<tr>
<td><p><code>elapsedTimeMs</code></p></td>
<td><p>The time the query took to complete in milliseconds.</p></td>
</tr>
<tr>
<td><p><code>event</code></p></td>
<td><p>The query event:</p>
<p><code>start</code> - The query was successfully parsed, awaiting execution.</p>
<p><code>fail</code> - The query failed to either parse or execute.</p>
<p><code>success</code> - The query executed successfully or was canceled.</p></td>
</tr>
<tr>
<td><p><code>executingUser</code></p></td>
<td><p>The name of the user who executed the query either through authentication (<code>authenticatedUser</code>) or through <a>impersonation</a>.</p></td>
</tr>
<tr>
<td><p><code>id</code></p></td>
<td><p>The ID of the query.</p></td>
</tr>
<tr>
<td><p><code>message</code></p></td>
<td><p>The log message: a truncated version of <code>query</code>.</p></td>
</tr>
<tr>
<td><p><code>pageFaults</code></p></td>
<td><p>The number of page faults resulting from the query.</p></td>
</tr>
<tr>
<td><p><code>pageHits</code></p></td>
<td><p>The number of page hits resulting from the query.</p></td>
</tr>
<tr>
<td><p><code>query</code></p></td>
<td><p>The full query text.</p></td>
</tr>
<tr>
<td><p><code>runtime</code></p></td>
<td><p>The <a>Cypher runtime</a> used to execute the query.</p></td>
</tr>
<tr>
<td><p><code>type</code></p></td>
<td><p>The type of log message.</p></td>
</tr>
<tr>
<td><p><code>time</code></p></td>
<td><p>The timestamp of the log message.</p></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

</div>

<div>

## Security logs

<div>

<div>

AuraDB Enterprise AuraDS Enterprise

</div>

<div>

A security log provides a log of all the security events that have
occurred on an instance within a specified time range.

</div>

<div>

Security events include:

</div>

<div>

-   Login attempts: both successful and unsuccessful.

-   Authorization failures from role-based access control.

-   Administration commands run against the `system` database.

</div>

<div>

### Requesting security logs

<div>

To request a security log from the **Logs** tab:

</div>

<div>

1.  Click **Request log**.

2.  Select the **Security Log** option under **Type**.

3.  Select a **Range** option.

4.  Click **Request**.

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
<p>Requested logs will appear for up to 7 days, at which point they will expire and be removed.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

You can select from the following time ranges when requesting a security
log:

</div>

<div>

-   Last 6 hours

-   Last 12 hours

-   Custom range - Any range up to 12 hours from the previous 30 days

</div>

<div>

Aura will generate a security log for your selected time range,
available to download once the **Status** shows **Completed**.

</div>

</div>

<div>

### Downloading security logs

<div>

You can download security logs by selecting the download icon on the
right-hand side of the log entry.

</div>

<div>

Downloaded security logs take the form of a zipped JSON file that, when
extracted, contains the following information:

</div>

<div>

<table>
<caption>Table 2. Security log entries</caption>
<colgroup>
<col/>
<col/>
</colgroup>
<thead>
<tr>
<th>Name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td><p><code>authenticatedUser</code></p></td>
<td><p>The name of the user who executed the security event (whose credentials were used to log in).</p></td>
</tr>
<tr>
<td><p><code>dbid</code></p></td>
<td><p>The ID of the instance the security event occurred on.</p></td>
</tr>
<tr>
<td><p><code>executingUser</code></p></td>
<td><p>The name of the user who executed the security event either through authentication (<code>authenticatedUser</code>) or through <a>impersonation</a>.</p></td>
</tr>
<tr>
<td><p><code>message</code></p></td>
<td><p>The log message.</p></td>
</tr>
<tr>
<td><p><code>type</code></p></td>
<td><p>The type of log message.</p></td>
</tr>
<tr>
<td><p><code>time</code></p></td>
<td><p>The timestamp of the log message.</p></td>
</tr>
</tbody>
</table>

</div>

</div>

</div>

</div>

</div>
