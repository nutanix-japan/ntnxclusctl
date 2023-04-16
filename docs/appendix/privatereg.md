---
title: Using Public Container Registry Credentials
---

# Using Public Container Registry

In this section we will go through a few steps to use your own registry and associated credentials.

Since most public container registries shape/rate-limit download, it may be essential to you use a private registry or use your login credentials to download container images from a public registry (Docker, etc).

In kubernets, we can configure the service accounts to use your public registry credentials to download container images. The steps include the following:

1. Create a generic kubernetes secret in your namespace with public registry credentials - this will become your pull secret
2. Associate a kubernetes service account to use your pull secret

## Create a Container Pull Secret

1. Login to your Linux Tools VM
2. Authenticate to your kubernetes cluster using the kubeconfig file your downloaded from Karbon
3. Change to the namespace you would like to use
   ```bash
   kubectl config set-context --current --namespace=<your-namespace>
   ```
   ```bash title="Example command"
   kubectl config set-context --current --namespace=default
   ```
3. Create a pull secret using your Docker account
   ```bash
   kubectl create secret generic regcred \
   --docker-username=DUMMY_USERNAME --docker-password=DUMMY_DOCKER_PASSWORD \
   --docker-email=DUMMY_DOCKER_EMAIL
   ```

## Associate Pull Secret with Service Account

4. Associate pull secret with the service account your will be using
   ```bash
   kubectl patch serviceaccount default -p '{"imagePullSecrets": [{"name": "regcred"}]}'
   ```
5. Verify if the serviceaccount is using your ``regcred`` docker registy secret
   
    ```bash
    kubectl get sa default -o yaml
    ```

    ```yaml hl_lines="8" title="Command output"
    apiVersion: v1
    kind: ServiceAccount
    metadata:
      name: default
      namespace: default
      uid: 052fb0f4-3d50-11e5-b066-42010af0d7b6
    imagePullSecrets:
    - name: regcred
    ``` 
6. Now your yaml manifest can use this secret to download container images

    ```bash title="Create a pod"
    k run nginx --image=nginx --restart=Never
    ```
    ```bash
    k get po nginx -oyaml
    ```
    ```yaml hl_lines="14 15" title="Command output if the pod was created by default service account"
    apiVersion: v1
    kind: Pod
    metadata:
        creationTimestamp: null
        labels:
            run: nginx
        name: nginx
    spec:
    containers:
    - image: nginx
      name: nginx
    dnsPolicy: ClusterFirst
    restartPolicy: Never
    imagePullSecrets:
    - name: regcred
    ``` 
    ```bash title="Delete the pod"
    k delete po nginx
    ```

You can now use your docker credentials to download container images from Docker public registry.
