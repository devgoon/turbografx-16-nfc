#Exam Tips

### Stub out a deployment yaml and write it to
`kubectl run --generator=run-pod/v1 nginx --image=nginx --dry-run -o yaml > nginx-deployment.yml`