# Deploying and Testing PrestaShop with MySQL on Kubernetes

This repository contains the necessary files to deploy and test PrestaShop with MySQL on a Kubernetes cluster. Follow the steps below to get started.

## Prerequisites

- A running Kubernetes cluster
- `kubectl` command-line tool installed
- Git installed on your local machine

## Clone the Repository

1. Open your terminal or command prompt.

2. Change to the directory where you want to clone the repository.

3. Run the following command to clone the repository:

```
git clone https://github.com/NikFD03/prestashop.git
```

## Deploy PrestaShop and MySQL

1. Change to the cloned repository directory:  
```
cd prestashop
```
2. Review and modify the YAML files in the `k8s` directory if needed. These files contain the Kubernetes manifests for deploying PrestaShop and MySQL. Adjust any configuration settings or resource allocations according to your requirements.  
3. Create namespace:
```
kubectl create ns prestashop
```
4. Apply the YAML files using `kubectl`:
```
kubectl apply -f mysql-configmap.yaml -n prestashop  
kubectl apply -f mysql-secret.yaml -n prestashop 
kubectl apply -f mysql-storage.yaml -n prestashop 
kubectl apply -f mysql-deployment.yaml -n prestashop 
kubectl apply -f prestashop-service.yaml -n prestashop
kubectl apply -f prestashop-deployment.yaml -n prestashop
```  
This command deploys the PrestaShop and MySQL resources to your Kubernetes cluster.

4. Monitor the deployment process:  
```
kubectl get pods -n prestashop
or 
kubectl get all -n prestashop  
```  
Wait until all the pods are in the `Running` state.  

5. Forward the local port to the PrestaShop service:  
```
kubectl port-forward <name-pod> 80:80 -n prestashop
```  

This command forwards port 8080 on your local machine to port 80 of the PrestaShop service running in Kubernetes.

6. Open a web browser and enter `http://localhost` to access PrestaShop.

7. Follow the on-screen instructions to complete the PrestaShop setup process.

8. Once the setup is complete, you can start testing and using PrestaShop.

## Access and Test PrestaShop

1. Open a web browser and enter the external IP address or hostname of the PrestaShop service obtained in the previous step.

2. Follow the on-screen instructions to complete the PrestaShop setup process.

3. Once the setup is complete, you can start testing and using PrestaShop.

## Cleanup

To clean up the deployed resources, run the following command:
```
kubectl delete -f mysql-configmap.yaml -n prestashop  
kubectl delete -f mysql-secret.yaml -n prestashop 
kubectl delete -f mysql-storage.yaml -n prestashop 
kubectl delete -f mysql-deployment.yaml -n prestashop 
kubectl delete -f prestashop-service.yaml -n prestashop
kubectl delete -f prestashop-deployment.yaml -n prestashop
```  

This command removes all the Kubernetes resources related to PrestaShop and MySQL.