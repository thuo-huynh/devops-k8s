# Build image

docker build . -t 020896/hello-kube

# Run container

docker run -d --name hello-kube -p 3000:3000 020896/hello-kube

# CURL

curl localhost:3000

# Create pod

kubectl apply -f hello-kube.yaml

# Forward port

kubectl port-forward pod/hello-kube 3000:3000
