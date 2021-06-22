Memory: 

1 G = 1 Gigabyte = 1,000,000,000 bytes
1 M = 1 Megabyte = 1,000,000 bytes
1 K = 1 Kilobyte = 1,000 bytes

1 Gi = 1 Gibibyte = 1,073,741,824 bytes
1 Mi = 1 Mebibyte = 1,048,576 bytes
1 Ki = 1 Kibibyte = 1,024 bytes

CPU: 
1 = 1 CPU = 1000m, 1 AWS vcpu,GCP Core, 1 Azure Core, 1 Hyperthread
0.1 cpu = 100m  (m - milli cycles?)

for resouces: 

```
apiVersion: v1
kind: Pod
metadata: 
  name: simple-webapp-color
  labels: 
    name: simple-webapp-color
spec:
  containers:
  - name: simple-webapp-color
    image: simple-webapp-color
    ports:
      - containerPort: 8080
    resources: 
      requests:
        memory: "1Gi"
	cpu: 1
      limits:
        memory: "2Gi"
	cpu: 2
```

