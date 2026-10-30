---
id: example-of-configuration
title: Example of configuration 
---
import Column from '@site/src/components/Column'

This example shows how to configure roles and privileges for a healthcare application that handles patients, appointments, and confidential data.
The application authenticates identities in its own `authentify()` function and calls [`Session.setPrivileges()`](https://developer.4d.com/docs/API/SessionClass#setprivileges) to assign roles to each session.
The rules below explain why each permission grants or denies access; see 4D's [privilege configuration rules](https://developer.4d.com/docs/ORDA/privileges#inherited-permissions) for details.


## Application overview

Here are the main characteristics of the HealthCare application.

### Model

The data model contains the following dataclasses:

<img src={require('./img/example-model.png').default} style={{borderRadius: '6px', width:'50%'}} />

:::note

The `AppSettings` dataclass is used only by the administrator to set up application settings, no external access is ever allowed.

:::

### Identities and roles

The application defines its own identities and validates them in its `authentify()` function. After authentication, this function calls `Session.setPrivileges()` to assign the appropriate role to the session. See the 4D documentation for [`authentify()`](https://developer.4d.com/docs/REST/authUsers#function-authentify) and [`Session.setPrivileges()`](https://developer.4d.com/docs/API/SessionClass#setprivileges).

<img src={require('./img/example-personae.png').default} style={{borderRadius: '6px', width:'70%'}} />

### Actions

In this example, only the **read** action is considered, to simplify the story. However, the exposed principles are the same for other actions (create, update...) ​


### Configuration target

We want to configure the following accesses:

<img src={require('./img/example-target.png').default} style={{borderRadius: '6px', width:'70%'}} />


## Configuring access

### Protecting all data

In this example, **Restrict Access By Default** is off, so resources without an explicit permission are accessible. The initial configuration is:

<img src={require('./img/example-startup.png').default} style={{borderRadius: '6px', width:'80%'}} />

The first step in activating safety is to **protect all data** by default. Accesses will then be opened for each resource.  

1. Create a **None** privilege and grant it **Read** access on the datastore.

<img src={require('./img/example-config1.png').default} style={{borderRadius: '6px', width:'100%'}} />

The datastore permission is inherited by every dataclass. Since no role receives **None**, read access to the dataclasses is denied by default.

<img src={require('./img/example-none.png').default} style={{borderRadius: '6px', width:'80%'}} />

2. Never assign **None** to a role. As an alternative, turn on **Restrict Access By Default** in `roles.json`; resources without an explicit permission are then denied, so the **None** lock privilege is unnecessary. See 4D's [restriction modes](https://developer.4d.com/docs/ORDA/privileges#restriction-modes).

### Creating the viewPatient privilege

*Doctor* and *Secretary* roles can read patient's data. 

1. Create the *viewPatient* privilege with a granted **Read** action on the `Patients` dataclass.​ 

<img src={require('./img/example-config2.png').default} style={{borderRadius: '6px', width:'100%'}} />

2. Assign it to the *Doctor* and *Secretary* roles (see [roles](#roles) below).​


<img src={require('./img/example-viewpatient.png').default} style={{borderRadius: '6px', width:'80%'}} />

The **Patients** dataclass permission replaces the datastore permission, so a session with **viewPatient** can read patient data without **None**. This also includes the `confidentialInfo` attribute unless a separate attribute permission is defined.

### Creating the viewConfidentialInfo privilege

Only the *Doctor* role can view the patient's confidential data (gathered in a *confidentialInfo* attribute). 

1. Create the *viewConfidentialInfo* privilege with **Read** access on the `Patients.confidentialInfo` attribute.

<img src={require('./img/example-config4.png').default} style={{borderRadius: '6px', width:'100%'}} />

2. Assign it to the *Doctor* role (see [roles](#roles) below). Attribute permissions are added to the parent dataclass permission, so reading `confidentialInfo` requires **both** **viewPatient** and **viewConfidentialInfo**. The *Secretary* role has only **viewPatient**, so it cannot read that attribute.

<img src={require('./img/example-viewsecretinfo.png').default} style={{borderRadius: '6px', width:'80%'}} />

### Roles

Here are the corresponding role definitions.

#### Secretary

<img src={require('./img/example-config3.png').default} style={{borderRadius: '6px', width:'100%'}} />

#### Doctor

<img src={require('./img/example-config-doctor.png').default} style={{borderRadius: '6px', width:'100%'}} />



### Allowing appointment reads

Grant the built-in **guest** privilege **Read** access to the `Appointments` dataclass.

<img src={require('./img/example-config5.png').default} style={{borderRadius: '6px', width:'100%'}} />

<img src={require('./img/example-guest.png').default} style={{borderRadius: '6px', width:'80%'}} />


The `Appointments` dataclass permission replaces the datastore-level **None** permission. Because every session has the built-in [**guest** privilege](./datastorePermissions.md#introducing-the-guest-privilege), all sessions can read appointments.

## The final picture

Here is a complete overview of the roles and privileges for our HealthCare application:

<img src={require('./img/example-full.png').default} style={{borderRadius: '6px', width:'80%'}} />

### A common pattern

A common configuration grants broad access through a **manager** privilege, then restricts one dataclass: for example, the `Salaries` dataclass requires the **payroll** privilege. A session must have **payroll** to access `Salaries`, because a dataclass permission replaces the datastore permission; **manager** continues to grant access to other dataclasses.

### Recommended practice

Grant access through roles. Create an administration role that includes every privilege except **None**, and add each new privilege to that role when it is created. With **Restrict Access By Default** off, review the **Detailed Permission Review** for every role after each permission change to confirm its effective access. See the 4D documentation on [roles, privileges, and permission rules](https://developer.4d.com/docs/ORDA/privileges#privileges-and-roles).


