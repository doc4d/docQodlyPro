---
id: dataClassPermissions
title: DataClass Permissions
---

import Column from '@site/src/components/Column'



## Configuring DataClass Permissions 

[Refer to the 4D documentation](https://developer.4d.com/docs/ORDA/privileges#inherited-permissions) to see how DataClass permissions interact with other permissions. 

To set DataClass permissions for a specific privilege:

- Select the resource name, like the `Employee` dataclass, from the dropdown list.
- Or, type the resource name directly into the search bar.

:::info
The <img src={require('./img/dataclass.png').default} style={{borderRadius: '6px', width:'3%'}} /> icon in the dropdown list indicates **DataClass** ressources.
:::

## Example: DataClass-Level Access Control

Building on the approach where the [Guest privilege is granted initial read access to the entire datastore](datastorePermissions.md#full-access-to-gradual-restriction), you can gradually restrict access to specific resources by configuring **DataClass** permissions. This involves excluding the `guest` privilege from certain DataClasses.

:::tip
While datastore permissions cascade down to DataClasses, they remain adaptable. DataClass permissions allow you to override or supplement the broader settings as needed.
:::

<img src={require('./img/overriddingDataStore.png').default} style={{borderRadius: '6px'}} />

<br/><br/>

1. Create a `Restricted` privilege for the `Employee` DataClass
2. Set all permissions to the `Restricted` privilege. 

In this context, the permissions set at the datastore level for the guest privilege are overridden by the Restricted privilege at the DataClass level. As a result, users with the guest role no longer have access to the Employee DataClass.