---
tag: [ "codenvy" ]
title: Permissions
excerpt: ""
layout: docs
permalink: /:categories/permissions/
---
{% include base.html %}


Permissions are used to control user actions. Rather than provide a fixed set of roles we use a broader set of permissions that can be applied in any combination to establish the security you need.

Codenvy also provides a mechanisms and layers which allow to define "who" is allowed to do "what". Any user and administrator can control resources managed by Codenvy and allow certain actions or behaviors for other users or groups. For example as owner of a workspace, you can grant other users permission to see and/or use your workspace.

Permissions can be applied to:
- Workspace
- Organization
- Stack
- Recipe
- System

Permissions can be assigned to:
- Users
- Group of users (see teams) [TODO:link]

# Workspace Permissions

The user who creates a workspace is the _workspace owner_ and has all permissions by default. Workspace owners can invite other users into the workspace and control their permissions for the workspace.

The following permissions are applicable to workspaces:

| Permission      | Description                                             |
| --------------- | ------------------------------------------------------- |
| read            | Allows reading a workspace's configuration.
| use             | Allows using a workspace and interacting with it.
| run             | Allows starting and stopping a workspace.
| configure       | Allows defining and changing a workspace configuration.
| setPermissions  | Allows updating workspace permissions for other users.
| delete          | Allows deleting the workspace.

# Organization Permissions

An organization is a named set of users. Organizations are the underlying layer for teams [TODO:link] in Codenvy.

The following permissions are applicable to organizations:

| Permission                    | Description                                                           |
| ----------------------------- | --------------------------------------------------------------------- |
| update                        | Allows editing of organization settings and information.
| delete                        | Allows deleting an organization.
| manageSuborganizations        | Allows creating and managing sub-organizations.
| manageResources               | Allows redistribution of an organization’s resources and defining resource limits.
| manageWorkspaces              | Allows creating and managing all the organization's workspaces.
| setPermissions                | Allows adding and removing users as well as updating their permissions.

# System Permissions

System permissions control aspects that affect the whole Codenvy installation.

The following permissions are applicable to organizations:

| Permission                    | Description                                                           |
| ----------------------------- | --------------------------------------------------------------------- |
| manageSystem                  | Allows control of the system, workspaces and organizations.
| setPermissions                | Allows updating of permissions for users on the system.
| manageUsers                   | Allows creating and managing users.

## Super Priviliged Mode

The permission "manageSystem" can be extended to provide a super privileged mode that allows advanced actions to be performed on any resources managed by the system. A user with "manageSystem" permission is able read and stop any workspaces. To perform other actions on workspaces and organizations, the user will need to assign himself the permissions needed.

By default, this mode is disabled.

It is possible to activate this option by configuring the `CODENVY_SYSTEM_SUPER_PRIVILEGED_MODE` in the `codenvy.env` file.

# Stack Permissions

Stack are defined [TODO: link]

The following permissions are applicable to a stack:

| Permission                    | Description                                                           |
| ----------------------------- | --------------------------------------------------------------------- |
| search                        | Allows searching of the stacks.
| read                          | Allows reading of the stack's configuration.
| update                        | Allows updating of the stack's configuration.
| delete                        | Allows deleting of the stack.
| setPermissions                | Allows managing permissions for the stack.

# Recipe Permissions

Recipe are defined [TODO: link]

The following permissions are applicable to a recipe:

| Permission                    | Description                                                           |
| ----------------------------- | --------------------------------------------------------------------- |
| search                        | Allows searching of the recipes.
| read                          | Allows reading of the recipe's configuration.
| update                        | Allows updating of the recipe's configuration.
| delete                        | Allows deleting of the recipe.
| setPermissions                | Allows managing permissions for the recipe.


# Permissions API

All permissions can be managed by using the provided REST API. The APIs are documented using Swagger, as explained here [TODO: link].

The permissions API list can be accessed by: [{host}/swagger/#!/permissions]().

## List Permissions

List the permissions which can be applied to a specific resources:
GET /permissions : [{host}/swagger/#!/permissions/getSupportedDomains]()

Applicable `domain` values are the following:

| Domain                     |
| -------------------------- |
| system                     |
| organization               |
| workspace                  |
| stack                      |
| recipe                     |

Note: `domain` is optional, in this case the API will return all possible permissions for all domains.

## List Permissions for Specific User

List the permissions which are applied to a specific user:
GET /permissions/{domain} : [{host}/swagger/#!/permissions/getCurrentUsersPermissions]()

Applicable `domain` values are the following:

| Domain                     |
| -------------------------- |
| system                     |
| organization               |
| workspace                  |
| stack                      |
| recipe                     |

`instance` parameter corresponds to the ID of the resource you want to get the applied permissions.

## List Permissions for All Users

List the permissions which are applied to a specific user (you must have sufficient permissions to allow you to see this information):
GET /permissions/{domain}/all : [{host}/swagger/#!/permissions/getUsersPermissions]()

Applicable `domain` values are the following:

| Domain                     |
| -------------------------- |
| system                     |
| organization               |
| workspace                  |
| stack                      |
| recipe                     |

`instance` parameter corresponds to the ID of the resource you want to get the applied permissions for all users.

## Assign Permissions

Assign permissions to a resource:
POST /permissions : [{host}/swagger/#!/permissions/storePermissions]()

Applicable `domain` values are the following:

| Domain                     |
| -------------------------- |
| system                     |
| organization               |
| workspace                  |
| stack                      |
| recipe                     |

`instance` parameter corresponds to the ID of the resource you want to get the applied permissions for all users.

`userId` parameter corresponds to the ID of the user who want to grant certain permissions.

Sample `body` to grant user `userID` permissions to a workspace `workspaceID`:

```json
{
  "actions": [
    "read",
    "use",
    "run",
    "configure",
    "setPermissions"
  ],
  "userId": "userID",
  "domainId": "workspace",
  "instanceId": "workspaceID"
}
```
