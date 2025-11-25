---
id: sessions
title: User sessions
slug: /guides/user-sessions
---

When a user connects to a Qodly application, a *user session* is automatically opened on the Qodly server to manage their access with regards to their privileges. A [session](../SessionClass.md) cookie is generated.

When the user connects to Qodly applications through an [**authenticated access**](../../getStarted/access.md#authenticated-access), the *user session* gets automatically their defined [privileges](../../../4DQodlyPro/roles/rolesPrivilegesOverview.md) according to the **Profile** [associated to the user in the console](../../console/userAccountManagement.md#add-new-user). 

:::info

A Qodly user session never expires, however the parent **Amazon Cognito** session expires after one week of inactivity.

:::

When the user connects to the application through the **Public access** (the public URL access must be [activated explicitely](../../console/resourceMonitoring.md#application-access) in the Console), the Qodly developer must authenticate the user and grant them a privilege or role using the [Session class API](../SessionClass.md). For example, you can get the list of privileges associated to the session using the [`getPrivileges()`](../SessionClass.md#getprivileges) function, or store user information in the session's [`storage`](../SessionClass.md#storage) property.

The user only has [Guest privilege](../../../4DQodlyPro/roles/datastorePermissions.md#introducing-the-guest-privilege) by default ([`Session.isGuest`](../SessionClass.md#isguest) returns true).  

See [this tutorial](./login.md) for an example of custom user authentication for public access. 

## Retrieving Current Session Information

You can retrieve user information in the current session using the `cs.Qodly.Users` class. This allows you to access essential user details, such as their email, role, first name, and last name.

Here's how you can retrieve and store user data for session-wide access:

```qs
exposed Function loadSessionUserInfo()

    use(session.storage)
        session.storage.currentUser = cs.Qodly.Users.me.currentUser()
    end

```

For more detailed information, refer to the [Sessions](../SessionClass.md) and [Users](../UsersClass.md) classes.



