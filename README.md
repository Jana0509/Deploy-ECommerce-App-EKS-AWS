# Host-E-Commerice- Application-EKS-AWS
Build and Deploy Highly Available, Scalable and Resilient 3-tier microservices solution in Elastic Kubernetes Service

### Introduction:
This Project demonstrates deploying Highly Available, Scalable and Resilient Application in AWS EKS Cluster. This Application consists of 9 Microservices such as User Service(Registration, Login), Shipping Service, Rating Service, Catalogue Service, Cart, Dispatch and Payment Service. All the Microservices are written in different Programming languages such as python, Java, Go, Php.
This Project is designed in 3-tier architecture which consistes of Presentation Layer(UI), Business Logic Layer, Database Layer (Mongo DB and Mysql DB) and included caching layer for the cart service, for caching, we have used Redis in memory store for it.


### Architecture

![eks Microservices](https://github.com/user-attachments/assets/0500a392-23f5-43fb-92ff-8af7847a563e)


### Project Highlights:
1. Containerization:
   * Containerized the 2048 application using docker to ensure consistent runtime environment

2. EKS Cluster:
   * It is fully managed Kubernetes cluster, Created the EKS Cluster from the stratch using EKSCTL utility for creating the Highly availability and resilience solution

3. EKS Nodes:
   * We have used EC2 instances type for running the microservices because Fargate won't support adding Redis cache and EBS Volume for persistent Volumes.

4. Kubernetes Tools:
   * Managed Kubernetes clusters using kubectl, eksctl, and Helm for streamlined operations.

5. Elastic Container Registry (ECR):
   * Set up ECR to store Docker images for streamlined deployment to EKS.

6. Route 53:
   * Created the Route 53 alias record to route traffic to the load balancer

7. Load Balancer:
   * Created and deployed the ALB in public subnet in multiple availability zones for high availabilityy and to route traffic to the fargate in worker nodes using Ingress Controller

8. VPC:
   * Created the Virtual network space from scratch to create the eks cluster in secure environment


### Understanding EKS Cluster:
* Control plane : Managed by AWS, including the components such as API Server, etcd, cloud controller manager, scheduler.
* Woker Nodes: It is handled by us for creating the node group such as EC2 instances or serverless compute as fargate to run the application.
* Integration : AWS eases the process of connecting between control plane and data plane
* Networking: Configured the secure communication between control plane and worker nodes, Secure isolation is created using VPC
* Monitoring and Logging : Integrated cloudwatch for the realtime performance and health tracking

### Resources created for the application:
1. Deployment : It contains the pod configuration such as app docker image and replica set configuration
2. Service : It is used for exposing the apps to external world and perform service discovery using labels and selectors
3. Ingress Resource : It contains the configuration for routing the external traffic to service which inturns reaches the containerized app running in pod
4. ALB Ingress Controller : This controller is deployed in control plane which will watch all the ingress resources and will configure the Load balancer

### Process Followed to Deploy to EKS
1. Dockerized all the services.
2. Created the Deployment and Service files for all the microservices
3. Created the HELM Charts for all the services for ease deployment process and for easy reusability of those services
4. Deploy the Helm Chart in EKS
5. Created the Ingress resource and Ingress ALB
6. Create and configure IAM OIDC provider for creating the communication between the pods and AWS Resources[Create Integration between k8 service and AWS IAM roles]
