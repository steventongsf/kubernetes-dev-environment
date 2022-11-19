# Vagrant managed Kubernetes environment for a single machine

## Kubernetes Environment
* Kubernetes 1.23
* Ubuntu 22.04

## Tested Environments
### Windows 

* Windows 11
* Vagrant 2.3.3
* VirtualBox 7.0.2

## Vagrant Usage

## Kubernetes Usage
Coming soon

## list pods on master
kubectl get pods -n kube-system 

## check networking
kubectl get svc -n kube-system 

## configuration
kubectl --namespace kube-system get configmap kubeadm-config -o yaml

## view nodes
kubectl get nodes

# view dashboard
kubectl proxy
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/#/login
use configs/token to login

## List all pods in namespace

kubectl get po -n kube-system

# deploy sample application
kubectl apply -f ./apps/nginx-example/deployment.yml

# test deployed application
http://10.0.0.11:32000


