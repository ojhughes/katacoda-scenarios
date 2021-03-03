# Deploying a Kubernetes cluster using Microk8s 

    MicroK8s is a small and fast Kubernetes distribution that can be installed locally, on a dev server or in the cloud. 
    It tracks upstream k8s releases and can be easily set up as a cluster with high availability.
    MicroK8s is suitable for offline development, prototyping, and testing.
    It also provides a built in installer for common k8s extensions such as ingress and service mesh.
    
    We are going to set up a 2 node microk8s cluster and set up the built in docker registry
```
export MASTER_IP=[[HOST_IP]]
k3sup install --ip ${MASTER_IP} --k3s-extra-args '--no-deploy traefik --no-deploy servicelb'
``` {{execute}}

Now that we have a working Kubernetes cluster, we can validate it is working with:
```
export KUBECONFIG="$(pwd)/kubeconfig"
kubectl get nodes -o wide
```{{execute}}

This command should show a single node cluster with the status READY.
