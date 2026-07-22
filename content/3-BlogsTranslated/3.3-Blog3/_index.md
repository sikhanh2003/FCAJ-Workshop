---
title: "Blog 3"
date: "2024-01-01"
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---
# AWS COST OPTIMIZATION – Migrating Amazon EBS Volumes from gp2 to gp3
-----

### ARCHITECTURE AND PERFORMANCE COMPARISON: gp2 VS gp3
The core difference between the two disk generations lies in their performance provisioning mechanism:

gp2 (Performance Tied to Capacity): Disk performance is strictly locked to storage capacity (3 IOPS/GB). If an application requires more IOPS, you are forced to increase the volume capacity (e.g., to get 3,000 IOPS, the disk must be at least 1,000 GB), which wastes money on unused space.

gp3 (Capacity and Performance Decoupled): Designed with complete independence between Capacity, IOPS, and Throughput. A default gp3 volume provides 3,000 IOPS and 125 MB/s Throughput completely free, independent of disk size. When higher performance is needed, you can purchase additional IOPS or Throughput separately without expanding capacity.

---
### Quick Comparison:

Storage Unit Price: gp3 is up to 20% cheaper than gp2 across all regions.

Default Baseline: gp2 delivers 3 IOPS/GB (up to 16,000 IOPS), while gp3 provides a fixed 3,000 IOPS (up to 16,000 IOPS).

Default Throughput: gp2 ranges from 128 MB/s to 250 MB/s (depending on capacity), whereas gp3 is fixed at 125 MB/s (can be actively increased up to 1,000 MB/s).

Scaling Mechanism: gp2 forces you to buy more GBs to scale performance, while gp3 lets you independently customize GBs, IOPS, and Throughput.

---
### CORE BENEFITS AND PRIORITY WORKLOADS
Immediate FinOps Budget Optimization: The GB/month unit price of gp3 is roughly 20% lower than gp2. For systems operating hundreds or thousands of volumes, migration delivers massive monthly operational cost savings.

Zero-Downtime Migration: Thanks to Amazon EBS Elastic Volumes, moving from gp2 to gp3 happens directly on active volumes. EC2 instances continue running normally without requiring reboots, data restoration, or application disruptions.

Priority Workloads for Migration:

Web Applications & API Servers

Small and Medium Databases (MySQL, PostgreSQL, MongoDB, SQL Server)

Bastion Hosts, Monitoring Servers (Prometheus, Zabbix)

CI/CD Workers (Jenkins, GitLab Runner)

File Servers & Storage Nodes

---
### AUDITING, AUTOMATION, AND MONITORING PROCESS FOR DEVOPS
To execute bulk migrations safely and efficiently, DevOps teams can follow this technical workflow:

Step 1: Audit Existing gp2 Volumes: Use administrative tools like AWS Cost Optimization Hub, AWS Cost Explorer, or AWS CLI to identify volumes needing upgrades and estimate cost savings.

Step 2: Automate the Migration Process (IaC & Automation): Instead of manually operating each volume on the AWS Management Console, use AWS Systems Manager (SSM) Automation or Lambda to call the ModifyVolume API for bulk upgrades. For Infrastructure as Code (Terraform / CloudFormation / AWS CDK), update the property volume_type = "gp3" in infrastructure management code to prevent IaC from overwriting old configurations during future deployments.

Step 3: Monitor CloudWatch Metrics Post-Migration: After upgrading, track key metrics on Amazon CloudWatch for 7–14 days:

VolumeReadOps and VolumeWriteOps: Calculate total actual IOPS consumed.

VolumeThroughputPercentage: Check bandwidth consumption.

VolumeConsumedReadWriteOps: Check if the system experiences throttling due to exceeding the default 3,000 IOPS threshold. If so, proactively configure higher IOPS for that volume.

---
### CONCLUSION
Migrating from gp2 to gp3 is one of the highest cost-benefit ratio "Quick Wins" on AWS. Businesses instantly cut storage costs by 20% while gaining flexible, independent performance without accepting any system downtime. If your infrastructure still runs gp2 drives, now is the ideal time to automate this upgrade process.

Reference Source: https://aws.amazon.com/blogs/storage/migrate-your-amazon-ebs-volumes-from-gp2-to-gp3-and-save-up-to-20-on-costs/

#AWS #AmazonEBS #AWSStorage #CostOptimization #FinOps #AmazonEC2 #CloudComputing #DevOps

-----

**TAGS:** announcements, Artificial Intelligence, AWS Public Sector, education, skills, skills development, workforce development

