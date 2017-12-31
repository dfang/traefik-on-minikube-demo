### Traefik on minikube



#### 1. install traefik as daemonset

```
kubectl apply -f https://raw.githubusercontent.com/containous/traefik/master/examples/k8s/traefik-ds.yaml
```

#### 2. whoami demo

create whoami deploments and expose as service  

```
kubectl run whoami --image=emilevauge/whoami --port=80 --replicas=5
kubectl expose deployment whoami --type=NodePort
```
or

```
kubectl run whoami --image=emilevauge/whoami --port=80 --replicas=5 --expose 
```

create ingress for whoami  

```
kubectl create -f whoami.ingress.yaml
```

Add dns records to /etc/hosts

```
echo "$(minikube ip) traefik-ui.minikube" | sudo tee -a /etc/hosts
echo "$(minikube ip) whoami.minikube" | sudo tee -a /etc/hosts
```

#### 3. open http://whoami.minikube, refresh and watch Hostname  

```
open http://whoami.minikube
```




install traefik as daemonset, otherwise you need to use NodePort to access traefik dashboard. see this [issue](https://github.com/containous/traefik/issues/2633)
