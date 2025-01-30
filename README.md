# Devops_Final_Project_Ih

## Overview

This project demonstrates the development, containerization, Inrastructure using terraform, deployment, and continuous integration (CI) and continuous delivery (CD) of a web application. 

The project is structured into four parts:

1. **Containerization of Microservices**: Dockerize the frontend, backend, and database.
2. **Infrastrucure using Terraform**: Provision EKS cluster.
3. **Kubernetes Deployment**: Deploy the application on Kubernetes (Amazon EKS).
4. **Continuous Integration (CI)**: Implement a CI pipeline using GitHub Actions.
5. **Continuous Delivery (CD)**: Implement a CD pipeline to deploy the application to Amazon EKS.
6. **Monitoring**: Monitering using Prometheus and Grafana

## Pre-requisites

Before you start, make sure you have the following:

- A **host machine** with **Docker** and a **Kubernetes cluster** (EKS) installed.
- An **AWS account** with valid IAM user permissions.
- Basic knowledge of Docker, Kubernetes, and GitHub Actions.

## Project Structure

- `expensy_backend`: Backend application code.
- `expensy_frontend`: Frontend application code.
- `Mongodb and Redis`: Database used in the project.

## Containerize All Microservices

In this part, we containerize the frontend and backend  applications using Docker.

### Steps:

1. **Create Docker Images**: 
   - Frontend and Backend containers should be created using Dockerfiles.
   - Ensure that Docker network settings are configured to allow communication between the containers.
   
2. **Run the Application Locally**:
   - Deploy the containers locally using Docker and verify the application is running successfully.
   

## Deploy the Application on Kubernetes

In this part, we deploy the containerized application on Kubernetes (Amazon EKS).

### Steps:

1. **Deployment Manifests**:
   - Create Kubernetes manifests for the frontend, backend, Mongodb and Redis services.
   - Deploy the frontend , backend , and database.

2. **Service Configuration**:
   - Create a **Load Balancer** service for the frontend and backend applications.
   - Create **ClusterIP** services to connect the frontend and backend, and the backend with Mongodb and Redis.
   - Use **Persistent Volume** on Amazon EFS to store Mongodb and Redis data.


## Continuous Integration (CI)

In this part, we implement a CI pipeline using **GitHub Actions**.

### Steps:

1. **Build, Test, and Scan**:
   - Add a step to build, test, and scan the frontend and backend code.
   
2. **Create Docker Images**:
   - Add steps to create Docker images for both frontend and backend.
   - Push these images to **Docker Hub**.
   
3. **Deploy Using Manifests**:
   - Include Kubernetes manifests for creating deployments and services in the pipeline.

## Continuous Delivery (CD)

In this part, we implement a CD pipeline to deploy the application to Amazon EKS.

### Steps:

1. **Connect to EKS Cluster**:
   - Add steps to connect to the **Amazon EKS** cluster using the correct IAM permissions.

2. **Deploy Using kubectl**:
   - Use `kubectl apply` commands in the pipeline to deploy all Kubernetes deployments and services.

3. **Verify Application**:
   - Ensure that the application is running successfully on the EKS cluster.

## Setting Up the Project

### Docker Setup

1. Build and run the Docker containers:

   ```bash
   docker build -t dsunitha/final_frontend .
   docker build -t dsunitha/final_backend .

2. Push the Docker images:
   
   ```bash
   docker push dsunitha2/final_backend
   docker push dsunitha2/final_frontend
   
### Kubernetes Setup
1. Ensure you have a Kubernetes cluster (EKS) running and kubectl is configured.

2. Apply the Kubernetes manifests:
   
   ```bash
          kubectl apply -f backend-deployment.yml --validate=false
          kubectl apply -f backend-service.yml --validate=false
          kubectl apply -f database-deployment.yml --validate=false
          kubectl apply -f database-service.yml --validate=false
          kubectl apply -f database-pv.yml --validate=false
          kubectl apply -f database-pvc.yml --validate=false
          kubectl apply -f frontend-deployment.yml --validate=false
          kubectl apply -f frontend-service.yml --validate=false
          kubectl apply -f redis-deployment.yml --validate=false
          kubectl apply -f redis-service.yml --validate=false
          kubectl apply -f redis-pv.yml --validate=false
          kubectl apply -f redis-pvc.yml --validate=false

3. Ensure pods are running:
    ```bash
     kubectl get pods
     kubectl get services

### Github Actions Setup

Set up GitHub Actions by creating a  .github/workflows/ci.yml file with the necessary steps.

1. Building and testing code.
2. Creating Docker images and pushing to Docker Hub.
3. Deploying the application to EKS

### Monitoring Setup
1. Install and add helm repositories
2. Install Prometheus and Grafana
3. Expose Prometheus and Grafana services with Load Balancer
4. Monitor the performance of your Kubernetes cluster using Grafana’s rich dashboard and Prometheus’s powerful metrics collection
