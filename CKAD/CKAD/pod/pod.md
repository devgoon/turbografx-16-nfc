#KUBECTL Commands

##PODS
###GET
Lists all the running pods
`kubectl get pods`
Get node info
`kubectl get pod -o wide`
Gets details about the pod 
`kubectl describe pod [pod name]`

###CREATE
Create a pod inline
`kubectl run nginx --image=ngnix`
Create a pod from a file
`kubectl create -f [file name.yml]`

###EDIT
If you don't have the yaml, then generate one from the running pod
`kubectl get pod <pod-name> -o yaml > pod-definition.yaml`
Apply the change
`kubectl apply -f [file name.yml]`
Edit the pod using kubectl directly
`kubectl edit pod <pod-name>`

###DELETE
Delete a pod by name
`kubectl delete pod [pod name]`


