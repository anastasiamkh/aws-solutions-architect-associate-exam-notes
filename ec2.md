# **EC2 Fundamentals for AWS Solutions Architect Associate Exam**

### **Overview**
Amazon EC2 (Elastic Compute Cloud) provides scalable compute capacity in the cloud. It allows you to run virtual machines, called **instances**, and scale workloads based on demand.

---

### **Key Features**
- **Instance Types**: Different types optimized for compute, memory, or storage (e.g., General Purpose, Compute Optimized).
- **Elasticity**: Scale instances up or down as needed.
- **Pricing Models**: Includes On-Demand, Reserved, Spot Instances, and Savings Plans.
- **Security**: EC2 instances are secured with **Security Groups** and can use **IAM roles** for access control.
- **Storage**: **Elastic Block Store (EBS)** provides persistent storage for instances.

---

### **Networking**
- **Elastic IPs**: Static, public IP addresses for EC2 instances.
- **VPC**: EC2 instances run within a Virtual Private Cloud (VPC), controlling networking settings.

---

### **Best Practices**
- Use **Auto Scaling** for cost-efficiency.
- Apply **IAM roles** to instances to manage access.
- Regularly monitor instances with **CloudWatch** for performance and logs.

# **EC2 Instance Types**

### **Overview**
Amazon EC2 offers a variety of instance types optimized for different use cases. Each instance type provides varying combinations of CPU, memory, storage, and networking to support specific workloads.

---

### **Categories of EC2 Instance Types**

1. **General Purpose**: Balanced for a wide range of workloads (e.g., T3, M6g).
   - Use cases: web servers, small databases, development environments.

2. **Compute Optimized**: Optimized for high-performance computing (e.g., C6g, C5).
   - Use cases: batch processing, media transcoding, scientific modeling.

3. **Memory Optimized**: High memory-to-CPU ratio for memory-intensive applications (e.g., R5, X1e).
   - Use cases: in-memory databases (e.g., Redis), large-scale caches, real-time big data processing.

4. **Storage Optimized**: High disk throughput and IOPS (e.g., I3, D2).
   - Use cases: large databases, big data processing, data warehousing.

5. **Accelerated Computing**: Hardware accelerators like GPUs or FPGAs for specialized workloads (e.g., P4, G5).
   - Use cases: machine learning, deep learning, gaming, video rendering.

---

### **Key Instance Types**

- **T-Series (Burstable Performance)**: Low-cost instances that provide a baseline level of CPU performance with the ability to burst (e.g., T3, T3a).
- **R-Series (Memory Optimized)**: Large amounts of memory for workloads requiring high memory capacity (e.g., R5, R6g).
- **P-Series (GPU-Optimized)**: Used for high-performance computing (HPC), AI, and machine learning (e.g., P4, G5).

#### **Burstable Instances (General Purpose)**

Burstable instances, such as the T3, T3a, and T4g families, are part of the **General Purpose** category. They are cost-effective for workloads with variable CPU demand that occasionally require high performance.

- **CPU Credits**: Instances accumulate CPU credits during low usage periods.
- **Bursting**: These credits allow instances to temporarily burst to higher CPU performance when needed.


### **Choosing an Instance Type**
- Consider the workload’s CPU, memory, storage, and networking requirements.
- Balance cost with performance based on use cases (e.g., for web applications, general-purpose instances may suffice, while for AI/ML workloads, GPU-based instances are optimal).

# **EC2 Instance Naming Convention**

EC2 instance names follow a structured pattern that conveys important information about the instance type. The format is:

**\<Family>\<Generation>\<Additional Attributes>.\<Size>**

---

### **Naming Breakdown**
1. **Family**: Indicates the instance's use case (e.g., `t`, `m`, `c`, `r`).
   - Example: `t` for burstable, `c` for compute optimized, `r` for memory optimized.

