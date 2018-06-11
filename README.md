# k8s-minikube-tutorial

[https://kubernetes.io/docs/tutorials/hello-minikube/](https://kubernetes.io/docs/tutorials/hello-minikube/)

- `brew cask install minikube virtualbox [vagrant] [vagrant-manager]`
    -  on macOS High Sierra to debug
        - `brew cask install --force [package] --verbose --debug`
        - may have to allow the desired developer from the Security & Privacy panel in System Preferences
- `minikube start`
    - to debug: `minikube logs -f`
- `minikube dashboard`

### build docker image

```
cd hellonode
eval $(minikube docker-env)
docker build -t hello-node:v1 .
```

### create deployment

- `kubectl run hello-node --image=hello-node:v1 --port=8080`
    - `kubectl run hello-node --image=hello-node:v1 --port=8080 --replicas=4`
- `kubectl scale deployment hello-node --replicas=8`

### create a service

- `kubectl expose deployment hello-node --type=LoadBalancer`
    - standard way to expose a service to the internet
- `kubectl expose deployment hello-node --type=NodePort`
    - most primitive way to get external traffic directly to the service
    - opens specific port on all the nodes (VMs), and any traffic that is sent to this port is forwarded to the service
    - can only have one service per port
- `minikube service hello-node`
    - `minikube service hello-node --url`

### update image of deployment

- `kubectl set image deployment/hello-node hello-node=[image:tag]`

### kubectl commands

- `kubectl config use-context minikube`
- `kubectl config view`
- `kubectl cluster-info`
- `kubectl get services`
- `kubectl get deployments`
- `kubectl get pods`
- `kubectl get events`

### minikube commands

- `minikube status`

