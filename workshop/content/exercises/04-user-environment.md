---
Title: User Environment
PrevPage: 03-spawner-development
NextPage: ../finish
---

When a user accesses the URL for the spawner, with the `learning-portal` configuration they will not be prompted for any login credentials. Instead, anonymous access is allowed and a user name will be generated for them.

For each user, a pod will be started up in the same project that the spawner was originally deployed to. This pod will run the workshop image, which comprises the dashboard, with workshop content, terminal and web console.

To see the pods corresponding to any user sessions run:

```execeute
oc get pods -l app=portal-%project_namespace%,spawner=learning-portal -o name
```

The `app` label is made up of the deployment name for the spawner and the project it is deployed to. The `spawner` label is optional, but adds a qualification that it is a pod created by a spawner using the `learning-portal` configuration.

You should see output similar to:

```execute
pod/portal-labs-3kbh2
```

The part of the name after the final `-` is the user name assigned to the user for that session. If you were to visit the same URL from a different web browser or different machine, you should see an additional pod created corresponding to that session, with a different user name.

In addition this pod created in the same project as the spawner was deployed, a separate project for use with the users session is also created. Run:

```execute
oc get projects -l app=portal-%project_namespace%,spawner=learning-portal -o name
```

This will show you all the projects for user sessions created by the spawner.
