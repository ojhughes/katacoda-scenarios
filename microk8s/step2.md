# Testing the cluster by deploying a Hello World API

You might have noticed we added the argument `--k3s-extra-args '--no-deploy traefik'` when deploying the K3s master node.
This is so we can use [metal-lb](https://metallb.universe.tf) to allocate an individual IP address to any services we deploy.
This is more convenient than having to set up port forwarding for each service. This script can be used to deploy metal-lb
to our cluster

`./metallb-config/deploy-metallb.sh`{{execute}}

Now we can deploy a real web API to our cluster and see that it is assigned a new IP address that we can use to access it.

`kubectl apply -f https://raw.githubusercontent.com/paulbouwer/hello-kubernetes/master/yaml/hello-kubernetes.yaml`{{execute}}

Now we can find the service IP and access the API:

```
kubectl get svc hello-kubernetes --watch
```{{execute}}

If we get our new service, it will display PENDING. Wait until the external IP is allocated and then press CTRL+C and test that we can access that IP by running a `curl` command.
