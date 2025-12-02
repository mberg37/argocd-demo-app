# ArgoCD GitOps Demo Application

En simpel demo-applikation der viser GitOps workflow med ArgoCD på K3s homelab cluster.

## 🎯 Formål

Demonstrere komplet GitOps workflow:
- GitHub som source of truth
- ArgoCD for automatisk deployment
- cert-manager for automatisk HTTPS
- Traefik ingress routing

## 🏗️ Arkitektur

```
GitHub Repository (denne)
    ↓
ArgoCD (overvåger repository)
    ↓
Kubernetes Cluster (deployer automatisk)
    ↓
Traefik Ingress (router traffic)
    ↓
Demo App (nginx med custom HTML)
```

## 📁 Struktur

```
argocd-demo-app/
├── k8s/                      # Kubernetes manifests
│   ├── namespace.yaml        # demo namespace
│   ├── configmap.yaml        # HTML indhold
│   ├── deployment.yaml       # nginx deployment (2 replicas)
│   ├── service.yaml          # ClusterIP service
│   ├── certificate.yaml      # Let's Encrypt SSL cert
│   └── ingress.yaml          # Traefik ingress
└── README.md                 # Denne fil
```

## 🚀 Deployment

### Via ArgoCD (Automatisk - GitOps)

ArgoCD er konfigureret til at overvåge dette repository:

```bash
# ArgoCD Application er allerede oprettet
# Enhver ændring i GitHub deployes automatisk!
```

### Manuel Deployment (Backup)

Hvis du vil deploye manuelt:

```bash
kubectl apply -f k8s/
```

## 🌐 Adgang

**URL**: https://demo.hl.berg-lab.com

- Automatisk HTTPS via Let's Encrypt
- HTTP redirects til HTTPS
- 2 replicas for redundans

## 🔄 GitOps Workflow

1. **Ændre HTML**: Rediger `k8s/configmap.yaml`
2. **Commit & Push**: Push til GitHub
3. **ArgoCD Syncer**: Opdager ændring automatisk
4. **Deployment**: Ny version deployes
5. **Live**: Ændring er synlig på https://demo.hl.berg-lab.com

## 📊 Overvågning

- **ArgoCD Dashboard**: https://argocd.hl.berg-lab.com
- **Traefik Dashboard**: https://traefik.hl.berg-lab.com
- **Grafana**: https://grafana.hl.berg-lab.com

## 🛠️ Teknologier

- **Kubernetes**: K3s cluster (3 nodes)
- **GitOps**: ArgoCD
- **Ingress**: Traefik
- **SSL**: cert-manager + Let's Encrypt
- **DNS**: Cloudflare DNS-01 challenge
- **Webserver**: nginx:alpine

## 📝 Deployment Dato

**Første deployment**: 02-12-2025

---

**Projekt af**: michab
**Domain**: berg-lab.com
**Cluster**: hl.berg-lab.com
