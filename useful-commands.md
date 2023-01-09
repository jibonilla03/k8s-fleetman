# Cluster
```
kubectl version
kubectl config view
```

# PODs
```
kubectl apply -f first-pod.yaml
kubectl exec webapp -- ls
kubectl -it exec webapp -- sh
kubectl get pods
kubectl port-forward webapp 30080:80
kubectl describe pod webapp
```
# Services
```

```
# Deployments
```
$ kubectl get deployments

$ kubectl rollout history deployment/nginx-deployment

$ kubectl rollout history deployment/nginx-deployment --revision=2

$ kubectl rollout undo deployment/nginx-deployment

$ kubectl get deployment nginx-deployment
```