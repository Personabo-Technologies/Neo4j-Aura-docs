<div>

<div>

# User management

</div>

<div>

<div>

<div>

AuraDB Enterprise AuraDS Enterprise

</div>

<div>

User management is a feature within Aura that allows you to invite users
and set their roles within an isolated environment.

</div>

</div>

</div>

<div>

## Tenants

<div>

<div>

Tenants are the primary mechanism for granting users access to an Aura
environment.

</div>

<div>

The tenant you're currently viewing is displayed in the header of the
Console. You can select the tenant name to open the **Tenant Dropdown**
menu, which allows you to view the *Tenant ID*.

</div>

<div>

It is possible to be a member of multiple tenants, in which case the
**Tenant Dropdown** will also display the other tenants you have access
to. You can switch between these tenants by clicking on the individual
tenant from the **Tenant Dropdown**.

</div>

</div>

</div>

<div>

## Team members

<div>

<div>

Each tenant consists of a single team that allows multiple users with
individual accounts to access the same environment.

</div>

<div>

The team and its members can be viewed and managed from the **Team
Members** page. You can access the **Team Members** page by selecting
**Team Members** from the sidebar menu of the Console.

</div>

<div>

### Roles

<div>

Users within a team can have one of two roles, *Admin* or *Member*.

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
<p>Each team must have at least one <em>Admin</em>, but it is also possible for teams to have multiple <em>Admins</em>.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

<div>

*Admins* can:

</div>

<div>

-   View the team members and their roles.

-   Invite new members to the team.

-   Edit an existing team member's role.

-   Delete existing team members from the team.

</div>

<div>

*Members* can:

</div>

<div>

-   View the team members and their roles.

</div>

</div>

<div>

### Inviting team members

<div>

As an *Admin*, to invite a new team member:

</div>

<div>

1.  Select **Invite member** from the **Team Members** page.

2.  Enter the **Email** address of the person you want to invite.

3.  Select the team member's **Role**.

4.  Select **Invite**.

</div>

<div>

The new team member will appear within the list of team members on the
**Team Members** page with the *Pending invite* **Status** until they
accept the invite.

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
<p>Tenant invites only appear within the Console and do not generate an email to the user you are inviting.</p>
</div>
<div>
<p>Therefore, the user you invite must have an existing <a>Neo4j Aura account</a> before they can <a>accept the invite</a>.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

</div>

<div>

### Editing team members

<div>

As an *Admin*, to edit an existing team member's role:

</div>

<div>

1.  Select the **Edit member** pencil icon next to the team member's
    name from the **Team Members** page.

2.  Select the team member's new **Role**.

3.  Select **Save changes**.

</div>

</div>

<div>

### Deleting team members

<div>

As an *Admin*, to delete an existing team member from the team:

</div>

<div>

1.  Select the **Delete member** trash can icon next to the team
    member's name from the **Team Members** page.

2.  Select **Delete**.

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
<p>It is also possible to delete a team member whose <strong>Status</strong> is <em>Pending invite</em>.</p>
</div>
<div>
<p>Select the <strong>Delete member</strong> trash can icon next to the team member’s name, and then select <strong>Revoke</strong>.</p>
</div>
</td>
</tr>
</tbody></table>

</div>

</div>

</div>

<div>

### Accepting an invite

<div>

When invited to a team, a **Tenant invitation** modal will appear the
next time you reload the Console. You can select the tenant(s) you have
been invited to and choose to accept or decline the invite(s).

</div>

<div>

You can also close the **Tenant invitation** modal without accepting or
declining the invite(s) and later manually re-open the modal by
selecting the **Pending invites** envelope icon in the Console header.

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
<p>User management within the Aura Console does not replace built-in roles or fine-grained RBAC at the database level, nor does it limit the ability to perform Console operations such as instance creation.</p>
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
