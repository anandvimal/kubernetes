for default limits we need to apply limit range in each namespace:

for memory LimitRange:

```
apiVersion: v1
kind: LimitRange
metadata:
  name: mem-limit-range
spec:
  limits:
  - default:
      memory: 512Mi
    defaultRequest:
      memory: 256Mi
    type: Container
```

https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/memory-default-namespace/


for cpu LimitRange:

```
apiVersion: v1
kind: LimitRange
metadata: 
  name: cpu-limit-range
spec:
  limits:
  - default:
      cpu: 1
    defaultRequest: 
      cpu: 0.5
    type: Container
```

https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/cpu-default-namespace/







