# Command

kubectl apply -f hello-kube.yaml
kubectl get pod

# Get pod with label

kubectl get pod -l app=ui

kubectl get pod -l app=system

# Get namespace

kubectl get ns

# List out all resource from namespace

kubectl get pod --namespace kube-system

# Create a namespace

kubectl create ns testing

# Create pod

kubectl apply -f hello-namespace.yaml

# Check pod is created with namespace testing

kubectl get pod -n testing

# Delete

kubectl delete pod hello-kube-testing -n testing
