<div>

<div>

# Instance actions

</div>

<div>

<div>

<div>

You can perform several actions on an AuraDS instance from the Neo4j
Aura Console homepage.

</div>

</div>

</div>

<div>

## Renaming an instance

<div>

<div>

You can change the name of an existing instance by using the **Rename**
action.

</div>

<div>

To rename an instance:

</div>

<div>

1.  Select the ellipsis (**...​**) button on the instance you want to
    rename.

2.  Select **Rename** from the resulting menu.

3.  Enter a new name for the instance.

4.  Select **Rename**.

</div>

</div>

</div>

<div>

## Resizing an instance

<div>

<div>

You can change the size of an existing instance by using the **Resize**
action.

</div>

<div>

To resize an instance:

</div>

<div>

1.  Select the ellipsis (...​) on the instance you want to resize.

2.  Select **Resize** from the resulting menu.

3.  Select the new size you want your instance to be.

4.  Tick the **I understand** checkbox and select **Submit**.

</div>

<div>

An instance becomes unavailable for a short period of time during the
resize operation.

</div>

</div>

</div>

<div>

## Pausing an instance

<div>

<div>

You can pause an instance during periods where you don't need it and
resume at any time.

</div>

<div>

To pause an instance:

</div>

<div>

1.  Select the pause icon on the instance you want to pause.

2.  Select **Pause** to confirm.

</div>

<div>

After confirming, the instance will begin pausing, and a **Resume**
button will replace the **Pause** button.

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
<p>Paused instances run at a discounted rate compared to standard consumption, as outlined in the confirmation window.
You can pause an instance for up to 30 days, after which point AuraDS automatically resumes the instance.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

</div>

</div>

<div>

## Resuming an instance

<div>

<div>

To resume an instance:

</div>

<div>

1.  Select the play icon on the instance you want to pause.

2.  Tick the **I understand** checkbox and select **Resume** to confirm.

</div>

<div>

After confirming, the instance will begin resuming, which may take a few
minutes.

</div>

</div>

</div>

<div>

## Cloning an instance

<div>

<div>

There are four options to clone an instance:

</div>

<div>

-   Clone to a new AuraDS instance

-   Clone to an existing AuraDS instance

-   Clone to a new AuraDB database

-   Clone to an existing AuraDB database

</div>

<div>

You can access all the cloning options from the ellipsis (**...​**)
button on the AuraDS instance.

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
<p>You cannot clone from a Neo4j version 5 instance to a Neo4j version 4 instance.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

### Clone to a new AuraDS instance

<div>

1.  Select the ellipsis (**...​**) button on the instance you want to
    clone.

2.  Select **Clone To New** and then **AuraDS** from the contextual
    menu.

3.  Set the desired name for the new instance.

4.  Tick the **I understand** checkbox and select **Clone Instance**.

    <div>

    <div>

    <table>
<tbody><tr>
<td>
<i></i>
</td>
<td>
<strong>Warning</strong>: Make sure that the username and password are stored safely before continuing. Credentials cannot be recovered afterwards.
</td>
</tr>
</tbody></table>

    </div>

    </div>

</div>

</div>

<div>

### Clone to an existing AuraDS instance

<div>

<div>

<table>
<tbody><tr>
<td>
<i></i>
</td>
<td>
<strong>Warning:</strong> Cloning into an existing instance will replace all existing data. If you want to keep the current data, take a snapshot and export it.
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

1.  Select the ellipsis (**...​**) button on the instance you want to
    clone.

2.  Select **Clone To Existing** and then **AuraDS** from the contextual
    menu.

3.  If necessary, change the instance name.

4.  Select the existing AuraDS instance to clone to from the dropdown
    menu.

    <div>

    <div>

    <table>
<tbody><tr>
<td>
<i></i>
</td>
<td>
Existing instances that are not large enough to clone into will not be available for selection. In the dropdown menu, they will be grayed out and have the string <code>(Instance is not large enough to clone into)</code> appended to their name.
</td>
</tr>
</tbody></table>

    </div>

    </div>

5.  Tick the **I understand** checkbox and select **Clone**.

</div>

</div>

<div>

### Clone to a new AuraDB database

<div>

<div>

<table>
<tbody><tr>
<td>
<i></i>
</td>
<td>
An AuraDS instance can only be cloned to an AuraDB Professional database (not Free).
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

1.  Select the ellipsis (**...​**) button on the instance you want to
    clone.

2.  Select **Clone To New** and then **AuraDB** from the contextual
    menu.

3.  Set your desired settings for the new database. For more information
    on AuraDB database creation, see Creating an instance.

4.  Tick the **I understand** checkbox and select **Clone Database**.

    <div>

    <div>

    <table>
<tbody><tr>
<td>
<i></i>
</td>
<td>
<strong>Warning</strong>: Make sure that the username and password are stored safely before continuing. Credentials cannot be recovered afterwards.
</td>
</tr>
</tbody></table>

    </div>

    </div>

</div>

</div>

<div>

### Clone to an existing AuraDB database

<div>

<div>

<table>
<tbody><tr>
<td>
<i></i>
</td>
<td>
An AuraDS instance can only be cloned to an AuraDB Professional database (not Free).
</td>
</tr>
</tbody></table>

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
<strong>Warning:</strong> Cloning into an existing database will replace all existing data. If you want to keep the current data, take a snapshot and export it.
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

1.  Select the ellipsis (**...​**) button on the instance you want to
    clone.

2.  Select **Clone To Existing** and then **AuraDB** from the contextual
    menu.

3.  If necessary, change the database name.

4.  Select the existing AuraDB database to clone to from the dropdown
    menu.

    <div>

    <div>

    <table>
<tbody><tr>
<td>
<i></i>
</td>
<td>
Existing instances that are not large enough to clone into will not be available for selection. In the dropdown menu, they will be grayed out and have the string <code>(Instance is not large enough to clone into)</code> appended to their name.
</td>
</tr>
</tbody></table>

    </div>

    </div>

5.  Tick the **I understand** checkbox and select **Clone**.

</div>

</div>

</div>

</div>

<div>

## Deleting an instance

<div>

<div>

You can delete an instance if you no longer want to be billed for it.

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
<p><strong>Warning:</strong> There is no way to recover data from a deleted AuraDS instance.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

To delete an instance:

</div>

<div>

-   Select the red trashcan icon on the instance you want to delete.

-   Type the exact name of the instance (as instructed) to confirm your
    decision, and select **Destroy**.

</div>

</div>

</div>

</div>
