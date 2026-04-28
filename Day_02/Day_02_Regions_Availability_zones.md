## 1 AWS Region
 - An AWS Region is a geographical area where AWS has multiple data centers.
 
 ### Example
 - Mumbai Region 			→ ap-south-1
 - US East (N. Virginia)	→ us-east-1
 ### Key_Points 
 - Each region is completely independent
 - Data does NOT automatically replicate across regions
 - You choose a region based on:
 - Latency (closer to users = faster)
 - Compliance (data residency laws)
 - Cost (pricing varies per region)
 ### Note : 
 - If Mumbai region goes down, your app is dead unless you designed it to run in another region.

---

## 2 Availability Zone (AZ)
 - An Availability Zone is a physically separate data center (or group of data centers) within a region.

 ### Example (inside Mumbai region):
 - ap-south-1a
 - ap-south-1b
 - ap-south-1c
 ### Key Points:
 - AZs are isolated from each other
 - Connected with low-latency, high-speed networking
 - Designed for fault isolation

 ### Note : 
 - If one AZ fails, your application should still run from another AZ if architected properly.
 
--- 

## 3 Quick Summary
 - Region is a geographical area, and Availability Zone is an isolated data center within that region used for high availability.
 - In AWS, a Region is a completely isolated geographic boundary, and within each region, we have multiple Availability Zones which are isolated data centers.
 - In production, we design applications across multiple AZs to achieve high availability. For example, I deploy EC2 instances in at least two AZs behind an Application Load Balancer and configure RDS in Multi-AZ mode.
 - This ensures that even if one AZ fails due to power or network issues, the application remains available.
 - For disaster recovery scenarios, we extend this design across regions using replication strategies.
 - Deploy app across multiple AZs → high availability
 - Deploy across multiple regions → disaster recovery