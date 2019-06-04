---
Title: Spawner Deployment
PrevPage: 02-learning-portal
NextPage: 04-user-environment
---

Deployment of the workshop spawner is performed using an OpenShift template. To deploy the workshop spawner using the `learning-portal` configuration, and the default workshop image, run:

```execute
oc new-app https://raw.githubusercontent.com/openshift-labs/workshop-spawner/master/templates/learning-portal-production.json \
  --param PROJECT_NAME=`oc project --short` \
  --param APPLICATION_NAME=portal
```

This is a bare bones example. You would need to use the image for the workshop you would want to run, and customize the options as necessary for the workshop. The name of the workshop image to use and any options, can be supplied using additional template parameters.

The one required template parameter is that for `PROJECT_NAME`, being the name of the project the deployment is being made to. The name of the deployment is given by `APPLICATION_NAME` and defaults to `portal` if not set.

Before you try the workshop environment you have just deployed, check that the deployment has completed by running:

```execute
oc rollout status dc/portal
```

When the deployment is done, run:

```execute
oc get routes/portal
```

This will give you the hostname to access the workshop spawner. The resulting URL should be:

[https://portal-%project_namespace%.%cluster_subdomain%/](https://portal-%project_namespace%.%cluster_subdomain%/)

Click on this link to bring up the workshop environment. It will be opened in a separate browser window or tab. Wait while it starts up. You may see a progress page while it starts, then a splash screen, and finally the workshop dashboard. Come back here when it is done.
