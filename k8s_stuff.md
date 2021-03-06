# KUBECTL

#  Contexts
Contexts are defined in your .kube/config file

Show available Contexts
```bash
kubectl config get-contexts
```
Get Current Context
```bash
kubectl config current-context
```
Set Current Contexts
```bash
kubectl config set current-context [Context]
```

## Basics

Show pods
```bash
kubectl -n [namespace] get pods
```
Describe a pod
```bash
kubectl -n [namespace] describe pods [podname]
```
View container logs (with tail)
```bash
kubectl -n monitoring logs --tail 100  pods/ingress-nginx-thanos-grpc-controller-5d6b76f7c7-hvq4x -f
```
View configmaps
```bash
kubectl -n monitoring describe configmaps ingress-nginx-thanos-grpc-controller
```
Describe Ingress
```bash
kubectl -n monitoring describe ingress thanos-grpc
```
Get Services
```bash
kubectl -n monitoring get service
```
Local Port Forward
```bash
kubectl -n monitoring port-forward pods/thanos-querier-59d64746cd-6plhh 10901:10901
```
Restart a pod
```bash
kubeclt -n monitoring delete [pod]
```

# Deployments

Show deployments for a namespace
```bash
kubectl -n monitoring get deployment
```
Perform a Rolling restart of a deployments
```bash
kubectl -n monitoring rollout restart deployment [deployment]
```


## Exec Commands In a container.

View nginix ingress config
```bash
kubectl exec -it -n monitoring ingress-nginx-thanos-grpc-controller-5d6b76f7c7-hvq4x -- cat /etc/nginx/nginx.conf
```
Open a shell in the container
```bash
kubectl exec -it -n monitoring ingress-nginx-thanos-grpc-controller-5d6b76f7c7-hvq4x -- /bin/sh
```

# Kubernetes Secrets
SSL Cert Example
```bash
kubectl -n [namespace] create secret tls [secret name] --key [file with key] --cert [file with cert]
```
File Example
Yaml file containing AWS S3 Credentials
```Yaml
type: S3
config:
  bucket: bucket
  endpoint: s3.us-west-2.amazonaws.com
  region: [region]
  access_key: xxxxxxxxx
  insecure: false
  signature_version2: false
  secret_key: xxxxxxx
```
Create Secret Example
```bash
kubectl -n monitoring create secret generic thanos-objstore-config --from-file=objstore.yml=/path/to/yaml/in/git/storage-secret.yaml
```
Update Secret
update the keys in the yaml
```bash
kubectl -n monitoring create secret generic thanos-objstore-config --from-file=objstore.yml=/path/to/yaml/in/git/storage-secret.yaml --dry-run -o yaml | kubectl apply -f -
```



# HELM

helm deploy

```bash
helm upgrade [realease] [chart] [flags]
```

Examples:
Thanos
* in git location for values file  (eg. Magnite/helm-bitnami_thanos_values)
```bash
helm upgrade thanos helm-bitnami/thanos --install -n monitoring -f values/dev/las2.yaml --version 2.3.4
```

Nginx ingress
```bash
helm upgrade ingress-nginx-thanos-grpc helm-github.io-kubernetes-ingress-nginx/ingress-nginx --install -n monitoring -f values/dev/las2.yaml --version 3.7.1
```
