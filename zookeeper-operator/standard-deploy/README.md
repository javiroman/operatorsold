````
https://kubernetes.io/docs/tutorials/stateful-application/zookeeper/
https://medium.com/@myte/kubernetes-nfs-and-dynamic-nfs-provisioning-97e2afb8b4a9 
https://github.com/kubernetes-sigs/nfs-ganesha-server-and-external-provisioner/blob/master/docs/usage.md
````

Issues:

1. PV hanged in terminating state: https://github.com/kubernetes/kubernetes/issues/77258

You can get rid of this issue by manually editing the pv and then removing the finalizers which looked something like this:

- kubernetes.io/pv-protection

e.g

kubectl patch pvc pvc_name -p '{"metadata":{"finalizers":null}}'
kubectl patch pv pv_name -p '{"metadata":{"finalizers":null}}'
kubectl patch pod pod_name -p '{"metadata":{"finalizers":null}}'

2. PV always in released, but not available because of StatefulSet claim

kubectl patch pv pv001 -p '{"spec":{"claimRef": null}}'




