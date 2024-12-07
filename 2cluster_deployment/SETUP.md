# Creating local cluster 


A
```
kind create cluster --wait 5m 
kubectl config set-context kind-kind
kubectl cluster-info

k get daemonSets --namespace=kube-system kube-proxy

k get deployments --namespace=kube-system

k get services --namespace=kube-system
```


# Install a GUI to view your cluster through 

```
kubectl apply -f https://raw.githubusercontent.com/kubernetes/dashboard/v2.0.0-beta8/aio/deploy/recommended.yaml
```
or 
```
kubectl apply -f 2cluster_deployment/dashboard.yaml
```

then use:
```
kubectl proxy
```
to port forward requests to 8001; head to 

`http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/`

to access the platform, create a *service account* and a *token* for said *service account* 

```
kubectl create serviceaccount akin
```
and the token: 
```
kubectl create token akin
```

**warning**
the following gives all serviceaccount permissions to view everything, such that the dashboard is actually populated

```
kubectl create clusterrolebinding permissive-binding \
  --clusterrole=cluster-admin \
  --user=admin \
  --user=kubelet \
  --group=system:serviceaccounts
```
