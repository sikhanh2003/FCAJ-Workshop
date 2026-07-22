---
title: "Translated Blogs"
weight: 3
chapter: false
pre: " <b> 3. </b> "
---
This section will list and introduce the blogs you have translated. For example:

###  [Blog 1 - AWS SECURITY & S3 – Amazon S3 to Disable SSE-C by Default in April 2026: What Developers and DevOps Need to Know](3.1-Blog1/)
Amazon S3 is one of the most popular storage services on AWS, used for everything from static websites and data lakes to backups and AI/ML applications. Alongside limitless scalability, data security is always a top priority for AWS.
Recently, AWS announced a major change regarding Server-Side Encryption with Customer-Provided Keys (SSE-C). Starting in April 2026, new S3 General Purpose Buckets will no longer support SSE-C by default, which directly impacts applications using this encryption method.

###  [Blog 2 - AWS BACKUP – Item-Level Recovery for Amazon EBS and Amazon S3](3.2-Blog2/)
Accidentally deleting data is a common operational issue—whether it's a config file, log, PDF, or video stored on Amazon EBS or Amazon S3. Previously, recovering a single file from an EBS Snapshot or AWS Backup meant restoring the entire volume, attaching it to an EC2 instance, and manually copying the file, which wasted time, compute resources, and storage costs.
To solve this, AWS introduced AWS Backup Search and Item-Level Recovery, enabling direct searching and restoring of individual files from Amazon EBS and Amazon S3 backups.

###  [Blog 3 - AWS COST OPTIMIZATION – Migrating Amazon EBS Volumes from gp2 to gp3](3.3-Blog3/)
Amazon EBS (Elastic Block Store) is a popular block storage service used alongside Amazon EC2 for many production systems. Over the years, many businesses still run a large volume of EBS volumes using gp2 (General Purpose SSD) because it used to be the default AWS choice.
