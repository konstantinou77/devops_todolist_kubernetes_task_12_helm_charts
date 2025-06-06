# Helm-Based Kubernetes Deployment with Kind

# Project Overview:

This project demonstrates a complete Helm-based Kubernetes deployment of a Django-based ToDo application with a MySQL backend, configured for use with a local kind cluster. The project demonstrates advanced Helm templating techniques, chart dependencies, resource customization, and controlled deployments through values.yaml.

# Tech Stack:

- Kubernetes (kind) – Local K8s cluster setup
- Helm – Kubernetes package manager
- Helm Subcharts – todoapp and dependent mysql
- MySQL – Persistent database (as a Helm subchart)
- Bash – Shell scripting for automated bootstrap

# What Was Done:

- Cluster and Nodes:
- Created a local kind cluster using cluster.yml
- Inspected nodes for labels and taints
- Tainted nodes with label app=mysql using app=mysql:NoSchedule to restrict scheduling of MySQL pods

- Helm Chart Structure:

  - Created a Helm chart todoapp inside the helm-chart/ directory
  - Added a Helm subchart mysql inside helm-chart/todoapp/charts/

- Todoapp Chart Includes:

  - All Kubernetes resource names prefixed with .Chart.Name
  - Namespace, image, secrets, resources, volumes, HPA, affinity - configurable from values.yaml

- Secrets generated dynamically using range and injected as environment variables
- RollingUpdate and resource limits/requests customized via values.yaml
- HPA for CPU/Memory autoscaling with customizable thresholds
- Affinity to schedule pods on specific nodes

- Mysql Subchart Includes:

  - StatefulSet with persistent volume claim
  - Tolerations and node affinity configurable via values.yaml
  - Secrets generation using range for secure DB credentials
  - Resource requests, PVC size, and replica count all configurable

- Created `INSTRUCTION.md` with detailed steps on how to run Helm-Based Kubernetes Deployment with Kind