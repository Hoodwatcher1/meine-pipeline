# DevOps Pipeline Demo

Eine vollständige CI/CD Pipeline mit automatischem Deploy in Kubernetes.

## Tech Stack

- **Kubernetes (k3s)** – Container Orchestrierung
- **Docker** – Containerisierung
- **GitHub Actions** – CI/CD Pipeline
- **nginx** – Webserver

## Architektur
```
git push → GitHub Actions → Docker Build → k3s Import → Kubernetes Rollout
```

## Was diese Pipeline macht

1. Bei jedem Push auf `main` startet die Pipeline automatisch
2. Docker Image wird gebaut
3. Image wird in den lokalen k3s Cluster importiert
4. Kubernetes rollt die neue Version auf alle 5 Pods aus
5. Zero-Downtime Deployment durch Rolling Update Strategie

## Setup

### Voraussetzungen
- Linux
- Docker
- k3s
- GitHub Actions Self-hosted Runner

### Installation
```bash
# k3s installieren
curl -sfL https://get.k3s.io | sh -

# Deployment anwenden
sudo kubectl apply -f deployment.yaml
sudo kubectl apply -f service.yaml
```

### App aufrufen
```bash
sudo kubectl get service meine-app-service
# App läuft auf http://localhost:<NodePort>
```

## Kubernetes Setup

- **5 Replicas** für Hochverfügbarkeit
- **Self-Healing** – ausgefallene Pods werden automatisch neu gestartet
- **Rolling Updates** – Zero-Downtime Deployments
