# **EC2 Storage Overview**

# **Elastic Block Store (EBS)**

### **Overview**
Amazon EBS is a persistent block storage service designed for EC2 instances. It provides high availability and durability, with data stored across multiple Availability Zones (AZs). EBS volumes can be attached to any EC2 instance in the same AZ.

---

### **Types of EBS Volumes**
1. **General Purpose SSD (gp3/gp2)**:
   - Balanced price and performance for general workloads.
   - Use Case: Boot volumes, small to medium databases.

2. **Provisioned IOPS SSD (io1/io2)**:
   - High-performance volumes for I/O-intensive applications.
   - Use Case: Databases requiring low-latency, high IOPS.

3. **Throughput Optimized HDD (st1)**:
   - Designed for high-throughput workloads.
   - Use Case: Big data, log processing, large datasets.

4. **Cold HDD (sc1)**:
   - Cost-effective storage for infrequently accessed data.
   - Use Case: Cold storage, file archiving.

---

### **Key Features**
- **Snapshots**: EBS volumes can be backed up as point-in-time snapshots to Amazon S3 for durability and easy restoration.
- **Encryption**: EBS volumes support encryption at rest and in transit.
- **Elasticity**: You can increase volume size or change types without downtime.

---

### **Use Cases**
- Databases (e.g., MySQL, PostgreSQL) with consistent I/O needs.
- Boot volumes for EC2 instances.
- Storage for critical applications requiring durability and reliability.

# **EBS Snapshots**

### **Overview**
EBS Snapshots are point-in-time backups of Amazon EBS volumes. These backups are stored by AWS and allow you to create new volumes or restore an existing volume to its previous state.

---

### **Key Features**
- **Incremental**: Only the changed data since the last snapshot is saved, reducing storage costs.
- **Cross-Region Copy**: Snapshots can be copied to other AWS regions for disaster recovery or migration.
- **Encryption**: Snapshots retain the encryption settings of the original volume.

---

### **Use Cases**
- Disaster recovery, backup, and creating test environments.
# **Additional EBS Features**

### **Performance Modes**:
- **GP3**: Offers baseline IOPS and throughput, but you can provision additional performance.
- **Provisioned IOPS (io1/io2)**: Consistent, high-performance volumes for I/O-heavy applications.

### **Elastic Volumes**:
- EBS volumes can be resized, and performance characteristics can be changed without detaching the volume, offering flexibility without downtime.

### **Snapshots Lifecycle**:
- Use **Amazon Data Lifecycle Manager** to automate and manage EBS snapshot creation and retention.

### **Multi-Attach (io1/io2)**:
- Enables multiple EC2 instances to attach to the same EBS volume for high availability.
# **Elastic File System (EFS)**

### **Overview**
Amazon EFS is a scalable, managed file storage system for Linux workloads, offering shared access to multiple EC2 instances. It automatically scales with your data needs and provides high availability across multiple Availability Zones (AZs).

---

### **Key Features**
- **Elastic Scaling**: Automatically adjusts capacity as data is added or removed.
- **Multi-AZ Availability**: Ensures high availability and redundancy.
- **Performance Modes**: 
  - **General Purpose** for low-latency.
  - **Max I/O** for high throughput.
- **Storage Classes**: 
  - **Standard** for frequently accessed data.
  - **Infrequent Access (IA)** for cost-effective storage of infrequently accessed data.

---

### **Access & Security**
- **POSIX-compliant**: Supports Unix/Linux file permissions and directory structure, ensuring compatibility for Linux workloads.
- **VPC Security**: Controlled via VPC security groups.
- **Cross-Region and On-Premises Access**: Can be accessed from AWS or on-premises via Direct Connect.

---

### **Use Cases**
- Web serving, content management, big data analytics, shared development environments, and machine learning workloads.

# **EC2 Instance Store**

### **Overview**
EC2 Instance Store provides temporary, high-performance storage directly attached to the physical host where an instance runs. Unlike EBS, data in instance store is ephemeral and is lost if the instance is stopped, terminated, or fails.

---

### **Key Features**
- **Ephemeral**: Data persists only during the instance's lifetime.
- **High Performance**: Ideal for low-latency, high-speed storage.
- **No Cost**: Included with the instance type.

---

### **Use Cases**
- Temporary data storage, such as caches, buffers, or scratch data.

# **Detailed Comparison: EBS, EFS, and Instance Store**

| Feature            | **EBS**                                        | **EFS**                                       | **Instance Store**                         |
| ------------------ | ---------------------------------------------- | --------------------------------------------- | ------------------------------------------ |
| **Persistence**    | Persistent across instance stops               | Persistent, elastic, shared file system       | Ephemeral (lost on stop/terminate)         |
| **Performance**    | Up to **64,000 IOPS** (Provisioned IOPS io2)   | Scales up to **10 GB/s throughput**           | High-speed, low-latency                    |
| **Max Throughput** | **1,000 MB/s** (gp3), **16,000 MB/s** (io2)    | Up to **10 GB/s**                             | Depends on instance type                   |
| **Availability**   | AZ-specific                                    | Multi-AZ                                      | Host-specific                              |
| **Cost**           | Pay per volume size, IOPS, and throughput      | Pay per GB usage (higher for frequent access) | Included with instance, no separate cost   |
| **Use Cases**      | Databases, boot volumes, critical applications | Shared file systems, multi-instance workloads | Caches, buffers, temporary data            |
| **Pricing**        | **gp3**: ~$0.08/GB, **io2**: ~$0.125/GB        | ~$0.30/GB (Standard), ~$0.025/GB (Infrequent) | No separate cost, tied to instance pricing |
| **Durability**     | **99.999%** for io2                            | **11 nines (99.999999999%)**                  | Non-durable, no data persistence           |

