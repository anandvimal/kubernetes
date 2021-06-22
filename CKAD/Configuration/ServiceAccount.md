create a service account: 

```
kubectl create serviceaccount dashboard-sa
```

to get service accounts do: 

```
kubectl get serviceaccount
```

get details of a service account
```
kubectl describe serviceaccount dashboard-sa
```

add this to pod:

```
spec:
  containers:
  - name:
    image: 
  serviceAccount: dashboard-sa
```


to disable mounting any service account to a pod/deployment etc add:
```
spec: 
  automountServiceAccountToken: false
```
