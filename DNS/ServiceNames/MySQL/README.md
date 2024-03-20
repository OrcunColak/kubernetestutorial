See  
https://medium.com/@manojkumar_41904/understanding-kubernetes-service-dns-a-deep-dive-7bf68b2baa63  
and  
https://medium.com/@muthanagavamsi/how-to-remember-kubernetes-dns-name-for-a-service-2ede2497951c

When a Service is created within a Kubernetes cluster, a DNS record is automatically assigned to it.
This DNS record is accessible within the cluster, allowing other components to resolve the Service’s IP address using
its DNS name.

The DNS name would typically be in the format **<service-name>.<namespace>.svc.cluster.local**
For our example, **mysql-service.default.svc.cluster.local**

1. Open bash. Use the correct deployment name

```
kubectl exec -it mysql-deployment-56f67c9d44-gndxk -- /bin/bash
```

2. Connect as mysql-service or mysql-service.default.svc.cluster.local

``` 
mysql -h **mysql-service** -u root -ppassword
```

or

```
mysql -h **mysql-service.default.svc.cluster.local** -u root -ppassword
```