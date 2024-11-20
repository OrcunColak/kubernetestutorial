See https://overcast.blog/managing-role-based-access-control-rbac-in-kubernetes-a-guide-79d5ed5cbdf6

# Roles

Roles are ideal for granting permissions within a specific namespace. For instance, you might create a Role to allow a
team of developers to manage Pods and Deployments in a development namespace without granting them access to other
namespaces.

Example Role for Pod Management:

```
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
namespace: development
name: pod-manager
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "list", "watch", "create", "update", "delete"]
```

This Role grants permissions to manage Pods within the development namespace.

# RoleBindings

RoleBindings grant the permissions defined in a Role to users, groups, or service accounts within a specific namespace.
They are namespace-scoped and link the Role to the subjects (users, groups, service accounts) within that namespace.
Example RoleBinding:

```
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
name: pod-reader-binding
namespace: development
subjects:
- kind: User
  name: jane.doe
  apiGroup: rbac.authorization.k8s.io
  roleRef:
  kind: Role
  name: pod-manager
  apiGroup: rbac.authorization.k8s.io
```  

This RoleBinding assigns the pod-manager Role to user jane.doe in the development namespace, allowing her to manage Pods
in that namespace.

```
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
  namespace: default
  name: pod-reader
rules:
- apiGroups: [""]
  resources: ["pods"]
  verbs: ["get", "list", "watch"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
  name: read-pods
  namespace: default
subjects:
- kind: User
  name: jane
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: Role
  name: pod-reader
  apiGroup: rbac.authorization.k8s.io
```