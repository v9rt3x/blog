---
title: "Cloud Certification - Core Infrastructure"
date: 2020-03-01T16:31:12+01:00
description: "This is a series of the way of reaching the Associate GCP Cloud Certification. For each chapter you'll find kinda reference document like this. The certification includes 4 chapter. This document comprehends the first one."
draft: false
categories: ["Certification"]
displayInMenu: false
displayInList: true
---

# GCP Cloud Certification - Associate Cloud Engineer

### Personal general remarks to the coursera certification program:
- Qwiklabs hands-on lab lets you do lab activities yourself in a real cloud environment, not in a simulation or demo environment. This is really well organized and makes lots of fun to accomplish the tasks.
- After each chapter there are questions about the latest topic. Those questions are sometimes really specific. I would say too specific. In most cases I would have to look-up anyway if I would face such specific problems.
- One of the general benefits, google remarks in each chapter, is that customers only pay per use.
- The course gives you a comprehensive overview of the gcp-products.
- At the end of each chapter there are summerizing tables which are helpful.
- General procedure in labs:
  - Create Network
  - Create Subnets in Network
  - Create VM Instance(s) and assign to Network

### Load Balancing Options
|Global HTTP(s)|Global SSL Proxy|Gloal TCP Proxy|Regional|Regional internal|
|---|---|---|---|---|
|Layer 7 load balancing based on load|Layer 4 load balancing of non-HTTPS SSL traffic based on load|Layer 4 load balancing of non-SSL TCP traffic|Load balancing of any traffic(TCP,UDP)|Load balancing of traffic inside a VPC|
|Can route different URLs to different back ends|Supported on specific port numbers|Supported on specific port numbers|Supported on any port number|Use for the internal tiers of multi-tier applications|

### Interconnect Options
|VPN|Direct Peering|Carrier Peering| Dedicated Interconnect|
|---|---|---|---|
|Connection over VPN tunnels|Private connection for hybrid cloud workloads|Connection through partner network of service providers| Transport circuits for private cloud traffic|


### Storage options on Google Cloud Platform

|              | Cloud Datastore | Bigtable      | Cloud Storage | Cloud SQL     | Cloud Spanner | Big Query |
| ------------ | -------------   | ------------- | ------------- | ------------- | ------------- | ------------- |
Type | NoSQL document | NoSQL wide column | Blobstore | Relational SQL for OLTP | Relational SQL for OLTP | Relational SQL for OLTP | 
Transactions | Yes | Single-row | No | Yes | Yes | No |
Complex queries | No | No | No | Yes | Yes | Yes|
Capacity | Terabytes+ | Petabytes+ | Petabytes+ | Terabytes | Petabytes | Petabytes + |
Unit size | 1 MB/entity | ~10 MB/cell </br> ~100MB/row | 5TB/object | Determined by DB engine | 10,240 MiB/row | 10 MB/row|


- Use Cases:
    1. Cloud Datastore:
       - Semi-structured application data that is used in app engines' applications.
    2. Bigtable:
       - Analytical data with heavy read/write events like AdTech, Financial or IoT data.
    3. Cloud Storage:
       - Saving images/movies
    4. Cloud SQL:
       - SQL is best for web frameworks and in existing applications like storing user credentials and customer orders
    5. Cloud Spanner:
       - Large scale database applications that are larger than two terabytes; for example, for financial trading and e-commerce
    6. Big Query:
       - BigData analysis, interactive queries


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



### Confused by all the engines in GCP?
1. **Compute Engine**:
    - GCPs Infrastructure as a Service offering, which lets you run Virtual Machine in the cloud and gives you persistent storage and networking for them.
2. **App Engine**:
   - One of GCP's platform as a service offerings.
   - Instead of getting a blank Virtual Machine, you get access to a family of services that applications need.
   - The platform scales your applications seamlessly and independently by workload and infrastructure.
   - Negative: You give up control of the underlying server architecture.
   - App Engine platform manages the hardware and networking infrastructure required to run your code.
   - Provides built-in services like: NoSQL databases, in-memory caching, load balancing, health checks, logging and a way to authenticate users.
   - It scales your application automatically in response to the amount of traffic it receives.
   - Pay for those resources you use.
   - Suitable for applications where the workload is highly variable or unpredictable like web applications and mobile backend.
