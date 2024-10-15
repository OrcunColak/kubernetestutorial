# Install Metrics Server

If metric server is not installed then run

```
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml
```

Check the metrics server with

```
 kubectl get deployment metrics-server -n kube-system
 ```

# Disable TLS

If metrics server does not start, check logs

```
 kubectl logs -n kube-system metrics-server-75bf97fcc9-4tlz4
```

Disable TLS
```
kubectl edit deployment metrics-server -n kube-system
then add. save and exit

spec:
  containers:
    - name: metrics-server
      args:
        - --kubelet-insecure-tls
        - ...

```