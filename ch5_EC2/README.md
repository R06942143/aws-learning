# ch5
---
## EC2
- EC2 is one of the most popular services in AWS
- It mainly consists in the capability of:
  - Renting virtual machines (EC2)
  - Storing data on virtual drives (EBS)
  - Distributing load across machines (ELB)
  - Scaling the services using an auto-scaling group (ASG)

## EC2 sizing & configuration types
- Operating system
- How much power (CPU)
- How much RAM
- How much disk space
  - Network-attached (EBS & EFS)
  - hardware (EC2 instance store)
- Network card
  - Speed of the card
  - Public IP address
  - Firewall rules (security groups)
- Bootstrap script / User data
  - Launch commands on the instance at first start
  - Ex: installing updates, downloading common files from the internet

## EC2 User Data
- It is possible to bootstrap our instances using an EC2 User Data script
- bootstrapping means launching commands when a machine starts
- That script is only run once at the instance first start
- EC2 User Data is used to automate boot tasks such as:
  - Installing updates
  - Installing software
  - Downloading common files from the internet
  - Anything you can think of
- The EC2 User Data Script runs with the root user

## EC2 Instance types
- Each instance type has different characteristics and pricing
- T-series:
  - Burstable performance
  - Great for web servers & small DBs
- C-series:
  - Compute optimized
  - Great for CPU intensive tasks / DBs
- R-series:
  - Memory optimized
  - Great for memory intensive tasks / DBs
- M-series:
  - Balanced
  - Great for general purpose apps
- A-series:
  - Arm-based workloads
- F-series:
  - Accelerated computing
  - Great for machine learning, data science, etc...
- P-series:
- GPU instances

## EC2 Instance Types Overview
- AWS has the following naming convention:
> m5.2xlarge
> - m: instance class
> - 5: generation(AWS improves the hardware generation every 12-18 months)
> 2xlarge: size within the instance class

## EC2 Instance Types - General Purpose
- Great for a diversity of workloads such as:
  - Small & medium databases
  - Data processing tasks
  - Backend servers
  - Caching fleets
  - Application servers

## EC2 Instance Types - Compute Optimized
- Great for compute-bound applications that benefit from high performance processors
  - Batch processing workloads
  - Media transcoding
  - High performance web servers
  - High performance computing (HPC)
  - Scientific modeling & machine learning
  - Dedicated gaming servers


## EC2 Instance Types - Memory Optimized
- Great for memory-bound applications that require high performance processors
  - High performance databases
  - Distributed web scale cache stores
  - In-memory databases optimized for BI
  - Applications performing real-time processing of big unstructured data

## EC2 Instance Types - Storage Optimized
- Great for storage-intensive tasks that require high, sequential read and write access to large data sets on local storage
  - High frequency online transaction processing (OLTP) systems
  - Relational & NoSQL databases
  - Data warehousing applications
  - Distributed file systems
  - Log or data processing applications


##