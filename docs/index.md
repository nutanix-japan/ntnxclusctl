# Landing Page


This is your home

The meaning of Serverless is evolving. 

## Lab Flow

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