2. **Generation**: The version or release generation of the instance (e.g., `3`, `5`, `6g`).
   - Example: `t3`, `m5`, `c6g`.

3. **Additional Attributes** (optional): Additional features like processor architecture.
   - Example: `g` for ARM-based Graviton instances.

4. **Size**: Denotes the instance size (e.g., `small`, `medium`, `large`, `xlarge`).
   - Example: `t3.medium`, `c6g.xlarge`.

---

### **Examples**
- **t3a.micro**:
  - **t**: Burstable
  - **3a**: 3rd generation, AMD processor
  - **micro**: Smallest size

- **m5.2xlarge**:
  - **m**: General-purpose
  - **5**: 5th generation
  - **2xlarge**: Twice the size of an `xlarge` instance

# **EC2 Pricing Models**

### **1. On-Demand Instances**
- **Overview**: Pay per hour/second with no long-term commitments.
- **Use Cases**: 
  - Testing or development environments.
- **Cost**: No upfront payment, highest hourly rate.

### **2. Reserved Instances**
- **Overview**: Commit to 1- or 3-year terms for discounts.
- **Use Cases**: 
  - Running databases or steady-state applications.
- **Discount**: Up to **75% off** compared to On-Demand.

### **3. Spot Instances**
- **Overview**: Bid on unused capacity at lower prices.
- **Use Cases**: 
  - Batch processing, fault-tolerant jobs.
- **Discount**: Up to **90% off** On-Demand pricing.

### **4. Savings Plans**
- **Overview**: Flexible plans with a 1- or 3-year commitment.
- **Use Cases**: 
  - Consistent workloads.
- **Discount**: Up to **66% off** On-Demand.

### **5. Dedicated Hosts**
- **Overview**: Physical servers for compliance needs.
- **Use Cases**: 
  - Enterprise apps or software requiring specific configurations.
- **Discount**: Pricing varies; higher than Reserved Instances but with hardware control.

### **6. Dedicated Instances**
- **Overview**: Run instances on dedicated hardware but without control over the underlying host.
- **Use Cases**: 
  - Workloads requiring physical isolation from other customers for compliance purposes.
- **Discount**: No upfront commitment, higher costs than shared instances; lower cost than Dedicated Hosts.

# **Difference Between Dedicated Hosts and Dedicated Instances**

- **Dedicated Hosts**:
  - Provides full control over **underlying hardware**.
  - Ideal for **compliance** and **BYOL** (Bring Your Own License) requirements.
  - Higher cost, more customization options.

- **Dedicated Instances**:
  - Instances run on **dedicated hardware** but without control over the physical server.
  - Offers **isolation** from other customers.
  - Cheaper than Dedicated Hosts, but less control over hardware.

### **Key Difference**: 
Dedicated Hosts give hardware control; Dedicated Instances provide isolation but with less customization.


# **Spot Instances**

### **Overview**
Spot Instances allow you to bid on unused AWS capacity, providing access at significantly lower prices (up to **90% off** compared to On-Demand). These instances are ideal for fault-tolerant workloads that can handle interruptions, like batch processing or big data analysis.

---

### **How Spot Instances Work**
1. **Bidding**: You specify a maximum price you're willing to pay, and AWS compares it to the current Spot price.
2. **Launching**: If your bid is higher than the Spot price, AWS launches the instances.
3. **Price Fluctuations**: Spot prices fluctuate based on supply and demand for spare capacity.

---

### **Interruption and Termination**
1. **Interruption Conditions**: Spot Instances can be terminated if:
   - The Spot price exceeds your maximum bid.
   - AWS needs to reclaim the capacity for On-Demand users.
2. **Notification**: AWS provides a **2-minute warning** before termination, allowing applications to shut down gracefully.
3. **Handling Interruption**: To manage potential interruptions:
   - Design your workload to be fault-tolerant.
   - Use AWS services like **Spot Instance interruption notices** and **EC2 Auto Scaling** to handle interruptions.

---

