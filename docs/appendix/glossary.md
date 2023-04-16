.. \_glossary:

  ----------
  Glossary
  ----------

Nutanix Core ++++++++++++

AOS ...

AOS stands for Acropolis Operating System, and it is the OS running on
the Controller VMs (CVMs).

Pulse .....

Pulse provides diagnostic system data to Nutanix customer support teams
so that they can deliver proactive, context-aware support for Nutanix
solutions.

Prism Element .............

Prism Element is the native management plane for Nutanix. Because its
design is based on consumer product interfaces, it is more intuitive and
easier to use than many enterprise application interfaces.

Prism Central .............

Prism Central is the multicloud control and management interface for
Nutanix. Prism Central can manage multiple Nutanix clusters and serves
as an aggregation point for monitoring and analytics.

Node ....

Industry standard x86 server with server-attached SSD and optional HDD
(All Flash & Hybrid Options).

Block .....

2U rack mount chassis that contains 1, 2 or 4 nodes with shared power
and fans, and no shared no backplane.

Storage Pool ............

A storage pool is a group of physical storage devices including PCIe
SSD, SSD, and HDD devices for the cluster.

Storage Container .................

A container is a subset of available storage used to implement storage
policies.

Anatomy of a Read I/O .....................

Performance and Availability

-   Data is read locally
-   Remote access only if data is not locally present

Anatomy of a Write I/O ......................

Performance and Availability

-   Data is written locally
-   Replicated on other nodes for high availability
-   Replicas are spread across cluster for high performance

Nutanix Karbon +++++++++++++++

Nutanix Karbon is an enterprise-grade Kubernetes Certified distribution
that simplifies the provisioning, operations and lifecycle management of
Kubernetes clusters with a native Kubernetes experience. Karbon makes it
simple to deploy and maintain highly available Kubernetes cluster and
operate web-scale workloads.