# **Amazon Machine Image (AMI)**

### **Overview**
An Amazon Machine Image (AMI) is a pre-configured template that contains the information needed to launch an EC2 instance, including:
- **Operating System (OS)**.
- **Application Software**.
- **Configuration settings**.

### **Types of AMIs**
- **Public AMIs**: Available for anyone to use.
- **Private AMIs**: Created by you and available only to your AWS account.
- **Marketplace AMIs**: Provided by third-party vendors.

### **Use Case**
AMIs enable you to create instances quickly, replicate environments, or launch multiple instances with the same configuration.


# **EC2 and Storage Knowledge Check Questions**

### **EC2 Questions**

1. **Scenario**: You need to run a high-traffic e-commerce website that experiences significant spikes during sales events. Which EC2 instance pricing model would you choose, and why? Explain how you would ensure cost-efficiency while handling traffic spikes.
   - **A)** On-Demand Instances, no scaling
   - **B)** Spot Instances with Auto Scaling
   - **C)** Reserved Instances with Auto Scaling
   - **D)** On-Demand Instances with Auto Scaling
   - **Answer**: **D)** On-Demand Instances with Auto Scaling for dynamic scaling during traffic spikes without upfront commitment.

2. **Scenario**: You have multiple applications that need to run in isolated environments, but they share large datasets that need to be accessed by each application simultaneously. Which storage solution would you recommend, and how would you configure it?
   - **A)** Instance Store
   - **B)** EBS volumes with separate EC2 instances
   - **C)** Amazon EFS with EC2 instances
   - **D)** S3 with EC2 instances
   - **Answer**: **C)** Amazon EFS with EC2 instances for shared, scalable storage with multi-instance access.

3. **Scenario**: You’re running a machine learning workload that occasionally requires GPU-based EC2 instances for training, but there are long idle times between training cycles. What instance type and pricing model would you choose to minimize cost without compromising performance? Justify your decision.
   - **A)** On-Demand GPU instances
   - **B)** Spot GPU instances
   - **C)** Reserved GPU instances
   - **D)** General-purpose instances with Auto Scaling
   - **Answer**: **B)** Spot GPU instances for cost savings during idle times with fault-tolerant ML workloads.

4. **Scenario**: You have a large-scale, latency-sensitive application that needs multiple EC2 instances to communicate quickly within the same Availability Zone. Which placement group would you use, and why? What are the potential downsides?
   - **A)** Spread Placement Group
   - **B)** Cluster Placement Group
   - **C)** Partition Placement Group
   - **D)** Multiple ENIs across instances
   - **Answer**: **B)** Cluster Placement Group for low-latency communication within the same AZ. The downside is limited scalability across multiple AZs.

---

### **Storage Questions**

5. **Scenario**: You are running a production database on EC2 with stringent IOPS and durability requirements. Which EBS volume type would you choose, and why? How would you optimize for performance while maintaining cost efficiency?
   - **A)** General Purpose SSD (gp3)
   - **B)** Provisioned IOPS SSD (io2)
   - **C)** Cold HDD (sc1)
   - **D)** Instance Store
   - **Answer**: **B)** Provisioned IOPS SSD (io2) for high IOPS and durability, with cost optimization by right-sizing and performance tuning.

6. **Scenario**: Your company needs to store large volumes of logs that are infrequently accessed but must be retained for compliance. Which EC2 storage solution would you recommend, and how would you manage the cost associated with storing the logs long term?
   - **A)** Instance Store
   - **B)** EFS with Infrequent Access
   - **C)** Cold HDD (sc1) EBS volumes
   - **D)** Amazon S3 Glacier
   - **Answer**: **D)** Amazon S3 Glacier for low-cost, infrequently accessed storage suitable for compliance retention.

7. **Scenario**: A critical application requires low-latency, high-performance storage for temporary data processing. The data does not need to persist when the instance is stopped. Would you choose EBS or Instance Store, and why?
   - **A)** EBS with io2 volumes
   - **B)** General Purpose SSD (gp3) EBS volumes
   - **C)** Instance Store
   - **D)** Amazon S3
   - **Answer**: **C)** Instance Store for low-latency, temporary storage needs that do not require persistence.

8. **Scenario**: You need to create multiple EC2 instances across different regions that use the same base operating system configuration. How would you create an AMI, and how would you ensure that all instances, regardless of region, have the same configuration?
   - **A)** Create an AMI and manually copy it to each region.
   - **B)** Use EC2 Auto Scaling with regional settings.
   - **C)** Create an AMI and copy it across regions via the AMI copy feature.
   - **D)** Create multiple instances in one region and replicate manually.
   - **Answer**: **C)** Create an AMI and copy it across regions using the AMI copy feature to maintain consistency.
