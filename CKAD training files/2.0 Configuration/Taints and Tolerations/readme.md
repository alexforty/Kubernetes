#H1 <b>Taints and Tolerations</b>

Taints and tolerations are used to restrict where the Kubernetes scheduler can place pods in a cluster.

- taints are applied to nodes only
- tolerations are added to pods only

<b> by default the master node in a cluster has a taint on it that blocks the scheduler deploying pods to the master (this can be over written - but is not recommended) </b>

#H3 commands:

#H4 Taints

syntax:
    kubectl taint nodes node-name key=value: tainteffect

example:
    kubectl taint nodes node1 app=tomato:NoSchedule

options:

- NoSchedule: pods without toleration will not be deployed on the node with the taint
- PreferNoSchedule: it is preferred that pods without toleration are not deployed, but it is not guaranteed (e.g. in cases of high utilisation)
- NoExecute: prevents new pods being deployed on the node and if existing pods are not tolerated they will be moved to a different node. 

#H3 Tolerations:

*tolerations are added to pods.*

add a section in the yaml playbook called tolerations (same level as containers element of the yaml file). for example, using the taint above as an example, to add a toleration to the pod, it would look like this:

apiVersion: v1
kind: Pod
metadata:
    name: myapp-pod
spec:
    containers:
        - name: nginx-container
          image nginx
    tolerations:
        - key: "app"
          operator: "eaqual"
          value: "tomato"
          effect: "NoSchedule"

**Taints and tolerations are only meant to restrict nodes from accepting pods. it does not stop a pods with a toleration being added to another node in the cluster.**

*in order to force a pod onto a specific node that is node affinity.*
