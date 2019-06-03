---
Sort: 2
Title: Workshop Setup
PrevPage: index
NextPage: exercises/01-workshop-spawner
ExitSign: Start Workshop
---

This workshop requires you have cluster admin access rights to the OpenShift cluster you are using. You will need to login as the cluster admin from the terminal provided with the workshop environment.

```execute
oc login
```

Supply credentials corresponding to an account with cluster admin access rights.

To check that you are logged in correctly and will be able to create the resources which need cluster admin access rights, run:

```execute
oc auth can-i create clusterroles
```

and:

```execute
oc auth can-i create clusterrolebindings
```

Did you type the command in yourself? If you did, click on the command instead and you will find that it is executed for you. You can click on any command which has the <span class="glyphicon glyphicon-play-circle"></span> icon shown to the right of it, and it will be copied to the interactive terminal and run.

If the output from the `oc auth can-i` command is `yes`, you are all good to go.
