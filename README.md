# Demos Google Container Engine - Using Persistent Disks with WordPress and MySQL

[![GitHub license](https://img.shields.io/github/license/mashape/apistatus.svg)](https://github.com/rafaelsf80/d4wretail/blob/master/LICENSE.txt)

## Demo 1: Using Persistent Disks with WordPress and MySQL

Refer to the files in this directory, specially [the script](https://github.com/rafaelsf80/demo-gke/blob/master/script-wordpress.sh)

Follow [this tutorial](https://cloud.google.com/container-engine/docs/tutorials/persistent-disk/)


## Demo 2: Load Balancing with nginx using an ingress object

See info on ingress object [here](http://blog.kubernetes.io/2016/03/Kubernetes-1.2-and-simplifying-advanced-networking-with-Ingress.html)

Kubernetes supports by default a network load balancer. For HTTP load balancer, you should use an Ingress object instead

```
      # Create cluster on Google Container Engine (by default, it creates 3 nodes)
      gcloud container clusters create demo-nginx
      # OPTIONAL: if more than 1 cluster, make sure you will act on your cluster
      gcloud container clusters get-credentials demo-nginx
      # Create a pod with a single nginx server
      kubectl run nginx --image=nginx --port=80
      # Create pods with nginx, note type is not LoadBalancer, but NodePort
      kubectl expose deployment nginx --target-port=80 --type=NodePort
      # See status of deployment
      kubectl get pods -owide
      # Create the ingress
      kubectl create -f basic-ingress.yaml
      # Monitor (wait until 3 servers are identified)
      kubectl get ingress basic-ingress --watch
      # Find IP address of the ingress object (access with http://<IP_ADDRESS> to see your nginx running)
      kubectl get ingress basic-ingress
      # Delete the ingress object
      kubectl delete -f basic-ingress.yaml
      # Shut down and delete nginx
      kubectl delete -f basic-ingress.yaml
      
      
```



