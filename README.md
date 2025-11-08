# Harden-Kubernetes-security

## Install MongoDb database

1. Create the pvc ( where mongodb data will be persisted inside our machine)
```bash
kubectl apply -f mongo/manifests/pvc.yaml -n pi
```
2. Create the secret
```bash
kubectl apply -f mongo/manifests/secret.yaml -n pi 
```
3. Create the configmap
```bash
kubectl apply -f mongo/manifests/configmap.yaml -n pi 
```
2. Deploy the Mongodb Database
```bash
kubectl apply -f mongo/manifests/statefulset.yaml -n pi 
```

## Deploy the backend
1. Build the docker image
```bash
docker builder build -t to-do-backend:v1 backend/
# docker push  soulredouane/to-do-backend:v1 
```
2. Create the deployment ( deploy the backend)
```bash
kubectl apply -f backend/manifests/deployment.yaml -n pi
```
3. Create the service
```bash
kubectl create -f backend/manifests/service.yaml -n pi
```
## Deploy the frontend
1. Build the docker image 
```bash
docker builder build -t to-do-frontend:v1 frontend/. 
```
2. Create the deployment ( deploy the frontend)
```bash
kubectl apply -f frontend/manifests/deployment.yaml -n pi
```
3. Create the service 
```bash
kubectl apply -f frontend/manifests/service.yaml -n pi
```

## Create port forwarding to access the application from the browser
open to shell terminall and run in each one of the bellow commands 

1. in first shell run the following command 
```bash


## Install Some usefull tools 
1. Install Metric server
```bash
# Add the metrics-server repository
helm repo add metrics-server https://kubernetes-sigs.github.io/metrics-server/
helm repo update

# Install metrics-server
helm install metrics-server metrics-server/metrics-server --namespace kube-system
```
`note`: this command migh not work if you're using k8s via docker


















## Some Debuging command 
1. check if mongodb db exist 
```bash
kubectl exec -it pod-name -- sh 
mongosh "mongodb://admin:Password123$@127.0.0.1:27017/pi_db"
```



## Next To DO Tasks 
2. install nginx ( ingress-controller) via helm
1. Create ingress to expose booth the backend and frontend 
3. Install Cert-manager via helm ( let's encrypt) 
4. create a cluster issuer ( use http-01 challenge)
5. expose your application to the outside via https 








