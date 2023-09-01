[[EBS vs EFS]]
# What is EBS
EBS (Elastic block storage) is an Amazon block-level storage service that is intended to be used exclusively with separate EC2 instances; no two instances can have the same EBS volume attached to them. EBS provides a high-performance option for many use cases because it is directly attached to the instance, and it is used for various databases (both relational and non-relational) as well as a wide range of applications such as software testing and development.



# Introduction to Elastic Block Store (EBS)
#chat <mark style="background: #FFF3A3A6;">from transcript</mark>

---

**Welcome:**

- Welcome to today's session, where we'll delve deep into the realm of EBS.

---

**What is EBS?**

- EBS stands for Elastic Block Store.
- It's essentially a raw and unformatted storage solution available to users.
- Think of it as akin to RAM for a physical machine. Just like RAM is a fast-accessible memory for physical computers, EBS serves as a quick-access memory for virtual machines.

---

**Using EBS:**

1. **Initial Setup:**
    - EBS volumes come unformatted.
    - Before using an EBS volume, you need to format it. Only after formatting can you begin using it.
2. **Root Volume vs. Manually Attached EBS:**
    - If using the root volume (attached during instance launch), it's already formatted.
    - If you're manually attaching an EBS volume to an instance, remember to format it before use.

---

**Key Features of EBS:**

1. **Flexibility:**
    - Choose your EBS type based on IOPS (Input/Output Operations Per Second) and throughput needs.
2. **Location:**
    - It's best to have the EBS in the same availability zone as your machine. This ensures faster access times.
3. **Customizable Storage:**
    - Specify the storage capacity you need when setting up EBS.


# EBS Concepts

- It is the raw unformatted block-level storage; it is exposed as raw device to the EC2 instance EBS volumes persist independently from the life Of the EC2 instance
- An EBS volume is automatically replicated within an availability zone

**Throughput**: 
It is the sequential transfer rate that an SSD or HDD will maintain continuously

![[IOPS]]


**Deep Dive into Elastic Block Store (EBS) Concepts**

---

**Welcome:**

- Welcome back to our session on EBS concepts.

---

**Review of EBS:**

- EBS is a raw, unformatted storage option available within the AWS ecosystem.

---

**Key Performance Metrics:**

1. **Throughput:**
    - Measures the amount of data transferred from/to storage in seconds or minutes.
2. **IOPS (Input/Output Operations Per Second):**
    - Provides a rate at which input and output operations are processed per second on storage.

---

**Types of EBS Volumes:**
![[EBS Volume Types.png]]
1. **General Purpose SSD:**
    - Offers a baseline of 3 IOPS per GB with a range of 100 to 10,000 IOPS.
    - Burst performance: 3,000 IOPS.
2. **Provisioned IOPS SSD:**
    - More performant than the general purpose SSD. Ideal for high-performance needs.
3. **Throughput Optimized HDD:**
    - Focused on providing superior throughput. Suited for large streaming workloads.
4. **Cold Storage HDD:**
    - Ideal for infrequently accessed data requiring high throughput.

---

**Comparing SSD and HDD:**

- **SSD (Solid State Drive):**
    - Performs better for smaller, random I/O operations.
    - Performance metric: IOPS.
- **HDD (Hard Disk Drive):**
    - Better for large streaming workloads.
    - Performance metric: Throughput.

---

**Advanced EBS Features:**

1. **Multi-Attach:**
    - A feature that lets you attach a single EBS volume to multiple EC2 instances (limited to AWS Nitro System based Amazon EC2 in the same availability zone).
      
      Amazon EBS Multi-Attach is now available on Provisioned IOPS io1 volumes
      
      We can now enable Multi-Attach on Amazon EBS Provisioned IOPS [[IO1 volumes]] to allow a single volume to be concurrently attached to up to 16 AWS Nitro System-based Amazon EC2 instances within the same availability zone


   

2. **Snapshots:**
    - Backups of your EBS volumes.
    - First snapshot is a full copy; subsequent snapshots are incremental.
    - Stored in Amazon S3 and can be transferred across regions.

---

**Managing EBS with [[AWS Data Lifecycle Manager]]:**

- [[AWS Data Lifecycle Manager|Amazon DLM]] supports Amazon EBS volumes and snapshots
- We can define backup and retention schedules for EBS snapshots by creating lifecycle policies based on tags 
- It is free to use
- We no longer need to create custom scripts for backup and restore

Automating the snapshot cycle helps with:
- Protecting valuable data by enforcing a regular backup schedule
- Retaining backups as required by auditors or internal compliance
- Reducing storage costs by deleting outdated backups

---

**EBS Encryption:**

- Encrypt EBS volumes to secure data.
- Protection against potential threats and malware.
- Encryption applies to volumes, not instances.

---

# EBS Pricing
![[Pasted image 20230821193744.png]]
### Free Tier Eligibility
- You get 30GB per month of free EBS data storage, which combines GP2 and magnetic types, along with some I/O operations and snapshots.

### Standard EBS Volumes
- If you exceed the 30GB free tier or use other types like Provisioned IOPS or Throughput Optimized, you will incur charges.

### Snapshots
- Creating snapshots is also chargeable if you're not under the free tier.

### Service Level Agreement (SLA)
- EBS also comes with a 99.99% availability guarantee.