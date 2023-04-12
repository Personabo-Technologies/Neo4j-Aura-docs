<div>

<div>

# Backup, export and restore

</div>

<div>

<div>

<div>

The data in your AuraDS instance can be backed up, exported, and
restored using snapshots. A *snapshot* is a copy of the data in an
instance at a specific point in time.

</div>

<div>

The **Snapshots** tab within an AuraDS instance shows a list of
available snapshots ^\[1\]^. To access the **Snapshots** tab:

</div>

<div>

1.  Navigate to the Neo4j Aura Console in your browser.

2.  Select the instance you want to access.

3.  Select the **Snapshots** tab.

</div>

</div>

</div>

<div>

## Snapshot actions

<div>

<div>

### Take a snapshot

<div>

You can manually trigger a snapshot by selecting **Take snapshot** in
the **Snapshots** tab. The snapshot status is shown as `In progress`
until the snapshot has been created; then, the `Status` becomes
`Completed`.

</div>

</div>

<div>

### Backup and Export

<div>

By selecting the ellipses (...​) button next to a snapshot, you can:

</div>

<div>

-   **Export** - Download the database as a ***.tar.gz*** file, allowing
    you to store a local copy and work on your data offline. The
    compressed archive contains a ***.dump*** file that can be imported
    directly or pushed to the cloud.

-   **Create instance from snapshot** - Create a new AuraDS instance
    using the data from the snapshot. This opens a window where you can
    assign a name to the instance that will be created.

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
<p><strong>Caution:</strong>
Restoring a snapshot overwrites the data in your instance, replacing it with the data contained in the snapshot.</p>
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

1. Snapshots are kept in the system for 180 days.

</div>

</div>

</div>
