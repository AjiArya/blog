---
title: "Cara Memasang Nginx Ingress Controller Pada Kubernetes Cluster [External IP]"
description: "Cara mudah memasang nginx ingress controller pada kubernetes cluster"
date: "2021-08-29"
tags: ["Kubernetes", "Nginx", "Ingress"]
categories: ["Kubernetes"]
ShowToc: true
TocOpen: true
---

# Prasyarat
- Kubernetes Cluster

# Panduan
1. Terapkan manifest yang disediakan pada website nginx
```bash
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v1.0.0/deploy/static/provider/baremetal/deploy.yaml
```

2. Sunting service `ingress-nginx-controller` pada namespace `ingress-nginx`

Isikan dengan IP Node kubernetes yang akan melayani _request_
```bash
kubectl -n ingress-nginx edit svc ingress-nginx-controller
```

Tambahkan baris berikut
```yaml
spec:
  externalIPs:
  - <IP_NODE_1>
  - <IP_NODE_2>
  - <IP_NODE_N>
```


# Referensi
- [Deploy Nginx Controller on Baremetal](https://kubernetes.github.io/ingress-nginx/deploy/#bare-metal)
- [Expose Nginx via ExternalIPs](https://kubernetes.github.io/ingress-nginx/deploy/baremetal/#external-ips)
