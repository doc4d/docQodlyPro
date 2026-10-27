---
id: includingPrivileges
title: Including Privileges
---

import Column from '@site/src/components/Column'   

## Overview

Privilege inclusion lets you combine existing privileges to build a reusable access-control structure.
An included privilege contributes its permissions to the privilege that includes it, helping avoid duplicate configurations.
This makes it easier to manage access consistently as application needs evolve.
Privileges can be assigned to roles to define what each group of users can do.


For example, `ManageFinancials` can include `ManageReports` to bring reporting permissions together with financial-specific access.
The resulting privilege can then be assigned to the `Financial Manager` role.

This approach keeps shared permissions in one place while allowing specialized privileges to add their own access rules. Use privilege inclusion to simplify administration while keeping access scoped to the needs of each role.
For details, see the 4D documentation on [privileges and roles](https://developer.4d.com/docs/ORDA/privileges#privileges-and-roles).

## Including Privilege Configuration

To include the `ManageReports` privilege within the scope of `ManageFinancials`:

1. Start by selecting the `ManageFinancials` privilege
2. In the interface, you'll encounter a list of tags representing previously created privileges. 
3. Include the `ManageReports` privilege into `ManageFinancials` by clicking the <img src={require('./img/includePrivilege.png').default} style={{borderRadius: '6px', width:'3%'}} /> button, with removal just a click away using the  <img src={require('./img/excludePrivilege.png').default} style={{borderRadius: '6px', width:'3%'}} /> button.

<img src={require('./img/IncludePrivilege3.png').default} style={{borderRadius: '6px'}} />

<br/><br/>

:::info


When a privilege is included within another:

<Column.List align="center" justifyContent="between">
    <Column.Item width="65%">
        <ul>
            <li>Its name appears below the initial privilege that included it.</li>
        </ul>
    </Column.Item>
    <Column.Item width="30%">
		<img src={require('./img/listedPrivilege.png').default} style={{borderRadius: '6px'}} />
    </Column.Item>
</Column.List>

<Column.List align="center" justifyContent="between">
    <Column.Item width="65%">
        <ul>
            <li>The privilege is highlighted in the tags.</li>
        </ul>
    </Column.Item>
    <Column.Item width="30%">
        <img src={require('./img/privilegeHighlighted.png').default} style={{borderRadius: '6px'}} />
    </Column.Item>
</Column.List>

<ul>
    <li>The <img src={require('./img/inherit.png').default} style={{borderRadius: '6px', width:'2%'}} /> icon indicates that permissions are inherited.</li>
</ul>

<Column.List align="center" justifyContent="between">
    <Column.Item width="65%">
        <ul>
            <li>Hovering over the <img src={require('./img/i.png').default} style={{borderRadius: '6px', width:'3%'}} /> icon reveals the privilege from which they are inherited.</li>
        </ul>
    </Column.Item>
    <Column.Item width="30%">
		<img src={require('./img/inherited_hoverModal.png').default} style={{borderRadius: '6px'}} />
    </Column.Item>
</Column.List>
:::

Upon successful inclusion, the `ManageFinancials` privilege inherits permissions from its counterpart, the `ManageReports` privilege, while retaining the delete permission exclusive to the `ManageFinancials` privilege.




