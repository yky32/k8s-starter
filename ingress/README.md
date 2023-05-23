# k8s Ingress
https://kubernetes.io/zh-cn/docs/concepts/services-networking/ingress/

Default Command
```bash
kubectl create deployment demo --image=httpd --port=80 --dry-run=client -o yaml > demo-deployment.yaml
kubectl expose deployment demo --dry-run=client -o yaml > demo-service.yaml
kubectl create ingress demo-localhost --class=nginx --rule="demo.localdev.me/*=demo:80" --dry-run=client -o yaml > demo-rewrite-ingress.yaml
```
### Routing by Domain

The most common way to route traffic with ingress is by domain:

* https://public.service-a.com/ --> Ingress --> k8s service --> http://service-a/
* https://public.service-b.com/ --> Ingress --> k8s service --> http://service-b/



## TLS
```yaml
apiVersion: v1
kind: Secret
metadata:
  name: testsecret-tls
  namespace: default
data:
  tls.crt: base64 编码的证书
  tls.key: base64 编码的私钥
type: kubernetes.io/tls
---
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: tls-example-ingress
spec:
  tls:
    - hosts:
        - https-example.foo.com
      secretName: testsecret-tls
  rules:
    - host: https-example.foo.com
      http:
        paths:
          - path: /
            pathType: Prefix
            backend:
              service:
                name: service1
                port:
                  number: 80
```