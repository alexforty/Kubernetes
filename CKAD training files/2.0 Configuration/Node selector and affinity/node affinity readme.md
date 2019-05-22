# Node Affinity

Node affinity feature in Kubernetes provides options such as _OR_ and _NOT_ when selecting nodes for pods.

based on the nodeSelector option detailed in the nodeSelector readme file:

```
nodeSelector:
    size: Large
```

the nodeAffinity option is detailed as below:

```
apiVersion:
kind:
metadata:
    name: myapp-pod
spec:
    containers:
        - name: data-processor
          image: data-processor
    affinity:
        nodeAffinity:
            requiredDuringSchedulingIgnoreDuringExecution:
                nodeSelectorTerms:
                    - matchExpressions:
                        - key: size
                          operator: In
                          values:
                            - Large
```

## Options

for example you may wish to allow the pod to be deployed in Large or medium nodes. There are 2 ways to do it

firstly add - Medium to the list of values under matchExpresions:

```
apiVersion:
kind:
metadata:
    name: myapp-pod
spec:
    containers:
        - name: data-processor
          image: data-processor
    affinity:
        nodeAffinity:
            requiredDuringSchedulingIgnoreDuringExecution:
                nodeSelectorTerms:
                    - matchExpressions:
                        - key: size
                          operator: In
                          values:
                            - Large
                            - Medium
```

secondly you could use the operator 'NotIn' as below:
```
apiVersion:
kind:
metadata:
    name: myapp-pod
spec:
    containers:
        - name: data-processor
          image: data-processor
    affinity:
        nodeAffinity:
            requiredDuringSchedulingIgnoreDuringExecution:
                nodeSelectorTerms:
                    - matchExpressions:
                        - key: size
                          operator: NotIn
                          values:
                            - Small
```

other operators you can use in relation to nodeAffinity are:

- In
- NotIn
- Exists 
- NotExists


## Node Affinity Types

there are currently 2 types of node affinity types available:

- requiredDuringSchedulingIgnoredDuringExecution
- preferredDuringSchedulingIgnoredDuringExecution

|        | DuringScheduling | DuringExecution | Notes  |
|--------|:----------------:|:---------------:|--------|
| Type 1 | Required         | Ignored         | Required means that the scheduler will find a node with the affinity rules to place the pod. if it can't find one, the pod will not be scheduled
| Type 2 | Preferred        | Ignored         | Preferred means try to apply the node affintiy rules, but if you can't put the pod anywhere
| _Type 3_| 