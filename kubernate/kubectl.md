# Kubernetes and Docker Operations Cheat Sheet

## Overview

Overview:
This guide covers commonly used Docker and Kubernetes commands for deploying, scaling, monitoring, and managing applications in a cluster environment. Each command is explained with its purpose and example usage.

---

## Docker Commands

### 1. Run a Container:
```bash
docker run -p 8080:8080 in28min/hello-world-rest-api:0.0.1.RELEASE
```
Purpose: Launches a containerized REST API service locally.

---

##  Kubernetes Commands:

### 1. Deployments

- Create a Deployment:
```bash
kubectl create deployment hello-world-rest-api --image=in28min/hello-world-rest-api:0.0.1.RELEASE
```
Purpose: Creates a deployment with the specified container image.

- Expose the Deployment:
```bash
kubectl expose deployment hello-world-rest-api --type=LoadBalancer --port=8080
```
Purpose: Exposes the deployment via a LoadBalancer on port 8080.

- Scale the Deployment:
```bash
kubectl scale deployment hello-world-rest-api --replicas=3
```
Purpose: Scales the deployment to 3 replicas for load distribution and fault tolerance.

- Update the Deployment Image:
```bashkubectl set image deployment hello-world-rest-api hello-world-rest-api=in28min/
hello-world-rest-api:0.0.2.RELEASE
```
Purpose: Updates the deployment to use a new version of the container image.

- Enable Autoscaling:
```bash
kubectl autoscale deployment hello-world-rest-api --max=10 --cpu-percent=70
```
Purpose: Automatically adjusts the number of Pods based on CPU usage.

- Rollout History:
```bash
kubectl rollout history deployment hello-world-rest-api
```
Purpose: Displays the revision history of the deployment.

- Rollback to a Previous Revision:
```bash
kubectl rollout undo deployment hello-world-rest-api --to-revision=1
```
Purpose: Reverts the deployment to a specific revision.

---

### 2. Pods

- View Pod Details:
```bash
kubectl describe pod <pod-name>
```
Purpose: Displays detailed information about the specified Pod.

- Delete a Pod:
```bash
kubectl delete pod <pod-name>
```
Purpose: Deletes a Pod, prompting the deployment to create a replacement.

- View Logs of a Pod:
```bash
kubectl logs <pod-name>
```
Purpose: Fetches logs for a specific Pod.

- Follow Logs in Real-Time:
```bash
kubectl logs -f <pod-name>
```
Purpose: Follows logs in real-time for the specified Pod.

---

### 3. Cluster Management

- Authenticate and Connect to a GKE Cluster:
gcloud auth login
```bashgcloud container clusters get-credentials in28minutes-cluster --zone us-central1-a 
--project solid-course-258105
```
Purpose: Authenticates and retrieves credentials for accessing a GKE cluster.

- Cluster Information:
```bash
kubectl cluster-info
```
Purpose: Displays detailed information about the cluster.

- Monitor Resource Usage:
kubectl top node
```bash
kubectl top pod
```
Purpose: Shows CPU and memory usage for nodes and Pods.

---

### 4. Resource Configurations

- Export Deployment and Service YAML:
kubectl get deployment hello-world-rest-api -o yaml > deployment.yaml
```bash
kubectl get service hello-world-rest-api -o yaml > service.yaml
```
Purpose: Extracts the configuration of a deployment or service into a YAML file.

- Apply Configuration:
```bash
kubectl apply -f deployment.yaml
```
Purpose: Applies the configuration changes specified in the YAML file.

- Check Differences:
```bash
kubectl diff -f deployment.yaml
```
Purpose: Displays differences between the live configuration and the desired YAML configuration.

- Delete Resources by Label:
```bash
kubectl delete all -l app=hello-world-rest-api
```
Purpose: Deletes all resources with a specific label.

---

### 5. Useful Get Commands

- Get All Resources:
```bash
kubectl get all
```
Purpose: Lists all resources in the current namespace.

- Get Pods:
kubectl get pods
```bash
kubectl get pods -o wide
```
Purpose: Lists Pods in the current namespace, with detailed information using the -o wide option.

- Get Events:
```bash
kubectl get events --sort-by=.metadata.creationTimestamp
```
Purpose: Lists cluster events, sorted by creation timestamp.

- Check Component Health:
```bash
kubectl get componentstatuses
```
Purpose: Displays the health of cluster components.

---

### Additional Notes:

- Use --all-namespaces to query resources across all namespaces.
- Use labels for targeted queries:
  kubectl get pods --all-namespaces -l app=hello-world-rest-api

---

Resources:

- Kubernetes Documentation: https://kubernetes.io/docs/home/
- Docker Documentation: https://docs.docker.com/
- Google Kubernetes Engine (GKE): https://cloud.google.com/kubernetes-engine

---

License:
This cheat sheet is open for use and contributions. Feel free to modify as needed!
