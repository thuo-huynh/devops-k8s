kubectl apply -f configmap.yml

kubectl get configmap myapp-config -o yaml

kubectl get po

kubectl exec -it myapp-deployment-5b644d47f4-mnnnf -- sh

kubectl get svc

kubectl apply -f configmap.yml

kubectl apply -f configmap.yml

kubectl rollout restart deploy myapp-deployment

# Secret

kubectl apply -f secret.yml

kubectl get secret myapp-secret -o yaml