---
title: "Cloud Certification - Core Services"
date: 2020-03-26T16:31:12+01:00
description: "This is the third chapter of the way towards the Associate GCP Cloud Certification."
draft: false
categories: ["Certification"]
displayInMenu: false
displayInList: true
---

# GCP - Cloud Certification - Associate Cloud Engineer

### GCP compute services
- Compute Engine
- Google Kubernetes Engine
- App Engine
- Cloud Functions

- IAM - Identity Access Management
   - Who - Can do what - On which resource
   - IAM-Objects(hierarchy): Organizaion, Folders, Projects, Resources, Roles, Members
   - IAM - member types (WHO)
      - Google Accounts (Belongs to an individual user)
      - Service Accounts (Belongs to an application)
      - Service Accounts (Collection of Google Accounts + Service Accounts)
      - Google Groups (Convenient way to apply an access policy to a collection of users)
      - Google Suite Domains (Represents a virtual group of all the Google Accounts that have been created in an organization's G Suite account - those accounts have no access to G Suite applications)
      - Cloud Identity domain
    - IAM - role types (CAN DO WHAT)
      - Primitive roles (owner, editor, and viewer roles, Billing Administrator(Super-Admin))
      - Predefined roles (Granular access rights to ressources. Role examples: Network Viewer, Network Admin or Security Admin)
      - Custom roles (Create custom roles with a list of permissions)

### Storage options on Google Cloud Platform
|              | Cloud Datastore | Bigtable      | Cloud Storage | Cloud SQL     | Cloud Spanner | Big Query |
| ------------ | -------------   | ------------- | ------------- | ------------- | ------------- | ------------- |
Type | NoSQL document | NoSQL wide column | Blobstore | Relational SQL for OLTP | Relational SQL for OLTP | Relational SQL for OLTP | 
Transactions | Yes | Single-row | No | Yes | Yes | No |
Complex queries | No | No | No | Yes | Yes | Yes|
Capacity | Terabytes+ | Petabytes+ | Petabytes+ | Terabytes | Petabytes | Petabytes + |
Unit size | 1 MB/entity | ~10 MB/cell </br> ~100MB/row | 5TB/object | Determined by DB engine | 10,240 MiB/row | 10 MB/row
Use-Case | Semi-structured application data that is used in app engines' applications | Analytical data with heavy read/write events like AdTech, Financial or IoT data | Saving images/movies) | SQL is best for web frameworks and in existing applications like storing user credentials and customer orders | Large scale database applications that are larger than two terabytes; for example, for financial trading and e-commerce | BigData analysis, interactive queries

### Cloud Storage Classes
|   |Multi-regional|Regional|Nearline|Coldline|
|---|---|---|---|---|
|Intended for data that is...|Most frequently accessed|Accessed frequently within a region|Accessed less than once a month|Accessed less than once a year|
|Availability SLA|99,95%|99,90%|99,00%|99,00%|
|Access APIs|Consistent APIs|
|Access time|Millisecond access|
|Storage price|high|||low|
|Retrival price|low|||high|
|Use cases|Content storage and delivery|In-region analytics, tanscoding|Long-tail content, backups|Archiving, disaster recovery|

### Cloud Storage Features
- Customer-supplied encryption key (CSEK)
- Object Lifecyle Management
  - Automatically delete or archive objects
- Object Versioning
  - Maintain multiple versions of objects
- Directory synchronization
  - Synchronizes a VM directory with a bucket
- Object change notification
- Data import
- Strong consistency

### Data import services
- Transfer Appliance: Rack, capture and then ship your data to GCP.
- Storage Transfer Service: Import online data (another bucket, an S3 bucket, or web source).
- Offline Media import: Third-party provider uploads the data from physical media.

### Cloud SQL (managed service instead installing SQL on a VM running on compute engine)
- Patches and updates automatically applied
- You administer MySQL users
- Cloud SQL supports many clients
  - gcloud sql
  - App Engine, G Suite scripts
  - Applications and tools
    - SQL Workbench, Toad
    - External applications using standard MySQL drivers
- Choice: MySQL/PostgreSQL
- Cloud SQL services:
  - Replica services
  - Backup service
  - Import/export
  - Scaling

### Cloud Spanner
- Combines the benefits of relational database structure with non-relational horizontal scale
- Scale to petabytes
- Strong consistency
- High availability
- Used for financial and inventory applications
- Monthly uptime
  - Multi-regional: 99,999%
  - Regional: 99,99%

### Cloud Spanner Characteristics
|   |Cloud Spanner|Relational DB|Non-Relational DB|
|---|---|---|---|
|Schema|Yes|Yes|No|
|SQL|Yes|Yes|No|
|Consistency|Strong|Strong|Eventual|
|Availability|High|Failover|High|
|Scalability|Horizontal|Vertical|Horizontal|
|Replication|Automatic|Configurable|Configurable|

### Cloud Firestore
- NoSQL document database
- Simplifies storing, syncing, and querying data
- Mobile, web, and IoT apps at global scale
- Live synchronization and offline support
- Security features
- ACID transactions (If any of the operations in the transaction fail and cannot be retried, the whole transaction will fail)
- Multi-regional application
- Powerful query engine
- Next generation of Cloud Datastore
- 2 modes:
  - Datastore mode: new server projects
  - Native mode: new mobile and web apps

### Cloud Bigtable
- If you don't need transactional consistency
- Petabyte-scale
- Consistent sub-10ms latency
- Seamless scalability for throughput
- Learns and adjusts to access patterns
- Ideal for Ad Tech, Fintech, and IoT
- Storage engine for ML apllications
- Easy integration with open source big data tools
- Smallest cluster has three nodes and handles 30,000 operations per second.
- You pay for the nodes wether they are used or not.

### Cloud Memorystore
- Fully managed Redis service
- In-Memory data store service
- Focus on building great apps
- High availability, failover, patching, and monitoring
- Sub-millisecond latency
- Instances up to 300 GB
- Network throughput of 12 Gbps
- Easy Lift-and-Shift

### Question Notes:
- Which data storage service provides data warehouse services for storing data but also offers an interactive SQL interface for querying the data?
  - BigQuery
- Which GCP data storage service offers ACID transactions and can scale globally?
  - Cloud Spanner
- What data storage service might you select if you just needed to migrate a standard relational database running on a single machine in a datacenter to the cloud?
  - Cloud SQL

### Cloud Resource Manager
- Lets you hierarchically manage resources
- A project accumulates the consumption of all its resources:
  - Track resource and quota usage
    - Enable billing
    - Manage permissions and credentials
    - Enable services and APIs
  - Projects use three identifying attributes:
    - Project Name
    - Project Number
    - Project ID (Application ID)
- Resources are global, regional or zonal
- Billing and reporting is per project

### Quotas
- All resources are subject to project quotas or limits
- Examples:
  - 5 VPC networks per project
  - 5 admin actions per second (Cloud Spanner)
  - 24 CPUs per region
- Why project quotas?
  - Prevent runaway consumption in case of an error or malicious attack
  - Prevent billing spikes or surprises
  - Forces sizing consideration and periodic review

### Labels and names
- Labels are a utility for organizing GCP resources
- Key-Value-Pairs you can attach to resources: VM, disk, snapshot, image
- Usages:
  - Distinguish between teams: marketing - research
  - Components: redis - frontend
  - Environment: prod - test
  - State: ready to delete - in use
- Difference to tags:
  - Tags are applied to instances only
  - Primarily used for networking

### Billing
- Budget and email alerts
- Programmatic Budgets: Cloud Pub/Sub -> Cloud Functions
- Visualizable with Data Studio (Billing Dashboard)

### Question Notes
- How do quotas protect GCP customers?
  - By preventing uncontrolled consumption of resources.

### Stackdriver overview
- Integrated monitoring, logging, diagnostics
- Manages across platforms
  - GCP and AWS
  - Dynamic discovery of GCP with smart defaults
  - Open-source agents and integrations
- Access to powerful data and analytics tools
- Collaboration with third-part software
- Integrated products:
  - Monitoring
  - Logging
  - Error Reporting
  - Trace
  - Debugger

### Stackdriver Monitoring
- Dynamic config
- Platform, system, and application metrics
  - Ingests dat: Metrics, events, metadata
  - Generates insights through dashboards, charts, alerts
- Uptime/health checks
- Dashboards
- Alerts

### Logging
- Platform, systems, and application logs
  - API to write to logs
  - 30-day retention
- Log search/view/filter
- Log-based metrics
- Monitoring alerts can be set on log events
- Data can be exported to Cloud Storage, BigQuery, and Cloud Pub/Sub

### Stackdriver Error Reporting
- Aggregate and display errors for running cloud services
- Error notifications
- Error dashboard

### Stackdriver Tracing
- Displays data in near real-time
- Latency reporting
- Per-URL latency sampling

### Stackdriver Debugging
- Inspect an apllication without stopping it or slowing it down significantly
- Debug snapshots:
  - Capture call stack and local variables of a running application
- Debug logpoints
  - Inject logging into a service without stopping it.

### Question Notes
- What is the foundational process at the base of Google's Site Reliability Engineering (SRE) ?
  - Monitoring
- What is the purpose of the Stackdriver Trace service?
  - Reporting on latency as part of managing performance.
- Stackdriver integrates several technologies, including monitoring, logging, error reporting, and debugging that are commonly implemented in other environments as separate solutions using separate products. What are key benefits of integration of these services?
  - Reduces overhead, reduces noise, streamlines use, and fixes problems faster