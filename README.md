# Microservices Setup Guide
## Prerequisites
Before starting, ensure the following tools are installed:
- Docker Desktop  
- Kind  
- Kubectl  
- Go  
- JDK 21  
- MySQL Workbench (to view `order` and `inventory` databases)  
---
## Docker Login
```bash
docker login -u <username>
Steps:
mvn spring-boot:build-image -DskipTests -DdockerPassword=
1. cd .\k8s\kind\ 
2. kind create cluster --name microservices --config kind-config.yaml
3. cd .\k8s\mainifests\
4. kubectl apply -f infrastructure
Common kubectl-commands:
kubectl get pods
kubectl get svc -> to get services name with ports they are in running
kubectl logs -f <pod-name>
kubectl port-forward svc/<svc-name> <port-forwarding-from>:<port-forwarding-to>
kubectl get all (to get all details of pods, service, deployment replicaset)
kubectl get secrets
kubectl get configmap
kubectl get pvc
kubctl get pv
When changed in frontend:
cd .\microservices-shop-frontend\
docker build -t microservices-shop-frontend .
docker tag microservices-shop-frontend:latest gokuooo/microservices-shop-frontend:latest  
docker push gokuooo/microservices-shop-frontend:latest
cd .\k8s\manifests\applications\
kubectl delete -f microservices-shop-frontend.yml
kubectl apply -f microservices-shop-frontend.yml
When images are loaded from docker-hub (manifests -> application files are retriggered):
problem occured --> " new- " keyword
1. Remove new keyword
2. Go to ./k8s/manifests
3. kubectl apply -f applications
4. kubectl rollout restart deployment api-gateway
5. Do 4th step whereever you changed
6. kubectl get pods (STATUS = RUNNNING)
