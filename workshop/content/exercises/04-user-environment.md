---
Title: User Environment
PrevPage: 03-spawner-deployment
NextPage: 05-workshop-images
---

When a user accesses the URL for the spawner, with the `learning-portal` configuration they will not be prompted for any login credentials. Instead, anonymous access is allowed and a user name will be generated for them.

For each user, a pod will be started up in the same project that the spawner was originally deployed to. This pod will run the workshop image, which comprises the dashboard, with workshop content, terminal and web console.

To see the pods corresponding to any user sessions run:

```execute
oc get pods -l app=portal-%project_namespace%,class=session -o name
```

The `app` label is made up of the deployment name for the spawner and the project it is deployed to. The `class=session` label selector ensures that only resources related to user sessions are shown.

You should see output similar to:

```
pod/portal-labs-3kbh2
```

The part of the name after the final `-` is the user name assigned to the user for that session. If you were to visit the same URL from a different web browser or different machine, you should see an additional pod created corresponding to that session, with a different user name.

In addition to the pod for the workshop environment created in the same project as the spawner was deployed, a separate project for use with the users session is also created. Run:

```execute
oc get projects -l app=portal-%project_namespace%,class=session -o name
```

This will show you all the projects for user sessions created by the spawner.

You should see output similar to:

```
project.project.openshift.io/portal-labs-3kbh2
```

As users are not using an existing OpenShift user account, we need to give them an identity to work as in the OpenShift cluster. This is done by creating a service account for each user.

To list the service accounts for the users, run:

```execute
oc get serviceaccounts -l app=portal-%project_namespace%,class=session -o name
```

You should see output similar to:

```
serviceaccount/portal-labs-3kbh2
```

The pod running the workshop environment, runs as the service account for that user. The project namespace for a user is setup using appropriate role bindings, so that the user's service account has effective project admin access over their project namespace.

This is what enables the user from the command line of the terminal, or the embedded web console, to make changes to their project namespace, or deploy applications to it. As each user has their own service account for their session, they can only work with their project namespace and cannot see or do anything to other projects in the cluster.

Jump back to the browser window for the workshop environment you created by accessing the URL for the spawner you deployed from this workshop.

Verify that the terminal for that workshop environment is a unique service account for that session by running:

```copy
oc whoami
```

Also run:

```copy
oc projects
```

to verify that you have access to only the one project namespace, and that it is that created for that session.

Both the name of the service account and the name of the project should use the same user identifier for that session.
