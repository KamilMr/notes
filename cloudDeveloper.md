# VPC

1. Google Compute Engine focuses on virtual networking.
2. Virtual Private Cloud (VPC) is a secure, individual cloud within a public cloud like Google Cloud.
3. VPC allows you to run code, store data, and host websites, combining the benefits of public and private clouds.
4. VPC networks handle resource connectivity and internet access, including firewall rules and static routes.
5. Google VPC networks are global and can have subnets in any Google Cloud region.
6. Subnets can span multiple zones within a region.
7. The size of a subnet can be expanded without affecting existing virtual machines.
8. Resources in different zones can be on the same subnet.

# IaaS

1. **IaaS Solution**: Compute Engine is Google Cloud's Infrastructure as a Service (IaaS) offering.
2. **Virtual Machines**: Users can create and run VMs with full-fledged operating systems on Google infrastructure.
3. **Flexible Configuration**: VMs can be customized for CPU power, memory, storage, and OS.
4. **Management Tools**: You can manage VM instances through Google Cloud console, CLI, or API.
5. **OS Support**: Supports both Linux and Windows Server images and allows customizations.
6. **Cloud Marketplace**: Quick way to launch pre-configured VMs and other resources.
7. **Billing Structure**: Billed by the second, with sustained and committed-use discounts available.
8. **Preemptible and Spot VMs**: Cost-saving options for temporary or interruptible workloads.
9. **Storage**: High-throughput storage available by default at no extra cost.
10. **Custom Machine Types**: Pay only for what you need by customizing machine properties.

## Containers

1. **Containers in IaaS and PaaS**: Containers provide scalability like Platform as a Service (PaaS) and an abstraction layer of the Operating System (OS) and hardware similar to Infrastructure as a Service (IaaS), making them a flexible and efficient option for developers.
2. **Virtual Machines vs. Containers**: While Virtual Machines (VMs) involve deploying a full OS and can be large and slow to boot, containers encapsulate an application and its dependencies in a lightweight, isolated environment, requiring less overhead and offering quicker startup times.
3. **Scalability and Portability**: Containers allow for rapid scaling of applications and ultra portability across different environments, from development to production or from a local machine to the cloud, without the need for changes or rebuilds.
4. **Efficiency and Modularity**: Containers start quickly, like a process, and use a fraction of the resources compared to VMs. They can be deployed in large numbers on a single host, enhancing the efficiency of resource usage.
5. **Application Architecture with Containers**: They support a microservices architecture, where applications are built using multiple containers, each performing a specific function. This modular approach facilitates easy deployment and independent scaling across a cluster of hosts.

## Kubernetes

- Kubernetes is a tool for managing and scaling containerized applications.
- It can be used efficiently with Google Kubernetes Engine (GKE) to save time and effort.
- Kubernetes operates through a set of APIs, managing containers on nodes within clusters.
- Pods are the smallest units in Kubernetes, representing running processes with unique network IPs and ports.
- Scaling and updates in Kubernetes can be done declaratively using configuration files, ensuring a desired state and controlled updates.

## Google Kubernetes Engine

1. GKE stands for Google Kubernetes Engine.
2. It is a managed Kubernetes service hosted by Google in the cloud.
3. GKE clusters are composed of Compute Engine instances grouped together.
4. You can create GKE clusters using the Google Cloud Console or the gcloud command.
5. GKE clusters can be customized, including machine types, node counts, and network settings.
6. Kubernetes is the primary tool for interacting with GKE clusters.
7. Kubernetes commands and resources are used to deploy, manage, and monitor applications in GKE.
8. GKE offers advanced cluster management features, such as load balancing, node pools, automatic scaling, and upgrades.
9. Node auto-repair helps maintain node health and availability in GKE clusters.
10. GKE provides logging and monitoring through Google Cloud's operations suite.
