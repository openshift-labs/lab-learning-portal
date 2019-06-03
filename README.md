LAB - Learning Portal
=====================

This repository provides a workshop in which you can learn how to deploy a leaning portal in OpenShift, for training anonymous users, where the training can be done at any time.

To deploy this workshop, it is recommended you first create a fresh project into which to deploy it.

```
oc new-project labs
```

In the active project you want to use, run:

```
oc new-app https://raw.githubusercontent.com/openshift-labs/workshop-dashboard/master/templates/production.json \
  --param TERMINAL_IMAGE="quay.io/openshiftlabs/lab-learning-portal:master" \
  --param APPLICATION_NAME=lab-learning-portal
```

To get the hostname for the sample workshop, run:

```
oc get route lab-learning-portal
```

Use your browser to access the workshop.

You may need to supply your login/password again for the OpenShift cluster you deployed the sample workshop to. You will only be able to access it if you are a project admin of the project it is deployed to.

When you are finished you can delete the project you created, or if you used an existing project, run:

```
oc delete all,serviceaccount,rolebinding,configmap -l app=lab-learning-portal
```

Note that this will not delete anything which may have been deployed when you went through the workshop. Ensure that you go right through the workshop and execute any steps described in it for deleting any deployments it had you make.
