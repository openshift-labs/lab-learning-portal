---
Title: Workshop Images
PrevPage: 04-user-environment
NextPage: ../finish
---

When you deployed the workshop spawner you did not specify a workshop image. As a result it used the default workshop image, which is the workshop base image that actual workshop images would be built from. When the workshop base image is used, it will show some sample content for testing.

To have the workshop spawner use your workshop image, you have a few choices.

The first method is to supply the `TERMINAL_IMAGE` template parameter when deploying the workshop spawner. The value used for `TERMINAL_IMAGE` can be a reference to an image hosted on an external image registry, or it can be the name of an image stream in the same project.

For example, instead of the original command we used to deploy the workshop spawner, we could instead have used:

```
oc new-app https://raw.githubusercontent.com/openshift-labs/workshop-spawner/master/templates/learning-portal-production.json \
  --param PROJECT_NAME=`oc project --short` \
  --param APPLICATION_NAME=portal \
  --param TERMINAL_IMAGE=quay.io/openshiftlabs/lab-workshop-content:1.0
```

In the case of using a reference to an image hosted on an external image registry it must include an image tag. In the case of it being an image stream, the image tag is optional, in which case it will use `latest`.

Note that when using a reference to an image hosted on an external image registry, it is recommended you use an image tag which represents a specific version, rather than a generic tag such as `latest`, `master` or `develop`. This is because when images are updated, the image registry may not keep copies of older images which a generic tag mapped to when there was no explicit version tag as well. This can result in a failure to be able to pull down the image where OpenShift cached the image hash for the image which was subsequently deleted from the image registry.

When the image is supplied via the `TERMINAL_IMAGE` template parameter, what it is set to can be seen by querying the environment variable of the same name on the deployment config for the spawner.

```execute
oc set env dc/portal --list | grep TERMINAL_IMAGE
```

For the current deployment of the workshop spawner, it would be empty as the template parameter wasn't supplied.

If you did use the `TERMINAL_IMAGE` template parameter for specifying the workshop image, you can change what is by using `oc set env`. For example:

```
oc set env dc/portal TERMINAL_IMAGE=quay.io/openshiftlabs/lab-workshop-content:1.0
```

Because you are changing the deployment configuration, this would trigger a re-deployment of the workshop spawner, which will have the side effect of killing off all active user sessions. As active user sessions will be interrupted, it isn't recommended you do this in a middle of a workshop.

If you expect that you may need to update the workshop image and do not want to interrupt any active user sessions, but have the new workshop image used for subsequent sessions, you should use a reference to an image stream and update the image tag in the image stream to refer to the new workshop image.

For this scenario, there is even a default image stream which is created and can be used for the case where the `TERMINAL_IMAGE` parameter is empty. The name of this image stream will be the name of the deployment with `-app` suffix.

To change the workshop image used by the current workshop spawner deployment, run:

```execute
oc tag quay.io/openshiftlabs/lab-workshop-content:1.0 portal-app:latest
```

Return to the browser window for the workshop environment created by the workshop spawner. Click on the menu top right of the dashboard, select "Restart Session" and confirm that a restart should be done when the popup is displayed.

When this is done the current session for the user will be shutdown and a new session will be created using the new workshop image. You should see that the identifier used for the user name has changed. This is because a new workshop environment and project namespace will be provisioned. The prior workshop environment and project namespace will be deleted in the background.

This ability to update the image stream with a new image can be used in conjunction with an image build, with the newly built image replacing the existing one for the next session which is started. This is useful when developing workshop content, as the project  namespace will be thrown away each time, meaning you don't need to manually delete anything created by the workshop.

To setup such a workflow, in the directory where you have the workshop content you are working on, first create a binary build with name matching the `-app` image stream for the deployment.

```
oc new-build --binary --name portal-app
```

Each time you want to update the workshop image, you can then run:

```
oc start-build portal-app --from-dir . --follow
```

Once the build is complete, restart the workshop session.
