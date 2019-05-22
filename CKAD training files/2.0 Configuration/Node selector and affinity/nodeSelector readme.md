# Node Selector

Node selectors allow pods to be deployed onto specific nodes based on node labels.

Node labels are applied to nodes, this can be done at any time, but usually at cluster creation.

To label nodes use the following command:

Syntax:
```
kubectl label nodes <node-name> <label-key>=<label-value>
```

Example:
```
kubectl label nodes node01 size=Large
```


## **_Limitations of nodeSelector_**

nodeSelector is used to assign a specific node based on labels, however you cannot use node selector if you want to choose multiples of labels e.g. Large _or_ Medium **or** choose a not option e.g. _not_ small.

these options are available with nodeaffinity
