# ngic-demo in DigitalOcean

> https://docs.digitalocean.com/tutorials/install-nginx-ingress-controller/

- install `nigc` by `helm`
- setup `A record` for the domain
- create `backend` namespace 
  >`kubectl create ns backend`
- create [cert-manager-issuer.yaml](cert-manager-issuer.yaml)