---
title: "Cloud Certification - Essential Cloud Infrastructure"
date: 2020-03-18T16:31:12+01:00
description: "This is the second chapter of the way towards the Associate GCP Cloud Certification."
draft: false
categories: ["Certification"]
displayInMenu: false
displayInList: true
---

# GCP - Cloud Certification - Associate Cloud Engineer Cheat Sheer

### Compute Services:
- Compute Engine
- Kubernetes Engine
- App Engine
- Cloud Functions

### Ways to interact with GCP
- GCP Console (Web user interface)
- Cloud Shell and Cloud SDK (Command-line interface)
- REST-based API (Custom applications)
- Cloud Mobile App

### Cloud shell provides the following:
- Temporary Compute Engine VM
- Command-line access to the instance via a browser
- 5 GB of persistent disk storage ($HOME dir)
- Pre-installed Cloud SDK and other tools
- gcloud: for working with Google Compute Engine and many GCP services
- gsutil: for working with Cloud Storage
- kubectl: for working with Google Container Engine and Kubernetes
- bq: for working with BigQuery
- Language support for Java, Go, Python, Node.js, PHP, and Ruby
- Web preview functionality
- Built-in authorization for access to resources and instances
- To create a persistent state in Cloud Shell, you need to configure the .profile file.

### VPC
- VPC is a comprehensive set of Google managed networking objects.
- Objects:
  - Projects
  - Networks
    - Default, auto mode, custom mode
  - Subnetworks
  - Regions
  - Zones
  - IP Addresses
    - internal, external, range
  - VMs
  - Routes
  - Firewall rules

### Projects
- Associates objects and services with billing.
- Contains networks (up to 5) that can be shared/peered

### Network
- Has no IP address range.
- Is global and spans all available regions.
- Contains subnetworks.
- Is available as default, auto, or custom.

### 3 VPC Network types
1. Default
   - Every project
   - One subnet per region
   - Default firewall rules
2. Auto Mode
   - Default network
   - One subnet per region
   - Regional IP allocation
   - Fixed /20 subnetwork per region
   - Expandable up to /16
3. Custom Mode
   - No default subnets created
   - Full control of IP ranges
   - Regional IP allocation
   - Expandable to any RFC 1918 size

### Subnetworks cross zones
- VMs can be on the same subnet but in different zones.
- A single firewall rule can apply to both VMs.
- Every subnet has four reserved IP addresses in its primary IP range.

### IP Addresses
- Each virtual machine can have two IP addresses assigned (internal+external)
- External IPs are mapped to internal IPs
- DNS resolution for internal addresses:
  - Each instance has a hostname that can be resolved to an internal IP address
  - Name resolution is handled by internal DNS resolver
- DNS resolution for external addresses:
  - Instances with external IP addresses can allow connections from hosts outside the project.
  - DNS records for external addresses can be published using existing DNS servers (outside of GCP)
  - DNS zones can be hosted using Cloud DNS.

|Internal IP|External IP|
|---|---|
|Allocated from subnet range to VMs by DHCP|Assigned from pool (ephemeral) or Reserved (static)|
|DHCP lease is renewed every 24 hours|Billed when not attached to a running VM|
|VM name + IP is registered with network-scoped DNS|VM doesn't know external IP; it is mapped to the internal IP|

### Routes and firewall rules
- A route is a mapping of an IP range to a destination.
- Every network has:
  - Routes that let instances in a network send traffic directly to each other.
  - A default route that directs packets to destinations that are outside the network.
  - ***Firewall rules must also allow the packet.***
- Routes map traffic to destination networks.
- Firewall rules protect VM instances from unapproved connections
- Firewall rules are applied to the network as a whole.
- Firewall rules are stateful. (firewall rules allow bidirectional communication once a session is established)
- Default: Deny all ingress and allow all egress.
- A firewall rule is composed of the following parameters:
   - Direction: ingress/egress rules
   - Source or Destination: ingress/egress specific rules
   - Protocol and Port: Protocol/Port specific rules
   - Action: Allow/Deny packets that match the direction,protocol,port..
   - Priority: Governs the order in which rules are evaluated.
   - Rules Assignment: All rules are assigned to all instances. But certain rules can be assigned 

