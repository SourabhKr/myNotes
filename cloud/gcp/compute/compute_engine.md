# Compute Engine

- Virtual  Machine 

    Data is encrypted automatically. A service account associated with a VM.

  - Compute

    - Machine Family

      - General purpose

        - Machine types

          - [ ] Shared Cores

          - [ ] Standard

          - [ ] High Memory

          - [ ] High CPU

      - Compute Optimized

        - Machine Types

          - [ ] Standard machine

      - Memory optimized

        - Machine Types

          - [ ] Mega Memory

          - [ ] Ultra Memory

      - GPU

        - Machine types

          - [ ] Type of GPU

          - [ ] # Number of GPU

  - Storage

    - Boot Disk

      - Boot Image

        - [ ] Predefined Boot Image

        - [ ] Custom based on Predifined

      - [ ] Containers

        While deploying a container, the restart policy (Always, Never, On failure) can be specified and if the container should run as privileged.  
        Containers are not allowed to access system devices, such as disks or network interfaces. When a container is run as privileged, the container has equivalent permissions to run as root on the host.

    - Additional Storage

      - [Persistent Disk volumes](https://cloud.google.com/compute/docs/disks#pdspecs)

        Persistent Disk volumes provide high-performance and redundant network storage. Each Persistent Disk volume is striped across hundreds of physical disks.

        - [ ] Standard persistent disks

            Suitable for large data processing workloads that primarily use sequential I/Os.  
            Backed by standard hard disk drives (HDD).

        - [ ] Balanced persistent disks

            Balance of performance and cost. For most VM shapes, except very large ones, these disks have the same maximum IOPS as SSD persistent disks and lower IOPS per GB. This disk type offers performance levels suitable for most general-purpose applications at a price point between that of standard and performance (pd-ssd) persistent disks.  

            Backed by solid-state drives (SSD).

        - [ ] Performance (SSD) persistent disks

            Suitable for enterprise applications and high-performance databases that require lower latency and more IOPS than standard persistent disks provide.  
            Designed for single-digit millisecond latencies; the observed latency is application specific.  
            Backed by solid-state drives (SSD).

        - [ ] Extreme persistent disks

            Offer consistently high performance for both random access workloads and bulk throughput.  
            Designed for high-end database workloads.  
            Allow you to provision the target IOPS.  
            Backed by solid-state drives (SSD).  
            Available with a limited number of machine types.

      - Google Cloud Hyperdisk

        Google Cloud Hyperdisk is Google's next generation block storage. By offloading and dynamically scaling out storage processing, it decouples storage performance from the VM type and size. Hyperdisk offers substantially higher performance, flexibility and efficiency.

        - [ ] Hyperdisk Extreme

        - [ ] Hyperdisk Throughput

      - Local SSD

        Local SSDs are physically attached to the server that hosts your VM instance. Local SSDs have higher throughput and lower latency than standard Persistent Disk or SSD Persistent Disk. The data that you store on a local SSD persists only until the VM is stopped or deleted.

        Only available on First Generation Machine Configuration.

      - Cloud Storage buckets

      - Filestore

    - [ ] Main Memory

- Sole-Tenant VMs

 Sole-tenancy lets you have exclusive access to a sole-tenant node, which is a physical Compute Engine server that is dedicated to hosting only your project's VMs. Use sole-tenant nodes to keep your VMs physically separated from VMs in other projects, or to group your VMs together on the same host hardware

  - Node group

    - Node Templates

   A node template is a regional resource that defines the properties of each node in a node group. When you create a node group from a node template, the properties of the node template are immutably copied to each node in the node group.

      - [ ] Node Type

    When configuring a node template, specify a node type to apply to all nodes within a node group created based on the node template. The sole-tenant node type, referenced by the node template, specifies the total amount of vCPU cores and memory for nodes created in node groups that use that template.

- [ ] Preemptible VM & Spot VMs

- Shielded VMs

 Shielded VMs are instances with enhanced security controls.

  - [ ] Secure boot

  Secure boot runs only software that is verified by digital signatures of all boot components using UEFI firmware feature.

  - [ ] vTPM

  Virtual Trusted Platform Module is a virtual module for storing keys and other secrets.

  - [ ] Integrity Monitoring

  Integrity monitoring compares the boot measurements with  a trusted baseline and returns true if the results match and false otherwise.

- [ ] Confidential VMs

 Confidential VMs encrypt data in use.  
 
 This can be created by enabling the feature when creating a VM.

- Instance Groups

 Instance groups are clusters of VMs that are managed as a single unit.

  - [ ] Managed Instance groups

  MIGs contain identically configured instance.  
  
  The configuration is specified in an instance template.

  - [ ] Unmanned Instance groups

  UMIGs are groups of VMs that may not be identical.  
  
  Not provisioned through instance templates.

![Compute-Engine](/asset/images/gcp/compute-engine.png)