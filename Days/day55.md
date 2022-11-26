On the fifty fifth day, I learned the following things about Cloud Computing.

# Elastic Compute Cloud

- Amazon EC2 or virtual machines provides scalable computing capacity in the AWS cloud.

- It enables you to scale up or scale down the instances to handle changes in requirements. You don't need to buy another server. You can just increase or decrease the requirement on the same server.

- You can use Amazon EC2 to launch as many or as few virtual servers as you need, configure it security, and manage the networking and the storage.

- Amazon EC2 is having two storage options i.e EBS and instance store. EBS is kept on the side of the physical server but instance store is present in host memory. Instance store is fast as compare to EBS.

- Preconfigured templates are available known as Amazon Machine Image like microsoft image, ubuntu image, etc. 

- **By default, when you create an EC2 account with amazon, your account is limited to a maximum of 20 EC2 instances per region with two default High I/O instances.**

# Types of EC2 instances

There are seven types of instances.

1. General purpose -> Balanced Memory and CPU
2. Compute Opmtimized -> More CPUs than RAM
3. Memory Opmtimized -> More RAMs
4. Storage Optimized -> Low Latency in which More Storage is Required
5. Accelerated Computing/GPU -> Graphics Optimized
6. High Memory Optimized -> High RAMs, Nitro System(Specialized hypervisor to increase the performance)
7. Previous Version Instances

## 1. General Purpose Instance

- General purpose instances provide a balance of compute, memory and networking resources and can be used for a variety of workloads.

- There are 3 series in a general purpose instance.

    - A Series
        - A1
    - M Series
        - M4
        - M5
        - M5a
        - M5ad
        - M5d
    - T Series
        - T2
            - t2.micro (Free tier eligible)
        - T3
        - T3a

- Instances are available in four sizes.

    - Nano or Micro (contains 1 virtual CPU, approximately 2GB RAM)
    - Small
    - Medium
    - Large (Higher configuration of virtual CPUs and RAM)
    
- A Series contains medium and large sizes.

- M Series contains only large size.

- T Series contains all the sizes from nano to large.

### A Series

- **A1-instances:** are ideally suitable for scale-out workloads(suddenly adding more configurations and managing them) that are supported by the [Arm ecosystem](https://www.arm.com/company/news/2019/04/the-arm-ecosystem-more-than-just-an-ecosystem).

- **Arm ecosystem:** Arm ecosystem provide customers with wide range of products to get market faster than the competition. 

- **Microservice:** It is a distinct method of developing software systems that tries to focus on building single-function modules with well defined interfaces and operations.

- These instances are well-suited for the following applications.

    - WebServer
    - Containerized microservices
    - Caching fleets(Stores the subset of data)
    - Distributed data stores
    - Application that requires Arm instruction set

### M Series

- **M4 instances:** The new M4 instances use a custom Intel Xeon E5-2676 v3 Haswell processor and it is optimized specifically for EC2.

    - vCPU (Virtual CPU) -> 2 to 40 (max)
    - RAM -> 8 GB to 160 GB (max)
    - Instance storage -> EBS only

- **M5, M5a, M5ad and M5d instances:** These instances provide an ideal cloud infrastructure, offering a balance of compute, memory and networking resources for a broad range of applications.

    - It is used in the gaming server, web server, small and medium databases.
    - vCPU -> 2 to 96 (max)
    - RAM -> 8 GB to 384 GB (max)
    - Instance storage -> EBS and NVMe SSD (Nitro system SSD)

### T Series

- **T2, T3, and T3a instances:** These instances provide a baseline of CPU performance from 5% to 40% with the ability to burst to a higher level(may increase above 40% but not necessary) when required by your workload.

    - An unlimited instances can sustain high CPU performance for any period of time whenever required.

    - It is not used for real time scenario. Instead it is used for practicing purpose like:
        - Websites
        - Code repositories
        - Development, build, test
        - Microservices of small applications

    - vCPU -> 2 to 8
    - RAM -> 0.5 GB to 32 GB

## 2. Compute Optimized Instance

- Compute optimized instances are ideal for compute-bound applications(processing several requests at the same time) that benefit from high performance processors.

- It is cheap and cost-effective.

- There are three types of series in it.

    - C3 (It was the previous instance. Updated version is C5)
    - C4
    - C5
    - C5n

- **C4 instances** are optimized for compute intensive workloads and deliver very cost effective high performance at a low price per compute ratio.

    - vCPU -> 2 to 36
    - RAM -> 3.75 to 60 GB
    - Storage -> EBS only
    - Network Bandwidth -> 10 Gbps

- Its usecases are

    - Web server
    - Batch Processing
    - MMO Gaming
    - Video Encoding

- **C5 instances** are optimized for compute intensive workloads and deliver very cost effective high performance at a high price per compute ratio.

- It is powered by AWS Nitro system.

    - vCPU -> 2 t0 72
    - RAM -> 4 to 192 GB
    - Intance storage -> EBS and NVMe SSD
    - Network Bandwidth -> Upto 25 Gbps

- Its usecases are

    - High performance web server
    - Gaming
    - Video Encoding

- **Note:** 

    - C5 supports maximum 25 EBS volume
    - C5 uses Elastics network adapter
    - C5 uses new EC2 hypervisor

## **Explaining it in a video**

Here you can get an explanation in a video. [55/60 Day of DevOps Challenge]()