### Network Pricing
- Each GCP service has its own pricing model.

The following rates do not apply for Cloud CDN, CDN Interconnect, Carrier Peering, Direct peering and Cloud Interconnect traffic.

|Traffic type|Price|
|---|---|
|Ingress|No charge|
|Egress to the same zone (internal IP address)|No charge|
|Egress to Google products (YouTube, Maps..)|No charge|
|Egress to different GCP service (within same region, exceptions)|No charge|
|Egress between zones in the same region (per GB)|$0.01|
|Egress to the same zone (external IP address, per GB)|$0.01|
|Egress between regions within the US (per GB)|$0.01|
|Egress between regions, not including traffic between US regions|At internet egress rates|


### Common Network Designs
- Putting resources in different zones.
- Putting resources in different regions.
- Bastion host isolation:
  - Provide an external facing point of entry into a network containing private network instances.
- Access internal load balancer using HTTPS load balancer
- Access internal load balancer using Cloud VPN or Cloud Interconnect.
- Shared VPC network with an inline security appliance.

### GCP compute and processing options
|   |Compute Engine|Kubernetes Engine|App Engine Standard|App Engine Flexible|Cloud Functions|
|---|---|---|---|---|---|
|Language Support|Any|Any|Python, Node.js, Go, Java, PHP|Python, Node, Go, Java, PHP, Ruby, .NET..|Python, Node, Go|
Usage model|IaaS|IaaS,PaaS|PaaS|PaaS|Microservices Architecture|
Scaling|Server Autoscaling|Cluster|Autoscaling managed servers|Autoscaling managed servers|Serverless|
Primary use case|General Workloads|Container Workloads|Scalable web apps, Mobile Web Apps.|Scalable web apps, Mobile Web Apps.|Lightweight Event Actions|


### Compute Engine Features
1. Machine rightsizing:
   - Recommendation engine for optimum machine size
   - Stackdriver statistics
   - New recommendation 24hrs after VM create or resize
2. Global load balancing:
   - Multiple regions for availability
3. Available policies:
   - Live migrate
   - Auto restart

### Compute options:
- Several machine types
  - Network throughput scales at 2 Gbps per vCPU
  - Theoretical max throughput of 16 Gbps with 8 vCPU
- A vCPU is equal to 1 hardware hyper-thread

### Storage options:
- Disks
  - Standard, SSD, or Local SSD
  - Standard and SSD PDs scale in performance for each GB of space allocated
- Resize disks or migrate instances with no downtime
- Data that is stored on local SSDs persists only until one stops or deletes the instance

### Networking options:
- Robust networking features
  - Default, custom networks
  - Inbound/outbound firewall rules
    - IP based
    - Instance/group tags
  - Regional HTTPS load balancing
  - Network load balancing
    - Does not require pre-warming
  - Global and multi-regional subnetworks

### VM Access
- Linux:SSH
  - SSH from GCP console or CloudShell via Cloud SDK
  - SSH from computer or third-party client and generate key pair
  - Requires firewall rule to allow tcp:22

### Availability policy: Automatic changes
- Called "scheduling options" in SDK/API
- Automatic restart
  - Automatic VM restart due to crash or maintenance event
    - Not preemption or a user-initiated terminate
- On host maintenance
  - Determines wether host is live-migrated or terminated due to a maintenance event. Live migration is the default.
- Live migration
  - During maintenance event, VM is migrated to different hardware without interruption.
  - Metadata indicates occurrence of live migration.

### Terminated VM
- No charge for stopped VM
  - Charged for attached disks and IPs
- Actions (in the terminated state)
  - Change the machine type.
  - Add or removed attached disks; change auto-delete settings.
  - Modify instance tags.
  - Modify custom VM or project-wide metadata.
  - Remove or set a new static IP.
  - Modify VM availability policy.
  - Can't change the image of a stopped VM.


