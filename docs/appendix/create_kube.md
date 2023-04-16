---
title:  Creating a Kubernetes Cluster
---

##Overview 

Before we can deploy an application using kubernetes we need to create a
Kubernetes cluster first. The cluster that we are ging to create
consists out of the following VMs:

-   1 Master node (VM)
-   1 Worker node (VM)
-   1 etcd nodes (VM)

!!!info
        For more information on the terms master, worker and etcd, please look at https://kubernetes.io/docs/concepts/.

## Creating a Karbon Cluster

1. In your Prism Central, select the three dash in the top left corner and select **Services** > **Karbon**
   
    ![](images/0.png)
   
2. A new browser window will open and accept the HTTPS error you will see.

    ![](images/1.png)

3. In the shown browser screen click on the **+ Create Cluster** button for starting to create the kubernetes cluster

    ![](images/2.png)

4. Provide the required parameters that are asked for in the wizard. The following screenshots can be used as a guideline

    !!!tip
          You can also hover over the **?** sign to get more information about each configuration option.

3. Choose Development Cluster

    ![](images/2-1.png)

3. Enter a name for your cluster **initials-cluster** and choose your HPOC
as **Nutanix Cluster**

    ![](images/3.png)

4. Provide the Worker, Master and etcd settings as default; click **Next**

    ![](images/4.png)

5. Provide the Network Provider settings as default; click **Next**

    !!!info
            We use flannel as the network provider. More information on Flannel can be found [here](https://github.com/coreos/flannel#flannel)

    ![](images/6.png)

6. Provide the Storage class settings. For the cluster settings use
**admin** and the **cluster password** that you used to login to the
cluster.

    ![](images/7.png)

7. Click on the **Create** button to have the cluster created by the
system. Follow the process in the Karbon UI.

    !!!note
            Based on the resources available on your cluster, it will take
            time. **Wait until the cluster has been created before proceeding to the
            next part of the module!!**

    ![](images/20.png)

During the creation of the Kubernetes cluster there will have been created:

-   VMs

     ![](images/10.png)

-   Persistent Storage as VolumeGroup

     ![](images/18.png)

     ![](images/9.png)

## Cluster properties

In the Karbon UI, hover over the just created cluster (**initials-cluster** in our example) and click on it.

![](images/21.png)

This will open another screen which shows the parts out of which the
cluster is created according to the provided parameters that have been
provided during the creation phase.

![](images/22.png)

The below screenshots provide an example for the three parts, Storage
Class, Volume and Add-on.

![](images/23.png)

![](images/24.png)

![](images/25.png)

This concludes the end of this part of the module. You now have a running Kubernetes Cluster.

## Takeaways

-   It is quite easy to create a kubernetes cluster using Nutanix Karbon
-   Both Development and Production cluster with different node count
    options are available
-   Flannel is the only CNI option available in the Karbon GUI. However,
    Calico is avaialble to configure through REST API calls
