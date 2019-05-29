#KUBECTL Commands

##Replica sets and Replication Controller
### Difference between Replica sets and Replication Controller
    selector:
        matchLabels:
        type: front-end

###Create
`kubectl create -f rs-definition.yml`

###Get
`kubectl get replicaset`

##Delete and remove underlying pods
`kubectl delete replicaset [name]` 

###Scaling up
Change the file definition and replace

`kubectl replace -f rs-definition.yml`

Change inline, but file remains unchanged

`kubectl scale --replicas=6 -f rs-definition.yml`