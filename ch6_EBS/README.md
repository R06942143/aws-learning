# CH6
---
## What is EBS?
- An EBS volume is a network drive you can attach to your instances while they run
- It allows your instances to persist data, even after their termination
- They can only be mounted to one instance at a time (at the CCP level)
- They are bound to a specific Availability Zone (AZ)
- Analogous: to a USB stick (you can plug it in to any computer)

## EBS Volume
- It is a network drive (i.e. not a physical drive)
  - It uses the network to communicate the instance, which means there might be a bit of latency
  - It can be detached from an EC2 instance and attached to another one quickly
- It is locked to an AZ
  - To move a volume across, you first need to snapshot it
  - An EBS volume in us-east-1a cannot be attached to us-east-1b
- Have a provisioned capacity (size in GBs, and IOPS)
  - You get billed for all the provisioned capacity
  - You can increase the capacity of the drive over time

## EBS - Delete on Termination Attribute
- By default, the root EBS volume is deleted when the instance is terminated
- By default, any other attached EBS volume is not deleted when the instance is terminated
- This can be controlled by the "Delete on Termination" flag

## About EBS Multi-Attach
- EBS volumes can only be attached to one instance in one AZ is not true for io1 and io2 volumes: this is called [Multi-Attach](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-volumes-multi.html)

## EBS Snapshots
- Make a backup (snapshot) of your EBS volume at a point in time
- Not necessary to detach volume to do snapshot, but recommended
- Can copy snapshots across AZ or Region

## EBS Snapshots Features
- EBS Snapshot Archive
  - Move a Snapshot to an "archive tier" that is less expensive
  - Takes within 24 to 72 for restoring the achived snapshot
- Recycle Bin for EBS snapshots
  - When you delete a snapshot, it goes to the recycle bin
  - Resources in the Recycle Bin are billed at their standard rates. There are no additional charges for using Recycle Bin and retention rules. For more information, see [Amazon EBS pricing](http://aws.amazon.com/ebs/pricing/).
  - Specify retention (from 1 to 365 days)

## AMI overview
- AMI = Amazon Machine Image
- AMI are a customization of an EC2 instance
  - You add your own software, configuration, operating system, monitoring...
  - Faster boot / configuration time because all your software is pre-packaged
- AMI are built for a specific region (and can be copied across regions)
- You can launch EC2 instances from:
  - A Public AMI: AWS provided
  - Your own AMI: you make and maintain them yourself
  - An AWS Marketplace AMI: an AMI someone else made

## AMI Process
- Start an EC2 instance and customize it
- Stop the instance (for data integrity)
- Build an AMI - this will also create EBS snapshots
- Launch instances from other AMIs

- You can create your own AMI by right click on the instance and select "Image" -> "Create Image"

## EC2 Image Builder
- EC2 Image Builder is a service that makes it easier and faster to build and maintain secure images for Windows and Linux EC2 instances
- Used to automate the creation, management, and deployment of customized, secure, and up-to-date "golden" server images that are pre-installed and pre-configured with software and settings to meet specific IT standards
- Can be run on a schedule or triggered by events
- Free service, you only pay for the underlying resources (EC2, EBS, S3, etc.)
![EC2 Image Builder](image.png)

## EC2 Instance Store
- EBS volumes are network drives with good but "limited" performance
- If you need a high-performance hardware disk, use EC2 Instance Store
- Better I/O performance
- EC2 Instance Store lose their storage if they're stopped (ephemeral)
- Good for buffer / cache / scratch data / temporary content
- Risk of data loss if hardware fails
- Backups and Replication are your responsibility

## Local EC2 Instance Store
![Alt text](image-1.png)

## EFS - Elastic File System
- Managed NFS (Network File System) that can be mounted on 100s of EC2
- EFS works with EC2 instances in multi-AZ
- Highly available, scalable, expensive (3x gp2), pay per use, no capacity planning
- ![Alt text](image-2.png)

## EBS vs EFS
- EBS is only available in one AZ and can be attached to only one EC2 instance in your VPC
- EFs is expensive (3x gp2), but can be attached to multiple EC2 instances across multi-AZ
![Alt text](image-3.png)

## EFS Infrequent Access(EFS-IA)
- Storage class that is cost-optimized for files not accessed every day
- Up to 92% lower cost compared to EFS Standard storage class
- EFS will automatically move files to EFS-IA based on last access time
- Enable EFS-IA with a Lifecycle Policy
- Transparent to the application accessing the files
![Alt text](image-4.png)

## Shared Responsibility Model for EC2 Storage
![Alt text](image-5.png)


## Amazon FSx - Overview
- Launch 3rd party file systems (Windows File Server, Lustre, etc.) on AWS
- Fully managed, highly reliable, scalable, expensive

## Amazon FSx for Windows File Server
- Fully managed native Microsoft Windows File System
- Built on Windows File Server
- Supports SMB protocol & Windows NTFS
- Integrated with Microsoft Active Directory
- Can be accessed from on-premise
![Alt text](image-6.png)

## Amazon FSx for Lustre
A fully managed file system optimized for compute-intensive workloads, such as high performance computing, machine learning, and media data processing workflows.
- Scales up to 100s GB/s, millions of IOPS, sub-ms latencies

## EC2 Instace Storage - Summary
- EBS volumes 
  - network drives with good but "limited" performance
- EFS:
  - Network file system (NFS) that can be mounted on many EC2
- EFS-IA:
  - Cost-optimized storage for files not accessed every day
- FSx for Windows File Server:
  - Fully managed native Microsoft Windows File System
- FSx for Lustre:
  - Fully managed file system optimized for compute-intensive workloads