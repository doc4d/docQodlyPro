---
id: overview
title: Configuring Roles and Privileges
---
import Column from '@site/src/components/Column'


## Roles: Defining User Profiles 

### Understanding Roles  

Roles are essential in defining distinct user profiles within Qodly. Each role corresponds to a specific set of privileges, and access levels (Permissions).

### Detailed Permission Review for Roles

When a role is selected in the `Roles & Privileges` editor, a detailed permission review is displayed to provide insight into the final permissions resolution for that specific role. This feature helps developers fine-tune privileges more effectively by showing the impact of privilege configurations.

This review is available on **roles only, by design**: roles are the recommended way to give access, so the effective permissions are shown where they apply. The review is computed from the [role's privileges plus `guest`](https://developer.4d.com/docs/ORDA/privileges#privileges-and-roles). 

<img src={require('./img/showRolePermissions.png').default} style={{borderRadius: '6px'}} />


- Comprehensive Permission Listing: Lists all application code assets, including: Dataclasses, Attributes, Functions, Singletons and Singleton functions.

- Organized and Alphabetical Grouping: Listed assets are grouped and sorted alphabetically as follows:

	- Datastore (ds)
	- Datastore Functions 
	- Dataclasses
	- Attributes
	- Dataclass Functions
	- Entity Functions
	- Entity Selection Functions
	- Singletons
	- Singleton Functions

- Permission Columns: For each asset, the following columns display resolved permissions: Read, Create, Update, Delete and Execute. The **ds** row shows the permissions defined on the datastore, not a summary of the dataclasses below (expand the row to see them).

:::tip Permission Indicators
A grey tick <img src={require('./img/PermissionIndicators1.png').default} style={{borderRadius: '6px', width:'3%'}} /> indicates that the permission is granted. 

If the access is granted through promoted privileges, an info indicator <img src={require('./img/PermissionIndicators3.png').default} style={{borderRadius: '6px', width:'5%'}} /> is provided.

An empty checkbox <img src={require('./img/PermissionIndicators2.png').default} style={{borderRadius: '6px', width:'3%'}} /> indicates that the permission is not granted.
:::

:::tip

To see what a session without role can do (before login, i.e. guest only), create a role with no privilege and look at its review.

:::


### Adding Roles  

To add a role:

1. Open the `Explorer` Panel.
2. Navigate to the `Roles and Privileges` section.
3. Click on the `Roles` tab to access role management.
4. To create a new role, click on the `+` button next to Roles. <img src={require('./img/addRole.png').default} style={{borderRadius: '6px', width:'30%'}} />
5. Enter the name of the role in the creation dialog box and click **Create** or **Cancel**. 

To edit or delete a role:

1. Select a role in the list.
2. Click on the `pencil` icon to rename it, or on the `trash` icon to remove it.

Renaming updates every reference; deleting asks for confirmation and removes the privilege from roles, inclusions and permissions. 

:::note Example
In a back-office travel agency solution, you might create roles such as:


|Roles          |Description|
|---------------|---|
|Agent       | Reserves and customizes travel packages for clients.|  
|Content Manager| Manages website content, including creating and updating travel packages.|
|Sales Manager  | Manages customer bookings, views sales reports, and generates invoices.|
:::

## Privileges: Enabling Controlled Access

### Understanding Privileges  

Privileges define the specific permissions that users of different roles can perform. By assigning privileges to roles, you determine the extent of a user's access to data and functionalities.

### Adding Privileges  

To add a privilege:

1. Open the `Explorer` Panel.
2. Navigate to the `Roles and Privileges` section.
3. Click on the `Privileges` tab to access privileges management.
4. Click on the `+` button to create a new privilege.
5. Enter the name of the privilege in the creation dialog box and click **Create** or **Cancel**. 

<img src={require('./img/addPrivilege.png').default} style={{borderRadius: '6px', width:'50%'}} />


<br/><br/>


### Guest

The `guest` privilege is always present. It cannot be renamed, deleted or included. [See the 4D documentation](https://developer.4d.com/docs/ORDA/privileges.md#guest-privilege) for more information on the `guest` privilege.


:::note Example
In a back-office travel agency solution, you might create privileges such as:

|Privileges     |Description|
|---------------|---|
|ManageReports        | Access to sales reports and statistical data.|
|ManageBookings       | Manage customer bookings, verify reservations, and generate invoices.|
|ManageContent        | Access and manage the travel agency's online content.|
:::


### Privileges Contextual Panel 

The contextual panel of privileges provides a clear visual representation of privilege relationships, making it easier to navigate and manage permissions efficiently.

When a privilege is selected from the list of privileges, the contextual panel updates to reflect the selection:

- **Standalone Privileges**: If a [privilege does not include another privilege](./includingPrivileges) (e.g., manageTags) and is not included by another privilege, it is displayed alone in the contextual panel.
	<img src={require('./img/PrivilegesContextualPanel.png').default} style={{borderRadius: '6px', width: '50%'}} />


- **Include Privileges**: If a [privilege includes another privilege](./includingPrivileges) (e.g., manageAuthors, which includes manageArticles) or is included by another privilege, the contextual panel will display a link between privileges.
	<img src={require('./img/PrivilegesContextualPanel2.png').default} style={{borderRadius: '6px', width: '50%'}} />


In the contextual panel, the currently selected privilege is highlighted with a purple background and is the one whose permissions table is currently displayed.

:::tip
You can click on another privilege within the contextual panel to switch to that privilege, making it the newly selected one.
:::


## Interplay Between Roles and Privileges

Achieving the optimal synchronization of roles and privileges ensures seamless task execution for users while maintaining robust data security. 

To assign one or multiple privileges to a role:

1. Navigate to the `Roles` tab within the `Roles and Privileges` section.
2. Select the desired role (e.g., `Sales Manager`).
3. Locate the privileges section on the top. 

	- In this section, you'll find a comprehensive list of available privileges.
	- `guest` is shown selected (italic) on every role and cannot be removed; it is not written in the role

4. To assign a privilege, click the `+` icon.
5. To remove a privilege, simply click the `-` icon.

<img src={require('./img/InterplayBetweenRoles_and_Privileges.png').default} style={{borderRadius: '6px'}} />

<br/><br/>


:::note Example
For instance, a `Sales Manager` role might possess privileges like `ManageBookings` and `ViewReports`, granting them the ability to analyze booking trends and monitor revenue for informed decision-making. Similarly, a `Content Manager` role could receive the privilege `ManageContent`.
:::

## Assigning Roles and Privileges

Roles are assigned to **user sessions** using the [`Session.setPrivileges()`](https://developer.4d.com/docs/API/SessionClass#setprivileges) function of the `4D.Session` class. 

It is recommended to assign **roles** rather than **privileges**: you define one role per user profile, assigned to the session. Although 4D allows you to assign privileges directly, this should be the exception. A privilege is merely a building block; it is the role that describes what a user can do. 




## Roles and privileges JSON Representation

Roles and privileges are stored in dedicated file named `roles.json`. [See the 4D documentation](https://developer.4d.com/docs/ORDA/privileges#rolesjson-file) for more information about this file. 

<Column.List align="center" justifyContent="between">
	<Column.Item width="50%">
        This representation can be accessed through a text editor by selecting the <code>Roles and privileges</code> in the <code>Explorer</code> and choosing <code>Open With</code> a <code>Text Editor</code>.
	</Column.Item>
	<Column.Item width="45%">
        <img alt="json" src={require('./img/openastext.png').default} style={{borderRadius: '6px'}} />
	</Column.Item>
</Column.List>

<br/>

This allows you to view, copy, or edit the JSON representation.

:::warning
Exercise caution when editing the JSON representation. The syntax checker does not validate whether attribute names match the expected ones or if there are issues with attribute names. Always ensure you have a backup before making changes.
:::