# Kubernetes Nginx Deployment with Minikube

This project demonstrates how to set up a Kubernetes cluster using Minikube, deploy a sample Nginx application, expose it using a service, and access it through a browser.

## 📌 Tools Used

- **Minikube** - Local Kubernetes cluster
- **Docker** - Container runtime
- **kubectl** - Kubernetes CLI
- **YAML** - Configuration files for Deployment & Service

## 📁 Project Structure

```
task5-devops/
│
├── deployment.yaml       # Kubernetes Deployment file
├── service.yaml          # Kubernetes Service (NodePort) file
├── README.md             # This documentation
└── screenshots/          # (Add your terminal & browser screenshots here)
```

## 🚀 Quick Start

### Prerequisites

- Docker installed and running
- Minikube installed
- kubectl installed

### Step 1: Start Minikube Cluster

```bash
minikube start --driver=docker
```

Verify if the node is running:

```bash
kubectl get nodes
```

### Step 2: Deploy Nginx Application

Apply the deployment:

```bash
kubectl apply -f deployment.yaml
kubectl get pods
```

### Step 3: Expose Deployment using Service

Apply the service:

```bash
kubectl apply -f service.yaml
kubectl get svc
```

### Step 4: Access Application

#### Method 1: Using Minikube Service Command

```bash
minikube service nginx-service
```

This will open a browser automatically with a URL like:
```
http://127.0.0.1:61004/
```

#### Method 2: Manual URL

Get the Minikube IP:
```bash
minikube ip
```

Access the application in browser:
```
http://<minikube-ip>:30008
```
Example: `http://192.168.49.2:30008`

### Step 5: Scale Deployment

Scale the deployment to 5 replicas:

```bash
kubectl scale deployment nginx-deployment --replicas=5
kubectl get pods
```

### Step 6: Cleanup

Stop cluster:
```bash
minikube stop
```

Delete cluster completely:
```bash
minikube delete
```

## 📋 Configuration Details

### Deployment Configuration

The `deployment.yaml` file includes:
- **Replicas**: 2 (initially)
- **Image**: nginx:1.21
- **Resources**: CPU and memory limits
- **Health Checks**: Liveness and readiness probes
- **Security**: Non-root user and security context

### Service Configuration

The `service.yaml` file includes:
- **Type**: NodePort
- **Port**: 80 (internal)
- **NodePort**: 30008 (external access)
- **Protocol**: TCP

## 🔍 Useful Commands

```bash
# Check cluster status
kubectl cluster-info

# View all resources
kubectl get all

# Check pod logs
kubectl logs <pod-name>

# Describe resources
kubectl describe deployment nginx-deployment
kubectl describe service nginx-service

# Port forward (alternative access method)
kubectl port-forward service/nginx-service 8080:80
```

## 📸 Screenshots

Add your terminal and browser screenshots to the `screenshots/` directory to document your setup process.

## 🐛 Troubleshooting

### Common Issues

1. **Minikube not starting**: Ensure Docker is running
2. **Pods not ready**: Check `kubectl describe pod <pod-name>`
3. **Service not accessible**: Verify NodePort is correct and firewall settings
4. **Image pull errors**: Check internet connection and image availability

### Debug Commands

```bash
# Check pod status
kubectl get pods -o wide

# View pod events
kubectl get events

# Check service endpoints
kubectl get endpoints nginx-service
```

## 📚 Additional Resources

- [Kubernetes Documentation](https://kubernetes.io/docs/)
- [Minikube Documentation](https://minikube.sigs.k8s.io/docs/)
- [Docker Documentation](https://docs.docker.com/)