\

Two environments:
   1. App Engine Standard
      - Simpler deployment experience
      - Offers a free daily usage quota for the use of some services.
      - Low utilization applications might be able to run at no charge.
      - Your application can't write to the local file system. It'll have to write to a database service instead.
      - All the requests your application receives has a 60-second timeout, and you can't install arbitrary third party software.
      - Use App Engine SDK to deploy to App Engine.
      - App Engine can access a variety of services using dedicated API's(e.g. Memcache, Task queues, Scheduled tasks, Logs..)
      - For people who want the service to take maximum control of their application's deployment and scaling.
      - Scaling is finer-grained.
      - Google provides and maintains runtime binaries.
   2. App Engine Flexible
      - App Engine flexible environment lets you specify the container your App Engine runs in.
      - The application runs inside Docker containers on Google Compute Engine Virtual Machines, VMs.
      - Ability to SSH into the virtual machines on which your application runs.
      - It lets you use local disk for scratch base, it lets you install third-party software, and it lets your application make calls to the network without going through App Engine.
      - Offers a free daily usage quota for the use of some services.
      - In the middle between App Engine Standard and Kubernetes Engine.
      - You get to choose which region your applications run in.

1. **Kubernetes Engine**:
   - A group of machines where Kubernetes can schedule workloads.
   - Saves you infrastructure chores(IaaS).
   - It's managed Kubernetes.
   - Kubernetes makes it easy to orchestrate many Containers on many hosts.
   - On each host is an operating system that supports Containers and a Container run-time.
   - K8s Engines helps for: Application configuration, service discovery, managing updates, and monitoring
   - Kubernetes lets you deploy containers on a set of nodes(nodes are virtual machines running in Compute Engine) called a cluster.
   - Each pod in Kubernetes gets a unique IP address and set of ports for your containers.
   - A deployment represents a group of replicas of the same pod.
   - A service groups a set of pods together and provides a stable endpoint for them. That could be a public IP address managed by a network load balancer.
   - With Rolling-Updates, kubernetes will create pods of the new version one-by-one.



### Multi-cloud architecture (Anthos advertisement)

- It allows you to keep parts of your systems infrastructure on-premises while moving other parts to the Cloud.
- Hybrid infrastructure(On-Prem+Cloud-Based): Anthos is a hybrid and multi-cloud solution powered by the latest innovations in distributed systems, and service management software from Google.
- Maximum number of zones is three (October 2019)
- Anthos, an Istio Open Source service mesh take lots of guesswork out of managing(keeping track of services, monitoring their health) and securing your microservices.
- Communication across the hybrid network works with Cloud interconnect.
- Stackdriver is the built-in logging, alerting and monitoring solution for Google Cloud.
- Anthos Configuration Management provides a single source of truth for your clusters configuration.
- Anthos Configuration Management provides the ability to deploy code changes with a single repository commit.


### Two API management tools (Cloud Endpoints / Apigee Edge)
1. **Cloud Endpoints**:
- Cloud Endpoints helps you create and maintain API's.
- Restrict API access to known developer's
- Monitoring and log its use.
- Generate client libraries.

2. **Apigee Edge**:
- Helps you secure and monetize APIs
- PaaS for making APIs available to your customers.
- Developing and managing API proxies.
- Contains analytics, monetization, and a developer portal.
- Focus on: Business problems like rate limiting, quotas, and analytics.
- Backend services for Apigee Edge need not be in GCP.
- Use Case: You want to gradually decompose a pre-existing monolithic application, not implemented in GCP, into microservices.


### Miscellaneous cloud capablities
1. Cloud Source Repositories
- Keeping source code private to a GCP project and use IAM permissions to protect it, but not having to maintain a Git instance yourself.

