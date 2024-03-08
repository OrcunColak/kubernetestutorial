From
https://medium.com/@martin.hodges/how-to-add-tls-to-your-cloudnativepg-postgres-installation-in-your-kubernetes-cluster-cfe9cb2723c8

This will open the configMap for coreDNS in an editor

```
kubectl edit configmap coredns -n kube-system
```

You can choose a different editor by setting the KUBE_EDITOR environment variable. I use nano and so this is how I can
set up kubectl to use that editor:

```
export KUBE_EDITOR=nano
kubectl edit configmap coredns -n kube-system
```