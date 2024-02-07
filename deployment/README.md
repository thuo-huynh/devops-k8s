# Update deployment

kubectl set image deployment <deployment-name> <container-name>=<new-image>
kubectl set image deployment hello-app hello-app=080196/hello-app:v2

# Verify update

kubectl rollout status deploy hello-app

# New version 
kubectl set image deployment hello-app hello-app=080196/hello-app:v3

# Rollback 
1. Check revision
kubectl rollout history deploy hello-app

2. Rollback
kubectl rollout undo deployment hello-app --to-revision=2

# Delete deployment
kubectl delete -f hello-deploy.yaml