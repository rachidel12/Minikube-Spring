# Minikube & Spring Boot Deployment Guide

This guide outlines the process of setting up a Kubernetes environment using Minikube and deploying Spring Boot applications.

1. we begin by installing minikube
2. configuring kubectl to talk with the cluster named minikube:
<br>
```kubectl config use-context minikube```

3. getting the info of the cluster: kubectl cluster-info
4. to access to minikube Dashboard: minikube Dashboard

5. we create 2 simple spring boot projetcs: "backend" and "frontend"

6. run the command: mvn clean packages in order to create the jar artefact of each project

- to run or use docker on your local docker images on your minikube cluster, run this commad before step 7:
<br>
```& minikube -p minikube docker-env --shell powershell | Invoke-Expression```

7. ****** we build now our docker images for the 2 projects:
<br>
```docker build --file=Dockerfile --tag=demo-backend:latest --rm=true .```
<br><hr>
```docker build --file=Dockerfile --tag=demo-frontend:latest --rm=true .```

8. we run the two following commands to create our services and deployments from their respective files:
<br>
```kubectl create -f backend-deployment.yaml```<hr>
```kubectl create -f frontend-deployment.yaml```

-  we created the demo-backend service using the type ClusterIP that disable any external traffic to call the service from the outside of the cluster but the demo-frontend project used the tyoe NodePort that let us call the service from the outside of the cluster 

-  to check for your deployments and services run these commands:
```kubectl get deployments```
```kubectl get services```

-  to delete a deployment or service, we run the following commands:
<br>
```kubectl delete service <service_name>```<hr>
```kubectl delete deployment <deployment_name>```

9.  to strat the minikube-frontend-service, we run this command to access to our application from our browser:
<br>
```minikube service minikube-demo-frontend ```


****** if you want to try this second method that let us push our local Docker image directly to Minikube, which will save time from building the images in Minikube again: 
	minikube image load demo-backend
