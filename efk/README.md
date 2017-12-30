### efk addon on minikube

```
minikube addons enable efk
kubectl apply -f efk.yaml
echo "$(minikube ip) kibana.minikube kibana.local grafana.minikube grafana.local" | sudo tee -a /etc/hosts

```
