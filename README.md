
# **Helm example with wordpress**
### **Prerequisites**
* Install <a href="https://github.com/kubernetes-sigs/kind">Kind</a>
    - On Linux: <br>
        ```
        curl -Lo ./kind "https://kind.sigs.k8s.io/dl/v0.11.1/kind-$(uname)-amd64"
        chmod +x ./kind
        mv ./kind /some-dir-in-your-PATH/kind
        ```
* Install <a href="https://helm.sh/docs/intro/install/">Helm</a>
    - From script: <br>
        ```
        curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
        chmod 700 get_helm.sh
        ./get_helm.sh
        ```

- - -
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
* Visit your <a href="http://wordpress.localdev.me:8080">site</a> or as <a href="http://wordpress.localdev.me:8080/admin">site_admin</a>