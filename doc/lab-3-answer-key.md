# Lab 3 - Deploying and operating

## Overview

In this lab, we will build a Docker image and deploy it to the microk8s cluster.

## Procedure

### Step 1 - Build Docker container image

1. Log into the microk8s VM with

`vagrant ssh workshop_microk8s`

2. Clone your fork of the Link app in the home directory:

`git clone https://github.com/base10/link.git`

3. Change into the Link directory with `cd link` and build the Docker image:

`sudo docker build -t link-container . -f deploy/Dockerfile`

4. Save the image to a tar file:

`sudo docker save link-container:latest > ~/link-container.tar`

5. Import the image in microk8s:

`microk8s ctr image import ~/link-container.tar`

### Step 2 - Apply k8s yaml files

Run this command to apply the yaml files:

`kubectl apply -f deploy/k8s`

### Step 3 - Review the app is running

1. Examine microk8s resources:

`kubectl get all --all-namespaces`

In the output from this command, you should see a pod, a deployment, a service,
and a replicaset for `link-app`.

2. Visit http://172.16.100.10:30000/ and http://172.16.100.10:30000/sidekiq

### Step 4 - Scale up and down

1. Run this command to scale the deployment up to 2 pods:

`kubectl scale --replicas=2 deployment.apps/link-app`

2. Run `kubectl get all --all-namespaces` to confirm that there are now two pods
for the `link-app` deployment.

3. Run this command to scale back down:

`kubectl scale --replicas=1 deployment.apps/link-app`

4. Run `kubectl get all --all-namespaces` again to confirm that the cluster
scaled back down to a single pod for `link-app`.
