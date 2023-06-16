# ch7
---
## Scalability & High Availability
- Scalability means that an application / system can handle greater loads by adapting
- There are two kinds of scalability:
  - Vertical Scalability
  - Horizontal Scalability
- Scalability is linked but different to High Availability

### Vertical Scalability
- Vertical Scalability means increasing the size of the instance
- Vertical Scalability is very common for non-distributed systems, such as a database
- There's usually a limit to how much you can vertically scale (hardware limit)

### Horizontal Scalability
- Horizontal Scalability means increasing the number of instances / systems for your application
- Horizontal Scaling implies distributed systems


## High Availability
- High Availability usually goes hand in hand with Horizontal Scaling
- High Availability means running your application / system in at least 2 data centers (ie: 2 AZs)
- The goal of High Availability is to survive a data center loss


## High Availability & Scalability for EC2
- Vertical Scaling for EC2:
  - Buy a bigger instance (more RAM, CPU, EBS...)
  - Pros:
    - No need to manage a group of instances
    - No need to manage inter-instance communication
  - Cons:
    - Limited by the size of the instance
    - If your app is not designed properly for distributed systems, it won't work
- Horizontal Scaling for EC2:
  - Increase the number of instances
  - Pros:
    - No need to manage a bigger instance
    - Better fault tolerance
    - Better load distribution
  - Cons:
    - Need to manage a group of instances (automatically or manually)
    - Need to manage inter-instance communication
    - More difficult to implement
- High Availability for EC2:
  - Run instances for your application in 2+ AZs
  - Pros:
    - If one AZ goes down, the application is still available
  - Cons:
    - More difficult to implement
    - Eventual Consistency for data (if using RDS, EBS, ElastiCache...)

## Scalability vs Elasticity (vs Agility)
- Scalability: ability to accomodate a larger load by making the hardware stronger (scale up / scale vertically) or by adding nodes (scale out / scale horizontally)
- Elasticity: once a system is scalable, elasticity means that you can automate the scalability: scale up if need be, scale down if you don't need it
- Agility: measure of how quickly you can change the size of your resources (vertical scaling is not very agile, horizontal scaling is)

## What is load balancing?
- Load Balancer are servers that forward internet traffic to multiple servers (EC2 Instances) downstream

## Why use a load balancer?
- Spread load across multiple downstream instances
- Expose a single point of access (DNS) to your application
- Seamlessly handle failures of downstream instances
- Do regular health checks to your instances
- Provide SSL termination (HTTPS) for your websites
- High Availability across zones

## Why use an EC2 Load Balancer?
- An ELB (EC2 Load Balancer) is a managed load balancer
  - AWS guarantees that it will be working
  - AWS takes care of upgrades, maintenance, high availability
  - AWS provides only a few configuration knobs
- It costs less to setup your own load balancer but it will be a lot more effort on your end (maintenance, upgrades, etc...)
- 4 kinds of load balancers offered by AWS:
  - Classic Load Balancer (retired 2023) - Layer 4 & 7
  - Application Load Balancer (HTTP / HTTPS only) - Layer 7
  - Network Load Balancer (ultra-high performance, allows for TCP) - Layer 4
  - Gateway Load Balancer (new) - Layer 3
![Alt text](image.png)

## What's an Auto Scaling Group?
- In real-life, the load on your websites and applications can change
- In the cloud, you can create and get rid of servers very quickly
- The goal of an Auto Scaling Group(ASG) is to:
  - Scale out (add EC2 instances) to match an increased load
  - Scale in (remove EC2 instances) to match a decreased load
  - Ensure we have a minimum and a maximum number of machines running
  - Automatically register new instances to a load balancer
  - Replace unhealthy instances
- Cost Saving: only run at an optimal capacity (principle of cloud)


## Auto Scaling Group in AWS
![Alt text](image-1.png)

## Auto Scaling Group in AWS With Load Balancer
![Alt text](image-2.png)

## Auto Scaling Group - Scaling Strategies
- Manaual Scaling
  - Not recommended
  - Set the ASG size yourself (eg: min = 5, max = 10, desired = 5)
- Dynamic Scaling: Respond to changing demand
  - Simple / Step Scaling
    - When a CloudWatch alarm is triggered (example: CPU > 70%), then add 2 units
    - When a CloudWatch alarm is triggered (example: CPU < 30%), then remove 1 unit
  - Target Tracking Scaling (default)
    - Most simple and easy to set-up
    - Example: I want the average ASG CPU to stay at around 40%
  - Scheduled Scaling
    - Anticipate a scaling based on known usage patterns
    - Example: increase the min capacity to 10 at 5pm on Fridays
  - Predictive Scaling (new)
    - Uses Machine Learning to predict the future
    - Example: increase capacity by 20 at 4:30pm based on an event (eg: a TV ad)

# ELB & ASG - Summary
- High Availability vs Scalability (Vertical vs Horizontal) vs Elasticity vs Agility in the Cloud
- Elastic Load Balancer (ELB)
  - Distribute traffic across AZs in one region
  - Supports health checks
  - 4 types: Classic, Application, Network, Gateway
- Auto Scaling Groups (ASG)
  - Implement elasticity for your application
  - Scale EC2 instances based on metrics (CPU, ASG...)
  - integrated with ELB, can be triggered by CloudWatch
