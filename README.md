# Minikube NFS Server Provisioner and HTTP Server Setup

---

### Steps

1. **Start Minikube**
   ```bash
   minikube start --cpus=2 --memory=4096
   ```
2. **Configure Docker to Use Minikube's Docker Daemon**
   ```bash
   eval $(minikube docker-env)
   ```
3. **Add Helm Repository and Install NFS Server Provisioner**
   ```bash
   helm repo add stable https://charts.helm.sh/stable 
   helm repo update
   helm install nfs-server-provisioner stable/nfs-server-provisioner --set storageClass.name=nfs-storage
   ```
4. **Create Persistent Volume Claim**
   ```bash
   kubectl apply -f pvc-nfc.yaml
   ```
5. **Create HTTP Server Deployment**
   ```bash
   kubectl apply -f nginx-deployment.yaml
   ```
6. **Create Service for HTTP Server Deployment**
   ```bash
   kubectl apply -f nginx-service.yaml
   kubectl get svc nginx-service
   ```
7. **Create Job to Populate Content on NFS PV**
   ```bash
   kubectl apply -f populate-content-job.yaml
   kubectl get jobs
   ```
8. **Test HTTP Server by Forwarding Port**
   ```bash
   kubectl port-forward svc/nginx-service 8080:80
   ```
   ![image](https://github.com/user-attachments/assets/1f498f34-1453-4927-8de2-0319da819ee2)


   
  
