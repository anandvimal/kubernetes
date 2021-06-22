to add security context in a pod add to specs:

```
securityContext:
  runAsUser: 1000
  capabilities:
    add: ["MAC_ADMIN"]
```

for containers add same section above to containers: section.

if security context is applied to both container level and pod level. 
container level config > pod level. 