### Helpful bash commands
- See information about unused and used memory and swap space: free
- Details about the RAM installed: sudo dmidecode -t 17
- Number of processors: nproc
- CPUs installed: lscpu

### Compute Options
- Machine types
  - Standard High-memory
  - High-CPU
  - Memory-optimized
  - Compute-optimized
  - Shared-core
  - Custom machine type

### Compute Pricing
- Per-second billing, with minimum of 1 minute
  - vCPUs, GPUs, and GB of memory
- Resource-based pricing
  - Each vCPU and each GB of memory is billed separately
- Discounts:
  - Sustained use (up to 30% discount for instances that run the entire month)
  - Committed use
  - Preemptible VM instances (their availability varies with usage)
- Recommendation Engine
  - Notifies you of underutilized instances
- Free usage limits


### Special Compute Configurations (Options)
- Preemptible
  - Lower price for interruptible service (up to 80%)
  - VM might be terminated at any time
    - No charge if terminated in the first 10 minutes
    - They live for up to 24 hours max
    - 30-second warning before termination is executed
  - No live migrate; no auto restart in preembtible VMs
  - CPU quota for a region is splitable between regular and preemption
    - Default: preemptible VMs count against region CPU quota

- Sole-tenant nodes
  - For workloads that require physical isolation from other workloads.
  - A sole-tenant node is a physical Compute Engine server that is dedicated to hosting VM instances only for a specific project

- Shielded VMs
  - Offer verifiable integrity
  - Integrity is verified through the use of secure boot
  - Requires shielded images


### Images
- What's in an image?
  - Boot loader
  - Operating system
  - File system structure
  - Software
  - Customizations
- Public base images
  - Linux/Windows images available
- Custom Images
  - Create and use a custom image by pre installing software that's been authorized for a specific organization

### Disk Options:
- VM comes with a single root persistent disk.
- Image is loaded onto disk during first boot:
  - Bootable: you can attach to a VM and boot from it.
  - Durable: can survive VM terminate.
- Some OS images are customized for Compute Engine.
- Can survive VM deletion if "Delete boot disk when instance is deleted" is disabled
- HDD or SSD
- Can be attached in read-only mode to multiple VMs
- Disk resizing: Even running and attached
- Local SSD disks are physicall attached to a VM
- RAM disk (use TMPFS if you want to store data in memory, best for small data structures)

### Summary disk options:
|   |Persistent disk HDD|Persistent disk SSD|Local SSD disk|RAM disk|
|---|---|---|---|---|
|Data redundancy|Yes|Yes|No|No|
|Encryption at rest|Yes|Yes|Yes|N/A|
|Snapshotting|Yes|Yes|No|No|
|Bootable|Yes|Yes|No|No|
|Use case| General, bulk file storage|Very random IOPS|High IOPS and low latency|low latency and risk of data loss|

### Maximum persistent
|Machine Type|Disk number limit|
|---|---|
|Shared-core|16|
|Standard|128|
|High-memory|128|
|High-CPU|128|
|Memory-optimized|128|
|Compute-optimized|128|

### Persistent disk management differences
|Cloud Persistent Disk|Computer Hardware Disk|
|---|---|
|Single file system is best|Partitioning|
|Resize grow disks|Repartitioning disk|
|Resize file system|Reformat|
|Built-in snapshot service|Redundant disk arrays|
|Automatic encryption|Subvolume management and snapshots|
|-|Encrypt files before write to disk|

### Common Compute Engine Actions
- Move an instance to a new zone
- Persistent disk snapshots (backups..)13
  - Snapshot is not available for local SSD
  - Creates an incremental backup of Cloud Storage
  - Snapshots can be restored to a new persistent disk
- Resize persistent disk
  - Disks can grow but never shrinked.

### Question notes:
- In GCP, what is the minimum number of IP addresses that a VM instance needs?
  - One: Only an internal IP address
- What are the three types of networks offered in the Google Cloud Platform?
  - Default network, auto network, and custom network.
- What is one benefit of applying firewall rules by tag rather than by address?
  - When a VM is created with a matching tag, the firewall rules apply irrespective of the IP address it is assigned.