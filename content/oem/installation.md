---
title: "Installation"
menu:
  oem:
    title: "Installation"
    parent: "getting_started"
    weight: 3
---

## Prerequisites

- [Docker](http://docker.com/) or another container runtime
- [AWS CLI]()
- [Skopeo]()

## Pulling the Docker Image 

We distribute Vector Charts OEM as a private Docker image on AWS ECR.

During your onboarding to Vector Charts OEM with the Zydro team, you will receive a set of user-specific, read-only IAM credentials which grant access to pull software from the OEM container registry.

As the first step of the process, wou

### 1. Authenticate with ECR

First, authenticate your Docker daemon with ECR:

```
export AWS_ACCESS_KEY="<YOUR KEY>"
export AWS_ACCESS_TOKEN="<YOUR TOKEN>"
...
```

### 2. Pull the Image

Next, pull the latest release of our OEM image:

```
docker pull
```

### 3. Optional: Mirror the Image

Optionally, you may want to mirror our image to your own repoository. A common reason to do this is to prevent the need to distribute Vector Charts IAM credentials to your CI/CD systems or production deployments.

We recommend the use of the skopeo tool which facilitates easy replication of images across container registries.

## Run the Software

Once you have obtained the Docker image, you can run the software in a variety of ways. Our documentation covers the use of the software in Docker, Docker Compose, Kubernetes, and Nix 


## Run with Docker

TODO

## Run with Docker Compose

TODO

## Run with Kubernetes

TODO 

## Run with Nix

TODO