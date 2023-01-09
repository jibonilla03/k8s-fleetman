# Cluster
```
kubectl version
kubectl config view
kubectl get all
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

```
# Services
```
$ kubectl describe service fleetman-webapp
```
# Deployments
```
$ kubectl get deployments

$ kubectl rollout history deployment/nginx-deployment

$ kubectl rollout history deployment/nginx-deployment --revision=2

$ kubectl rollout undo deployment/nginx-deployment

$ kubectl get deployment nginx-deployment
```