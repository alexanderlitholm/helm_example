# **Helm example with wordpress**
### **Installation and Setup**
* Create your cluster using kind:<br>`kind create cluster`
* Install the ingress-nginx and create the namespace: <br>`helm upgrade
--install ingress-nginx ingress-nginx
--repo https://kubernetes.github.io/ingress-nginx 
--namespace ingress-nginx --create-namespace`
* Install wordpress using Helm:<br>`helm install happy-panda bitnami/wordpress`
* Create the ingress resource:<br>`kubectl create ingress wordpress-localhost
--class=nginx
--rule=wordpress.localdev.me/*=happy-panda-wordpress:80`
* Run a port-forward toward the ingress-controller:<br>`kubectl port-forward --namespace=ingress-nginx service/ingress-nginx-controller 8080:80`
* Visit your <a href="wordpress.localdev.me:8080">site</a> or as <a href="wordpress.localdev.me:8080/admin">site_admin</a>