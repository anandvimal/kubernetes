update ClusterIP to Nodeport:
```
kubectl patch service nginx -p '{ "spec": {"type": "NodePort"} }'
```

how to find the port for nodeport?
kubectl get service nginx

how to find ip for nodeport?
kubectl get nodes

kubectl describe node nodename | grep InternalIP:

>now you can do curl nodeIP:nodePort and verify the results.

Network Policies:
podSelector: Selects pods in the namespace to apply the network policy to
policyTypes: Defines the type of traffic.
ingress: list rules for incoming traffic. Each rule can define from and ports section.
egress: list rules for outgoing traffic. Each rule can define to and ports section.

sample networking policy in declaration file:

networkpolicy-api-allow.yaml
```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: api-allow
spec: 
  podSelector: 
    matchLabels:
      app: payment-processor
      role: api
    ingress:
    - from:
      - podSelector:
        matchLabels:
        app: coffeeshop
```

to apply above policy run a pod that matches it:
kubectl run payment-processor --image=nginx --restart=Never -l app=payment-processor,role=api --port=80

check if pods are applied (also note down the pod ip, we will use this to test reaching to pod): 
kubectl get pods -o wide

then apply above policy:
kubectl create -f networkpolicy-api-allow.yaml


to test the above networking policy try (traffic should be blocked for this as label selector does not match policy):
kubectl run grocery-store --rm -it --image=busybox --restart=Never -l app=grocery-store,role=backend -- /bin/sh 
# wget --spider --timeout=1 10.0.0.51 
10.0.0.51 is pod ip of payment-processor pod.

(traffic from this one should reach the )
kubectl run coffeeshop --rm -it --image=busybox --restart=Never -l app=coffeeshop,role=backend -- /bin/sh
# wget --spider --timeout=1 payment-pod-ip

---

get network policies:
kubectl get networkpolicy

details of a networkpolicy:
kubectl describe networkpolicy api-allow

---

Isolating all pods in a namespace


```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: default-deny-all
spec:
  podSelector: {}
  policyTypes:
  - Ingress
  - Egress
```

podSelector: {}, means it will select all the pods. 



restricting access to Ports
```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: port-allow
spec:
  podSelector:
    matchLabels:
      app: backend
  ingress:
  - from:
    - podSelector:
      matchLabels:
        app: frontend
    ports:
    - protocol: TCP
      port: 8080
```










































