## Purpose of Management Cluster

## Workstation Setup

We will need a Kubernetes cluster setup on our workstation. This could be any of the following:

- Kind
- Minikube
- k3d
  
During testing on a Intel Macbook pro with 8 CPU and 16 CPU, we found out that ``kind`` cluster performed the best.

Please feel free to choose what you are familiar with and have proven sucess with.

## Create Management Cluster

Follow steps here to [create](https://kind.sigs.k8s.io/) a ``kind`` mangement cluster 

## Initialise Management Cluster 

1. Create the following file in your workstation 
    
    ```bash
    vi ~/.cluster-api/clusterctl.yaml
    ```

2. Fill in the following contents

    ```bash
    NUTANIX_ENDPOINT: ""     # IP or FQDN of Prism Central
    NUTANIX_USER: "admin"             # Prism Central user
    NUTANIX_PASSWORD: ""    # Prism Central password
    NUTANIX_INSECURE: true
    EXP_CLUSTER_RESOURCE_SET: true    # Experimental for testing CCM and Autoscaling
    EXP_MACHINE_POOL: "true"          # Experimental
    CLUSTER_TOPOLOGY: "true"          # Experimental
    
    KUBERNETES_VERSION: "v1.24.7"
    WORKER_MACHINE_COUNT: 3
    NUTANIX_MACHINE_VCPU_SOCKET: 4
    NUTANIX_MACHINE_MEMORY_SIZE: "8Gi"
    NUTANIX_SSH_AUTHORIZED_KEY: ""
    
    NUTANIX_PRISM_ELEMENT_CLUSTER_NAME: ""
    NUTANIX_MACHINE_TEMPLATE_IMAGE_NAME: "ubuntu-2204-kube-v1.24.11"
    NUTANIX_SUBNET_NAME: "Primary"
    ```

3. Instantiate the Cluster API to communicate with Nutanix Cluster

    ```bash
    clusterctl init -i nutanix
    ```
4. Make sure all pods are in a Running and healthy state in the following namespaces:

    ```bash
    kubectl get pods -n capi-system
    kubectl get pods -n capx-system
    kubectl get pods -n cert-manager
    ```

    !!!warning
           If pods in the above name spaces are not running or have any errors, troubleshoot your CAPX deployment on management cluster. 