### **Spot Request Types**
1. **One-Time**: Requests a specific number of Spot Instances that terminate once completed.
2. **Persistent**: Keeps Spot Instances running until manually terminated, even if interrupted, ensuring AWS relaunches them when capacity becomes available.

---

### **Use Cases**
- **Batch Processing**: Tasks that can resume from where they left off, like video rendering.
- **Big Data Analytics**: Cost-effective for processing large datasets.
- **Containerized Workloads**: Ideal for scaling tasks in environments like ECS or Kubernetes.
- **CI/CD Pipelines**: Non-critical tasks that tolerate interruptions.

---

### **Spot Fleet**
- **Overview**: A Spot Fleet is a collection of Spot and optional On-Demand instances, managed as a single fleet.
- **Scaling & Cost Optimization**: AWS dynamically provisions the lowest-cost Spot Instances to meet your capacity needs, balancing costs across instance types and availability zones.
- **Capacity Targeting**: Ensures your target capacity is met even when some Spot Instances are interrupted by dynamically adjusting and replacing instances.

---

### **Best Practices**
- **Instance Flexibility**: Use various instance types and availability zones to improve your chances of securing Spot capacity.
- **Auto Scaling**: Use EC2 Auto Scaling groups with Spot Instances for automatic scaling and cost efficiency.
- **Spot Fleet Allocation Strategy**: Use the **lowest-price** or **capacity-optimized** strategy to ensure efficient instance allocation.

# **EC2 Placement Groups**

### **Overview**
Placement groups in EC2 help you control how your instances are deployed across the underlying hardware for optimized performance or redundancy.

---

### **Types of Placement Groups**

1. **Cluster Placement Group**:
   - Instances placed in a single **Availability Zone (AZ)**.
   - Optimized for **low latency** and **high throughput**.
   - **Max instances**: Soft limit of 16; contact AWS for larger clusters.
   - **Use Case**: HPC, data processing.

2. **Partition Placement Group**:
   - Instances spread across partitions, each in separate racks within one or more **AZs**.
   - **Max instances**: Hundreds per partition.
   - **Use Case**: Big data workloads.

3. **Spread Placement Group**:
   - Instances spread across multiple **AZs** to reduce failure risks.
   - **Max instances**: 7 per AZ.
   - **Use Case**: Critical applications with high availability.

# **Elastic Network Interface (ENI)**

### **Overview**
An Elastic Network Interface (ENI) is a virtual network card attached to an EC2 instance, providing network connectivity in a VPC.

---

### **Key Features**
- **Multiple ENIs**: Instances can have multiple ENIs, allowing different network interfaces for management, logging, or public/private subnets.
- **Static IPs**: ENIs can have primary and secondary private IP addresses, along with Elastic IPs.
- **Moveable**: ENIs can be detached from one instance and attached to another.

---

### **Use Cases**
- High availability with multiple network interfaces.
- Network management and monitoring with dedicated ENIs for specific tasks.

An **Elastic Network Interface (ENI)** is tied to a specific **subnet** in a VPC, which represents a single network (public or private). Since each subnet has unique IP ranges and routing rules, one ENI can only operate within one network at a time. To connect to multiple networks (e.g., public and private), you need multiple ENIs, with each ENI assigned to a different subnet, allowing an instance to communicate across different network environments simultaneously.

# **EC2 Hibernate State**

### **Overview**
EC2 Hibernate allows you to preserve the instance's in-memory state (RAM) when it stops, enabling faster startup compared to rebooting.

### **How It Works**
- The RAM data is saved to the instance's root EBS volume.
- When the instance starts again, the RAM is reloaded, and the instance resumes exactly where it left off.

### **Use Cases**
- Long-running processes or applications that need to quickly resume activity.
- Applications with extensive initialization that can benefit from faster restarts.

### **Limitations**
- Only available for certain instance types and AMIs.
- Root EBS volume must be encrypted.
