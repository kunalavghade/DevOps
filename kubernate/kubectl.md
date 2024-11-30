## Pods

    DESCRIPTION:
        Pod is a collection of containers that can run on a host. This resource is
        created by clients and scheduled onto hosts.

get Explain
```
kubectl explain pods
```

List all pods (-o wide for more info)
```
kubectl get Pods -o wide
```

Get Details of pod
```
kubectl describe pod <podID>
```



Update deployment
```
kubectl set image deployment <name> <container-name>=image-name:tag
```