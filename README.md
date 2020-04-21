# Jitsi in Kubernetes

This Guide for set-up Jetsi components on Kubernetes cluster

## Creating Namespace

```bash
kubectl create namespace jitsi
```

### Create Secrets , You should replace `...` with secret passphare

```bash
kubectl create secret generic jitsi-config -n jitsi --from-literal=JICOFO_COMPONENT_SECRET=... --from-literal=JICOFO_AUTH_PASSWORD=... --from-literal=JVB_AUTH_PASSWORD=...
```

#### create ssl certificate using Lets Encrypt 
```bash
certbot -d linuxawy.co --manual --preferred-challenges dns certonly
```
#### adding certificate to k8s secrets 
```bash
kubectl create secret tls tls-secret --key privkey.pem --cert cert.pem -n jitsi
```

#### Deploy all services 

```bash
kubectl create -f jvb-service.yaml
kubectl create -f deployment.yaml
kubectl create -f web-service.yaml
```


Congratulations you finished setup all Jitsi Services/Deployments on your cluster now you should visit your domain after point the DNS record to your ingress ip.
