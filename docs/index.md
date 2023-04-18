# Introduction

``Always be Scaling to Zero! ``

Now you may be sick of hearing this one too many times. Perhaps you want to see this in action and see what the fuss is all about? Perhaps you are person that wants to get your hands dirty?

Perhaps the following japanese sentence makes much sense to you?

``手を動かして見ないと。。``

Then read on..

Welcome to the EXPERIMENTAL Serverless labs. This is not intended for PRODUCTION purposes.

Most of the project works around Serverless capabilities that can be provided on Nutanix. (EXPERIMENTAL)

All the experiments are inspired by content in Nutanix [Opendocs](https://opendocs.nutanix.com) documents.

This repository/Gitpages is just a way for us to gather and document all that we have tested and worked with and share with like-minded people.

# Our Perceived Evolution of Serverless
## Cloud Provider Controlled

You would logon to a cloud provider console and input your function and cloud provider took care of running the funtion. The OS, the infrastructure required to run your code. 

At the end of the billing period you got a bill for the amount of CPU and memory you used for a period of time.

## Customer Controlled

Customers are increasingly required to do more with less. Emergence of Kubernetes is allowing customers to gain control over cloud spending by automating resource consumption only when they are required. There is no requirement to have infrastructure running if no workloads are running. Automating launching required resources on-demand, scaling up and scaling them down makes sense for customers.

This gives customer tight integration of infrastructure resources with their applications.
## Lab Flow

This lab will introduce you the afore mentioned customer controlled serverless scenario. 

All these steps are done on Nutanix hybrid cloud platform which can be installed on-premises and on a cloud provider of your choice (AWS and Azure for now).


The flow works in the following manner:

```mermaid
stateDiagram
    direction LR
    BuildVMImage --> CreateManagementCluster
    state BuildVMImage{
        direction LR
        Sucessful? --> UploadtoPC
    }
    CreateManagementCluster --> CreateWorkloadCluster
    state CreateManagementCluster {
      direction LR
      UseKind? --> WaitForUp
    }
    CreateWorkloadCluster --> TestScalingEvents
    state CreateWorkloadCluster {
      direction LR
      Success? --> GetKubeConfig
    }
    state TestScalingEvents {
      direction LR
      ScaleUp --> ScaleDown
    }
```

1. Using Hashicorp Packer tool you will create VM image for Kubernetes OS - this image will be uploaded to Prism Central 
2. You will create a Management Kubernetes Cluster on your Laptop (Kind suggested here) - please feel free to use your installation tool and platform
3. You will deploy a Workload Kubernetes Cluster from your Management Kubernetes Cluster
4. You will configure Autoscaler capability on Management Kubernetes Cluster
5. You will deploy a workload on the Workload Kubernetes cluster
6. You will test Scaling events on the workload in the Workload Kubernetes cluster

Happy Scaling to Zero!