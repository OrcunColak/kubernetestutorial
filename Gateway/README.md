# Install Gateway

The Gateway API is still in beta, so we first need to install the Gateway API CRDs for Gateway resources.

kubectl apply -k "github.com/kubernetes-sigs/gateway-api/config/crd?ref=v0.8.0"