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
- [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html) to authenticate Docker with AWS ECR

## Pulling the Docker Image 

We distribute Vector Charts OEM as a private Docker image on AWS ECR.

During your onboarding to Vector Charts OEM with the Zydro team, you will receive a set of user-specific, read-only IAM credentials which grant access to pull software from the OEM container registry.

### 1. Authenticate with ECR

First, authenticate your Docker daemon with ECR:

<pre>
# Add AWS environment credentials for AWS CLI to read
export AWS_ACCESS_KEY="...your IAM key...."
export AWS_ACCESS_TOKEN="...your IAM secret..."
export AWS_REGION=us-east-2

# Generate a temporary ECR token and pipe into Docker
aws_pass=$(aws ecr get-login-password --region us-east-2)
echo $aws_pass | docker login --username AWS --password-stdin 402590802363.dkr.ecr.us-east-2.amazonaws.com &>/dev/null
</pre>

AWS ECR tokens are short-lived, so you will need to reauthenticate frequently in order to pull new images.

We recommend internally mirroring the Vector Charts OEM image to an ECR or other repository which you control.

### 2. Pull the Image

We distribute versions of Vector Charts OEM as version and architecture-tagged images.

`402590802363.dkr.ecr.us-east-2.amazonaws.com/vector-charts-oem:<version>-<sha>-<architecture>`

For example, at the point of writing this documentation the current version is

`402590802363.dkr.ecr.us-east-2.amazonaws.com/vector-charts-oem:0.4.1-ba68d44-x86_64`.

Versions are publicized by the Vector Charts team with OEM customers, in tandem with our release notes. Please see [Changelog](/oem/changelog/) for all recent release notes and tagged release versions. 

To pull a release of our OEM image:

<pre>
docker pull 402590802363.dkr.ecr.us-east-2.amazonaws.com/vector-charts-oem:0.4.1-ba68d44-x86_64
</pre>

This image is now available to use locally.

### 3. Optional: Mirror the Image

Optionally, you may want to mirror our image to your own repoository. A common reason to do this is to prevent the need to distribute Vector Charts IAM credentials to your CI/CD systems or production deployments as mentioned above.

We recommend the use of the [skopeo](https://github.com/containers/skopeo) tool, which facilitates easy replication of images across container registries.

## Run the Software

Once you have obtained the Docker image, you can run the software in a variety of ways.

Please see [Configuration](/oem/configuration/) for a detailed list of configuration parameters.

## Run with Docker

To start up a test instance with Docker, run:

<pre>
docker run -d \
    --name vector-charts-oem \
    -p 9909:9909 \
    -e INITIAL_ADMIN_USERNAME=${INITIAL_ADMIN_USERNAME:-admin} \
    -e INITIAL_ADMIN_PASSWORD=${INITIAL_ADMIN_PASSWORD:-admin} \
    -e LICENSING_ORGANIZATION_ID=...your organization... \
    402590802363.dkr.ecr.us-east-2.amazonaws.com/vector-charts-oem:0.4.1-ba68d44-x86_64
</pre>

Once running, navigate to [http://localhost:9099](http://localhost:9099) which will show the Admin dashboard. This is the same port that the API runs on.

## Run with Docker Compose

<pre>
services:
    vector-charts-oem:
        image: 402590802363.dkr.ecr.us-east-2.amazonaws.com/vector-charts-oem:0.4.1-ba68d44-x86_64
        restart: always
        environment:
            LICENSING_ORGANIZATION_ID: "...your organization..."
            LICENSING_SERVER_NAME: "...you organization..."
        ports:
            - 9909:9909
        volumes:
            - vector-charts-oem-data:/home/vector-charts/data
volumes:
    vector-charts-oem-data:
</pre>