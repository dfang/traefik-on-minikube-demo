### Traefik on minikube



#### install traefik first

```
helm install -f traefik-values.yaml --name lb --namespace kube-system stable/traefik 
```

#### whoami demo

create whoami deploments and expose as service  

```
kubectl run echoserver --image=gcr.io/google_containers/echoserver:1.4 --port=8080 --replicas=5
kubectl expose deployment echoserver --type=NodePort
```
or

```
kubectl run whoami --image=emilevauge/whoami --port=80 --replicas=5 --expose 
```

create ingress for whoami  

```
kubectl create -f whoami.ingress.yaml
```

#### Add dns records to /etc/hosts

```
echo "$(minikube ip) traefik-ui.minikube" | sudo tee -a /etc/hosts
echo "$(minikube ip) whoami.minikube" | sudo tee -a /etc/hosts
```

#### open http://whoami.minikube and refresh, watch Hostname  

```
open http://whoami.minikube
```








Note: there is no need to add annotation:
  
  ```
  annotations:
    # kubernetes.io/ingress.class: traefik
  ```
  at least, it didn't work on minikube version: v0.24.1 and kubectl version 1.8.4
