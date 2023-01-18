# Cluster
```
$ kubectl version

$ kubectl config view

$ kubectl get all

$ kubectl get all --namespace kube-system
```
# Namespaces
```
$ kubectl get namespaces
```

# PODs
```
$ kubectl apply -f first-pod.yaml

$ kubectp apply -f .

$ kubectl exec webapp -- ls

$ kubectl -it exec webapp -- sh

$ kubectl get pods

$ kubectl port-forward webapp 30080:80

$ kubectl describe pod webapp

$ kubectl get pods --show-labels

$ kubectl get pods --show-labels -l release=0-5

$ kubectl get pods -o=wide

$ kubectl delete pod webapp-release-0-5

$ kubectl delete pods --all

$ kubectl get pods --namespace kube-system
```
# Services
```
$ kubectl describe service fleetman-webapp

$ kubectl describe svc kube-dns -n kube-system
```
# Deployments
```
$ kubectl get deployments

$ kubectl rollout history deployment/nginx-deployment

$ kubectl rollout history deployment/nginx-deployment --revision=2

$ kubectl rollout undo deployment/nginx-deployment

$ kubectl get deployment nginx-deployment

$ kubectl rollout status deployment/webapp

$ kubectl rollout history deployment/webapp

$ kubectl rollout undo deployment/webapp

$ kubectl rollout undo deployment/webapp --to-revision=2
```

# Replicaset

```
$ kubectl describe rs webapp
```