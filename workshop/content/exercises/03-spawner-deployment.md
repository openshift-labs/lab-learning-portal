---
Title: Spawner Deployment
PrevPage: 02-learning-portal
NextPage: 04-user-environment
---

Deployment of the workshop spawner is performed using an OpenShift template. To deploy the workshop spawner using the `learning-portal` configuration, with the base image for the workshop dashboard as an example, run:

```execute
oc new-app https://raw.githubusercontent.com/openshift-labs/workshop-spawner/master/templates/learning-portal-production.json \
  --param TERMINAL_IMAGE=quay.io/openshiftlabs/workshop-dashboard:2.11.0 \
  --param PROJECT_NAME=%project_namespace% \
  --param APPLICATION_NAME=portal \
  --param SERVER_LIMIT=8 \
  --param IDLE_TIMEOUT=300 \
  --param MAX_SESSION_AGE=3600 \
  --param RESOURCE_BUDGET=medium
```

This is just an example. You would need to use the image for the workshop you would want to run, and customize the options as necessary for the workshop. We will though use this example to explore the settings you can use.

Before we can try the workshop environment you have just deployed, check that the deployment has completed by running:

```execute
oc rollout status dc/portal
```

The name "portal" corresponds to what you would supply to `APPLICATION_NAME` in the template parameters.

When the deployment is done, run:

```execute
oc get routes/portal
```

This will give you the hostname to access the workshop spawner. The resulting URL should be:

[https://portal-%project_namespace%.%cluster_subdomain%/](https://portal-%project_namespace%.%cluster_subdomain%/)

Click on this link to bring up the workshop environment. It will be opened in a separate browser window or tab. Wait while it starts up. You may see a progress page while it starts, then a splash screen, and finally the workshop dashboard. Come back here when it is done.
