<div>

<div>

# Connecting to an instance

</div>

<div>

<div>

<div>

There are a few different methods of connecting to an instance in Neo4j
AuraDB:

</div>

<div>

-   Neo4j Browser - A browser-based interface for querying and viewing
    data in an instance.

-   Neo4j Bloom - A graph exploration application for visually
    interacting with graph data.

-   Neo4j Desktop - An installable desktop application used to manage
    local and cloud instances.

-   Neo4j Cypher Shell - A command-line tool used to run cypher queries
    against a Neo4j instance.

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
<p>For first-time users, we recommend using Neo4j Browser.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

</div>

</div>

<div>

## Neo4j Browser

<div>

<div>

You can query an instance using Neo4j Browser.

</div>

<div>

To open an instance with Browser:

</div>

<div>

1.  Navigate to the Neo4j Aura Console in your browser.

2.  Select the **Query** button on the instance you want to open.

3.  Enter the **Username** and **Password** credentials in the Neo4j
    Browser window that opens. These are the same credentials you stored
    when creating the instance.

4.  Select **Connect**.

</div>

<div>

Once you have successfully connected, there are built-in guides you can
complete to familiarize yourself with Neo4j Browser.

</div>

<div>

For more information on using Neo4j Browser, please see the Browser
manual.

</div>

</div>

</div>

<div>

## Neo4j Bloom

<div>

<div>

You can explore an instance using Neo4j Bloom.

</div>

<div>

To open an instance with Bloom:

</div>

<div>

1.  Navigate to the Neo4j Aura Console in your browser.

2.  Select the **Explore** button on the instance you want to open.

3.  Select **Neo4j Bloom** from the dropdown menu.

4.  Enter the **Username** and **Password** credentials in the Neo4j
    Browser window that opens. These are the same credentials you stored
    when creating the instance.

5.  Select **Connect**.

</div>

<div>

For more details on using Neo4j Bloom, please see the Neo4j Bloom
documentation.

</div>

<div>

<div>

<table>
<tbody><tr>
<td>
<i></i>
</td>
<td>
<div>Perspectives in AuraDB</div>
<div>
<p>Due to the nature of AuraDB’s infrastructure, it is not currently possible to share Perspectives in Bloom, as the data for a given Perspective is stored in local storage in the user’s web browser.</p>
</div>
<div>
<p>An alternative is to export your Perspective as a JSON file and import it into another Bloom session.</p>
</div>
<div>
<p>To export a Perspective:</p>
</div>
<div>
<ol>
<li>
<p>Open the Bloom interface for your Neo4j AuraDB instance.</p>
</li>
<li>
<p>Navigate to the <em>Perspectives Gallery</em>.</p>
</li>
<li>
<p>Click on the vertical ellipsis (<strong>…​</strong>) and select <strong>Export</strong>.</p>
</li>
<li>
<p>Save the file to your local disk.</p>
</li>
</ol>
</div>
<div>
<p>You can import perspectives by clicking the blue "Import Perspective" button in the Perspective gallery.
Please note that the Perspective exposes details about your graph’s schema but not the actual data within.</p>
</div>
<div>
<p>For more information, see <a>Bloom Perspectives</a>.</p>
</div>
<div>
<p><strong>Deep links</strong></p>
</div>
<div>
<p>As data for a given Perspective is stored in local storage in the user’s web browser, if you want to access a deep link referencing perspectives, you will first need to import the perspectives into your local instance of Bloom.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

</div>

</div>

<div>

## Neo4j Desktop

<div>

<div>

You can connect AuraDB instances to the Neo4j Desktop application,
allowing the ability to have a single portal for interacting with all
instances of Neo4j, whether local or located in the cloud.

</div>

<div>

To connect to an instance using Neo4j Desktop:

</div>

<div>

1.  Navigate to the Neo4j Aura Console in your browser.

2.  Copy the **Connection URI** of the instance you want to connect to.
    The URI is below the instance status indicator.

3.  In Neo4j Desktop, select the **Projects** tab and select an existing
    project or create a new one.

4.  Select the **Add** dropdown and choose **Remote connection**.

5.  Enter a name for the instance and enter the URL from the Neo4j Aura
    console from the second step. Once complete, select **Next**.

6.  With **Username/Password** selected, enter your credentials and
    select **Next**. These are the same credentials you stored when
    creating the instance.

7.  When available, activate the connection by clicking the **Connect**
    button.

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
<ul>
<li>
<p>Neo4j Desktop only allows 1 connection at a time to an instance (local or remote).</p>
</li>
<li>
<p>Deactivating an instance in Neo4j Desktop won’t shut it down or stop a remote instance - it will only temporarily close the connection to it in Neo4j Desktop.</p>
</li>
</ul>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

As with other instances in Neo4j Desktop, you can install Graph Apps for
monitoring and other functionality.

</div>

<div>

To do this, follow the same process to install the graph application you
need, and open it from Neo4j Desktop or a web browser with the running
and activated Neo4j AuraDB instance.

</div>

</div>

</div>

<div>

## Neo4j Cypher Shell

<div>

<div>

You can connect to an AuraDB instance using the Neo4j Cypher Shell
command-line interface (CLI) and run cypher commands against your
instance from the command-line.

</div>

<div>

To connect to an instance using Neo4j Cypher Shell:

</div>

<div>

1.  Navigate to the Neo4j Aura Console in your browser.

2.  Copy the **Connection URI** of the instance you want to connect to.
    The URI is below the instance status indicator.

3.  Open a terminal and navigate to the folder where you have installed
    Cypher Shell.

4.  Run the following `cypher-shell` command replacing:

    <div>

    -   **`<connection_uri>`** with the URI you copied in step 2.

    -   **`<username>`** with the username for your instance.

    -   **`<password>`** with the password for your instance.

        <div>

        <div>

        <div>

        <div>

        <div>

        Copied!

        </div>

        </div>

        </div>

            ./cypher-shell -a <connection_uri> -u <username> -p <password>

        </div>

        </div>

    </div>

</div>

<div>

Once connected, you can run `:help` for a list of available commands.

</div>

<div>

<div>

    Available commands:
      :begin    Open a transaction
      :commit   Commit the currently open transaction
      :exit     Exit the logger
      :help     Show this help message
      :history  Print a list of the last commands executed
      :param    Set the value of a query parameter
      :params   Print all currently set query parameters and their values
      :rollback Rollback the currently open transaction
      :source   Interactively executes cypher statements from a file
      :use      Set the active instance

    For help on a specific command type:
        :help command

</div>

</div>

<div>

For more information on Cypher Shell, including how to install it,
please see the Cypher Shell documentation.

</div>

</div>

</div>

</div>
