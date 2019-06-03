---
Title: Leaning Portal
PrevPage: 01-workshop-spawner
NextPage: ../finish
---

The different configurations supported by the workshop spawner provide different capabilities and behaviour. The sections below go into more details about different aspects of how the `leaning-portal` configuration works so it can be compared to other configurations. By comparing these to other configurations you can determine if this configuration is the best one for the type of workshop you want to run.

#### User Access

Anyone can access the workshop environment at any time. A unique workshop environment will be created for each user, using a temporary service account for the user, and a separate project namespace to work in.

#### Shell Terminal

A shell terminal is provided in the web browser. Command line tools for accessing the cluster, such as `oc`, `odo` and `kubectl` are provided, and configuration is setup in advance so those tools will talk to the cluster the workshop environment is running in.

The user will be automatically logged in on the command line for these tools. The only project namespace which they will be able to interact with will be that for their specific workshop environment.

#### Web Console

An embedded web console is provided. As for command line access, this will be automatically logged in, and they will only be able to access their own project namespace.

#### Cluster Access

The user will only be able to perform actions based on the default rule set applied to the service account for the user by the spawner. Specific workshops may provide custom configuration for the spawner to give additional roles to the service account for the user.

#### Default Project

Each user is given access to a single project namespace. This is created automatically when the workshop environment is setup for their session.

Specific workshops may provide custom configuration for the spawner to have the spawner create additional resources in the users project namespace. This can include deploying applications.

When the user session expires, the project namespace is automatically deleted.

#### Cluster Admin

The user does not have any cluster admin access rights.

Specific workshops may provide custom configuration for the spawner to give additional roles to the service account for the user. It is not recommended though to use this to give uses any roles that would normally be performed by a cluster admin. This is because it is a shared OpenShift cluster and users could interfere with each other, or the cluster control plane.

#### Resource Quotas

Resources quotas and limit ranges that apply to the user and their project namespace is by default dictated by any global configuration, or limit ranges applied by a project template when a project was created.

The spawner can be configured for a specific workshop to set different size resource budgets, overriding the global configuration, or remove all quotas and limits.

#### User Storage

The local file system accessible from the terminal is ephemeral. It is not possible to add persistent storage for container the terminal is running in.

#### Session Timeout

By default the session timeout is set to one hour, after which the workshop environment for a user will be automatically deleted. The workshop environment will also be deleted if the user closes the browser window or their computer goes to sleep. The maximum time allowed can be overridden for workshops that need more (or less) time.

#### Spawner Admin

There is no ability to access the admin page for the spawner. It would be necessary to configure a API key for accessing the REST API of the spawner and write a custom client to access details of sessions, and control them, via the REST API.
