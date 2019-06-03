---
Sort: 3
Title: Workshop Summary
PrevPage: exercises/04-user-environment
ExitSign: Finish Workshop
---

For details on other ways the workshop spawner can be configured, see:

* https://github.com/openshift-labs/workshop-spawner

If you want to learn how you can create your own workshop content, see:

* https://github.com/openshift-labs/lab-workshop-content

To delete the workshop itself, from where you originally deployed the workshop, run:

```copy
oc delete all,serviceaccount,rolebinding,configmap -l app=lab-learning-portal
```
