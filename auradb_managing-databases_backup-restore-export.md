<div>

<div>

# Backup, export and restore

</div>

<div>

<div>

<div>

The data in your AuraDB instance can be backed up, exported, and
restored using snapshots.

</div>

<div>

A snapshot is a copy of the data in an instance at a specific point in
time.

</div>

<div>

The **Snapshots** tab within an AuraDB instance shows a list of
available snapshots. ^\[1\]^

</div>

<div>

To access the **Snapshots** tab:

</div>

<div>

1.  Navigate to the Neo4j Aura Console in your browser.

2.  Select the instance you want to access.

3.  Select the **Snapshots** tab.

</div>

</div>

</div>

<div>

## Snapshot types

<div>

<div>

There are three different types of snapshot:

</div>

<div>

-   AuraDB Professional AuraDB Enterprise **Scheduled** - Runs when you
    first create an instance, when changes to the underlying system
    occur (for example, a new patch release), and automatically at a
    cadence depending on your plan type. ^\[2\]^

-   AuraDB Professional AuraDB Enterprise **Load** - Runs when you load
    a dump file from the **Import Database** tab of a instance and when
    you run the `push-to-cloud` command from the **Import** section of
    the sidebar menu of the Aura Console.

-   **On-demand** - Runs when you select **Take snapshot** from the
    **Snapshots** tab of an instance.

</div>

</div>

</div>

<div>

## Snapshot actions

<div>

<div>

### Backup and Export

<div>

You can use any of the **Scheduled** snapshots as a backup or manually
trigger an **On-demand** snapshot by selecting **Take snapshot**.

</div>

<div>

By selecting the ellipses (**...​**) button next to a snapshot, you can:

</div>

<div>

-   **Export** - Download the instance as ***.dump*** file, allowing you
    to store a local copy and work on your data offline.

-   **Create instance from snapshot** - Create a new AuraDB instance
    using the data from the snapshot.

</div>

</div>

<div>

### Restore

<div>

You can restore data in your instance to a previous snapshot by
selecting **Restore** next to the snapshot you want to restore.

</div>

<div>

Restoring a snapshot requires you to confirm the action by typing
RESTORE and selecting **Restore**.

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
<p>Restoring a snapshot overwrites the data in your instance, replacing it with the data contained in the snapshot.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

</div>

</div>

</div>

<div>

------------------------------------------------------------------------

<div>

1. Snapshots are kept in the system for 7 days for Professional plans
and 90 days for Free and Enterprise plans. Only the latest snapshot is
available for Free instances.

</div>

<div>

2. Automatic scheduled snapshots run once a day for Professional
instances and once an hour for Enterprise instances.

</div>

</div>

</div>
