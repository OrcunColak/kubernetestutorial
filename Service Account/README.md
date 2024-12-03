See https://adil.medium.com/kubernetes-core-concepts-service-account-c3db1154d86a

# Read me
To call a Kubernetes API we need a token. Default token is not sufficient. We need to create 
1. A Role + and a RoleBinding
or 
2. ClusterRole + ClusterRoleBinding

# Create pod

```
kubectl apply -f 01-pod.yaml
```

Go to pod

```
kubectl exec -it web-pod -- /bin/bash
```

From the pod run

```
curl -k https://kubernetes.default.svc/api/v1/namespaces/default/pods
```

Result is Forbidden because to access the API, we must have a token. Kubernetes API assumed the request came from an
Anonymous System User because we didn’t send a token.

But this works from kubectl

```
kubectl get --raw /api/v1/namespaces/default/pods
kubectl get --raw /api/v1/namespaces/default/pods/web-pod
```

# Default Service Account

Run

```
kubectl describe pod web-pod
```

The output is

```
...
Service Account:  default
...
```

A token for the default service account is automatically created. The token is added to the pod automatically as a file:

# Token

A token for the default service account is automatically created. The token is added to the pod automatically as a file:

```
token=`more -l /var/run/secrets/kubernetes.io/serviceaccount/token`
curl -k --header "Authorization: Bearer ${token}" https://kubernetes.default.svc/api/v1/namespaces/default/pods
```

This time we still get **Forbidden** however, now, Kubernetes API can recognize our user: **default**
The **default** service account does not have the right permissions to list the pods in the default namespace.

# Apply Role

```
kubectl apply -f 02-role.yaml
```

Role is valid for a particular namespace (in our case, default )

```
kubectl apply -f 03-role-binding.yaml
```
We can call the Kubernetes API with the token.