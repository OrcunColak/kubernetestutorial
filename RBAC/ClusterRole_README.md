`See https://overcast.blog/managing-role-based-access-control-rbac-in-kubernetes-a-guide-79d5ed5cbdf6`
# ClusterRoles

ClusterRoles are used for granting broad permissions across the entire cluster or for system-wide roles that need to
operate beyond the confines of namespaces. For example, granting a monitoring system the ability to read resources
across all namespaces.

Example ClusterRole for Reading Nodes:

```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
name: node-reader
rules:
- apiGroups: [""]
  resources: ["nodes"]
  verbs: ["get", "list", "watch"]
```

This ClusterRole allows reading information about nodes across the cluster.

# ClusterRoleBindings

ClusterRoleBindings are cluster-scoped objects that grant the permissions defined in a ClusterRole to subjects (users,
groups, service accounts) across all namespaces. They can also be used to grant cluster-wide permissions to resources
within a specific namespace.

Example ClusterRoleBinding:

```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
name: cluster-admin-binding
subjects:
- kind: User
  name: john.doe
  apiGroup: rbac.authorization.k8s.io
  roleRef:
  kind: ClusterRole
  name: cluster-admin
  apiGroup: rbac.authorization.k8s.io
```  

This ClusterRoleBinding assigns the cluster-admin ClusterRole to user john.doe, granting him administrative access
across the entire cluster.

```
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRole
metadata:
  name: node-manager
rules:
- apiGroups: [""]
  resources: ["nodes"]
  verbs: ["get", "list", "watch", "create", "delete"]
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: manage-nodes
subjects:
- kind: Group
  name: node-admins
  apiGroup: rbac.authorization.k8s.io
roleRef:
  kind: ClusterRole
  name: node-manager
  apiGroup: rbac.authorization.k8s.io
```