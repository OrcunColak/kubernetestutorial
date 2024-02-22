The original idea is from  
https://medium.com/@seifeddinerajhi/kube-proxy-and-cni-the-hidden-components-of-kubernetes-networking-eb30000bf87a

Kube Proxy performs Service to Pod mapping.
It monitors changes to Service objects and their corresponding endpoints.   
It then translates these changes into tangible network rules within the node.  
Typically, Kube-Proxy operates within your cluster as a DaemonSet.

# Relationship with API server.

Once Kube-Proxy is installed, it establishes authentication with the API server.
As new Services or endpoints are introduced or removed, the API server promptly communicates these changes to
Kube-Proxy.

# Learn Kube-Proxy Mode

1. IP tables Mode
2. IPVS Mode
3. KernelSpace Mode :  Exclusive to Windows nodes
4. Userspace Mode
   From CLI type

```
kubectl get configmap kube-proxy -n kube-system -o yaml
```

Output is something like this

```
apiVersion: v1
data:
  config.conf: |
    bindAddress: 0.0.0.0
    clientConnection:
      acceptContentTypes: ""
      burst: 10
      contentType: application/vnd.kubernetes.protobuf
      kubeconfig: "/var/lib/kube-proxy/kubeconfig.conf"
      qps: 5
    clusterCIDR: "10.244.0.0/16"
    configSyncPeriod: 15m0s
    ...
    # other configuration parameters
    ...
    mode: ""  # <-- Empty or not explicitly set (default mode is iptables)
kind: ConfigMap
metadata:
  creationTimestamp: "2022-02-22T08:00:00Z"
  name: kube-proxy
  namespace: kube-system
  resourceVersion: "12345678"
  uid: abcdefgh-ijkl-mnop-qrst-uvwxyz012345
```
