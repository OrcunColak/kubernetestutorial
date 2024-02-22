The original idea is from  
https://medium.com/@seifeddinerajhi/kube-proxy-and-cni-the-hidden-components-of-kubernetes-networking-eb30000bf87a

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
