---
Title: Workshop Spawner
PrevPage: ../setup
NextPage: 02-learning-portal
---

Workshops are provided as a container image. The image includes the workshop content, slides and any additional files required to do the workshop. The image also bundles commonly used UNIX utilities and programming language runtimes, as well as the applications which provide the workshop dashboard environment and terminal.

For individual use, the container image for a workshop can be deployed standalone, without requiring any additional applications to deploy it. This standalone mode is likely how you are consuming this workshop.

In order to be able to deploy a workshop to many users at the same time, a separate workshop spawner application is available. The workshop spawner is deployed, along with the details of the container image for the workshop. When a user accesses the URL for the workshop spawner, logging in via a login page first if necessary, they will be provided with their own unique instance of the workshop environment running in a container. The user can then go through the workshop, knowing they are isolated from any other users who are doing the workshop at the same time.

The workshop spawner application can be found at:

* https://github.com/openshift-labs/workshop-spawner

It supports a number of different configurations or modes in which it can be deployed. These are:

* `hosted-workshop` - Used to run a supervised workshop where each user is provided with separate login credentials for an existing user of the OpenShift cluster in which the workshop is being run, in order to login. Users can perform any action in the cluster that the OpenShift user can do, including being able to create multiple projects, if the cluster user quota configuration permits it.
* `learning-portal` - Used for a more permanent interactive learning environment where users are anonymous and may do a workshop at any time. Users are given temporary access as a service account user, with a single temporary project. When a workshop is completed, or allowed time expires, the service account and project are automatically deleted.
* `user-workspace` - Similar to the learning portal, but users need to login through Keycloak. Users are given access as a service account user, with a single project. The service account and project are dedicated to the user and will still be present if the user were to leave and come back at a future time. This provides a place where users can do ongoing work, but without needing to allocate users in OpenShift itself.
* `jumpbox-server` - Users login through Keycloak. Their instance, possibly only a terminal rather than full workshop environment, runs in the OpenShift cluster, but they have no access to the cluster itself to do anything. The terminal would be used to access a separate system.

In this workshop, you will learn about the `hosted-workshop` configuration.
