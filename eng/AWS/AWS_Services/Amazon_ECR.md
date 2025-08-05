# Amazon ECR (Elastic Container Registry)

> Reference: [AWS docs](https://docs.aws.amazon.com/AmazonECR/latest/userguide/what-is-ecr.html)

<br>

<br>

## What is Amazon Elastic Container Registry?

<br>

- Amazon ECR (Elastic Container Registry) is a **secure**, **scalable**, and **reliable** **Fully-managed Docker Container Image Registry Service**
- ECR provides **resource-based permissions** using `AWS IAM`
  - How?
    - Only specific users or EC2 instances can access ECR repositories and images

- Developers can use their preferred CLI to push, pull, and manage **Docker images**, **OCI (Open Container Initiative) images**, and OCI-compatible artifacts

<br>

<br>

## Components of Amazon ECR

<br>

### Registry

- Amazon ECR Registry can be created for each account, and you can create **image repositories** within the registry to store images

<br>

### Authorization token

- Only authenticated AWS users can **Push / Pull** images to/from Amazon ECR registry

<br>

### Repository

- You can store **Docker images** in Amazon ECR image repositories

<br>

### Repository policy

- You can manage access permissions to repositories and images through **repository policies**

<br>

### Image

- You can **Push / Pull** container images to/from repositories

<br>

<br>

## Features of Amazon ECR

<br>

- You can manage the lifecycle of images in repositories using **Lifecycle policies**
  - You can create policies to remove unused images
- You can use **Image scanning** to help identify **software vulnerabilities** in images 
