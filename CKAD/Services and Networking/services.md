Services:

Services Types:
ClusterIP: Exposes the Service on a cluster-internal IP. Only reachable from within the cluster.
NodePort: Exposes the Service on each node's IP address at a static port. Accessible from outside of the cluster. 
LoadBalancer: Exposes the Service externally using a cloud provider's load balancer.
ExternalName: Maps a service to a DNS name.

For CKAD focus on ClusterIP and Nodeport.

Creating services:

Imperative command:

format:
```
kubectl create service service-type service-name port-mappings
```
Note: 
- service-type is must as 3rd commandline option, 
- port-mappings is optional
- we will have to edit selector: key:value for service to get the desired pods captured.

eg:
```
kubectl create service clusterip nginx-service --tcp=80:80
```


create a pod and expose it at same time:
```
kubectl run nginx --image:nginx --restart=Never --port=80 --expose
```
creates a pod of named: nginx.
creates a service named: nginx
service type will be clusterIP as its default service type. 


expose a existing deployment: 
```
kubectl expose deployment my-deploy --port=80 --target-port=80
```

Declarattive approach:

```
apiVersion: v1
kind: Service
metadata: 
  name: nginx-service
spec:
  type: ClusterIP
  selector: 
    app: nginx-service
  ports:
    - protocol: 80
      port: 80
      targetPort: 80
```

list services:
```
kubectl get services
```

get service details:
```
kubectl describe service nginx-service
```

Port Mappings:
port: port where service recieves traffic. (incoming port)
target port: port on container. outgoing port from service. 
NodePort: if service is nodeport, this is the port on the k8 node. 

accessing a service with type ClusterIP (commands)

- create a pod and service with same command:
```
kubectl run nginx --image=nginx --restart=Never --port:80 --expose

kubectl get pod,service
```



