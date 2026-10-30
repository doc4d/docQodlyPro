---
id: functionPermissions
title: Function Permissions
---

import Column from '@site/src/components/Column'   


Function-level permissions control access to custom functions defined within the Model. These functions can perform actions such as managing bookings, generating invoices, and handling reservations.

## Configuring Function Permissions 

To configure **Function** Permissions for a specific privilege, follow these steps:

- Choose the resource name, like the `register` function, from the dropdown list.
- Alternatively, type the resource name, such as the `register` function, directly into the search bar.

:::info

- The <img src={require('./img/function.png').default} style={{borderRadius: '6px', width:'3%'}} /> icon in the dropdown list indicates **Function** ressources.
- The <img src={require('./img/singleton.png').default} style={{borderRadius: '6px', width:'3%'}} /> icon in the dropdown list indicates **Singleton function** ressources.
:::

:::tip

If the Singleton class or its exposed functions don't appear in the permissions dropdown, follow these steps to enable it:
1. Navigate to the [Singleton class](https://developer.4d.com/docs/Concepts/classes#singleton-classes) in the class section.

2. Check if the **Singleton class** is missing any exposed functions.

3. If there are no exposed functions, add at least one. Here’s an example:<img src={require('./img/singletonFunctionExposed.png').default} style={{borderRadius: '6px', width:'35%', verticalAlign: 'middle', marginLeft: '2px'}} />.

4. Save the changes and re-check the permissions dropdown. 

5. If the Singleton class and its exposed functions still don't appear, [reload](../qodlyStudioInterface.md#contextual-menu) the changes by following the documentation for applying the latest updates. 

Now, the Singleton class and its exposed functions should be available for selection, whether it’s the standard class Singleton or the shared one.

:::

### Execute Permission

Execute permissions allow the designated privilege to run the function's code <img src={require('./img/executeFunction.png').default} style={{borderRadius: '6px', width:'5%'}} />.

:::info

<Column.List align="center" justifyContent="between">
    <Column.Item width="65%">
        If the Execute function permission checkbox has the <img src={require('./img/functionPermission_promotedIcon.png').default} style={{borderRadius: '6px', width: '4%'}} /> icon on the right, it signifies that the <a href="#promote-permission">function has been promoted by another privilege</a>. Hover over the privilege name, and clicking on it will redirect you to the privilege promoting the function.
    </Column.Item>
    <Column.Item width="30%"> 
        <img src={require('./img/functionPermission_goToPrivilege.png').default} style={{borderRadius: '6px'}} />
    </Column.Item>
</Column.List>

:::

### Promote Permission

Promote permissions enable temporary privilege escalation during function execution <img src={require('./img/promoteFunction.png').default} style={{borderRadius: '6px', width:'5%'}} />, ensuring the secure performance of critical operations within that function's code without permanently adding privileges.

:::info
Upon executing a specific function within a session with a designated privilege, Qodly dynamically integrates the privileges that `Promote` the function into the session. This temporary elevation allows the function's execution, even when the original session's privilege lacks direct permission for resources in that function code.

After the function concludes, the temporary elevation from the `Promote` permission is revoked.
:::

<Column.List align="center" justifyContent="between">
    <Column.Item width="65%">
        A function can be promoted from multiple privileges. In such cases, there's no hierarchy determining priority.
        <br/> 
        Instead, the session experiencing temporary privilege elevation during function execution, will have access to all resource permissions set in each of the promoting privileges.
    </Column.Item>
    <Column.Item width="30%">
        <img src={require('./img/functionPermission_promotedFromMultiple.png').default} style={{borderRadius: '6px'}} />
    </Column.Item>
</Column.List>

<br/> 

:::info
<Column.List align="center" justifyContent="between">
    <Column.Item width="65%">
        The <img src={require('./img/functionPermission_promotedIcon.png').default} style={{borderRadius: '6px', width: '4%'}} /> icon indicates that the function has been promoted by another privilege. Hover over the privilege name, and clicking on it will direct you to the privilege promoting the function.
    </Column.Item>
    <Column.Item width="30%">
        <img src={require('./img/functionPermission_goToPrivilege.png').default} style={{borderRadius: '6px'}} />
    </Column.Item>
</Column.List>
:::



