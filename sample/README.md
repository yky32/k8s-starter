```bash
kubectl create deployment demo --image=httpd --port=80 --dry-run=client -o yaml > demo-deployment.yaml
kubectl expose deployment demo --dry-run=client -o yaml > demo-service.yaml
kubectl create ingress demo-localhost --class=nginx --rule="demo.localdev.me/*=demo:80" --dry-run=client -o yaml > demo-minimal-ingress.yaml
```