2. Cloud Functions
- Ability to write code without worrying about servers or runtime binaries + configuring when to fire the code.
- You pay whenever your functions run, in 100 millisecond intervals.
- Functions can trigger on events in Cloud Storage, Cloud Pub/Sub, or in HTTP call.
- Often used to enhance existing applications without having to worry about scaling.

3. Stackdriver
- Core components of Stackdriver: Monitoring, Logging, Trace, Error Reporting and Debugging, Profiler.
- With Stackdriver Trace, you can sample the latency of app engine applications and report Per-URL statistics.
- Stackdriver Logging lets you define metrics based on your logs.

4. Deployment Manager
- Deployment Manager is an infrastructure management system for GCP resources.
- Component to provision declaratively(deployments) vm's.

### Big Data and Machine Learning

#### Services:
1. Cloud Dataproc
   - Managed Hadoop(Open source framework for big data, based on the MapReduce programming model)
   - MapReduce: The "Map function" runs in parallel with a massive dataset to produce intermediate results. And another function, traditionally called the "Reduce function," builds a final result set based on all those intermediate results.
   - Managed way to run Hadoop and Spark/Hive/Pig on GCP
   - Although the rate for pricing is based on the hour, Cloud Dataproc is billed by the second.
   - You can save money, by telling Cloud Dataproc to use preemptible Compute Engine instances for your batch processing.
   - Great when you have a data set of known size or when you want to manage your cluster size yourself.
2. Cloud Dataflow
   - Good for real time data or data that's of unpredictable size or rate.
   - Let's you execute a big range of data processing patterns: extract, transform, and load batch computation and continuous computation.
   - It's general purpose ETL tool and its use case as a data analysis engine comes in handy.
   - Source(BigQuery) - Transform(Cloud Dataflow) - Sink(Cloud Storage)
3. BigQuery
   - Provides near real-time interactive analysis of massive datasets using SQL syntax.
   - Petabyte-scale, low-cost analytics data warehouse.3
   - Load data into it from cloud storage or cloud data store, or stream it into BigQuery at up to 100,000 rows per second.
   - Free monthly quotas.
   - BigQuery separates storage and computation.
   - Compute and storage are seperated.
   - You only pay for storage and processing used.
   - Automatic discount for long-term data storage.
4. Cloud Pub/Sub
   - Scalable messaging
   - Application components make push/pull subscriptions to topics.
   - Designed to provide "at least once" delivery at low latency(There is a small chance some messages might be delivered more than once).
   - On-demand scalability to one million messages per second and beyond.
   - You're able to configure the subscribers to receive messages on a push or pull basis.
5. Cloud Datalab
   - Offers interactive data exploration.
   - Tool for large-scale data exploration, transformation, analysis, and visualization.
   - Runs in a Compute Engine virtual machine.
   - Built on Jupyter(lets you create and maintain web-based notebooks containing Python code and you can run that code interactively and view the results).
   - Integrated with BigQuery, Compute Engine, and Cloud Storage.
6. Cloud Machine Learning Platform
- TensorFlow is an open source tool to build and run neural network models.
- GCP makes TPUs(hardware devices designed to accelerate machine learning workloads with TensorFlow) available in the cloud with Compute Engine virtual machines.
- Wide range of machine learning APIs suited to specific purposes.


**2 categories of ML-Applications:**
   1. Structured Data
   - Classification and regression(e.g. customer churn analysis)
   - Recommendation(e.g. content personalization)
   - Anomaly detection(e.g. sensor diagnostics)
   2. Unstructured Data
   - Image and Video analytics(e.g. identifying damaged shipment)
   - Text analytics(e.g. sentiment analysis)
- Machine Learning APIs available like:
  - Cloud Vision API(Analyze images e.g. extract text, analyze sentiment)
  - Cloud Natural Language API(Convert audio to text, parse text,translating)
  - Cloud Video Intelligence API(Annotate videos)