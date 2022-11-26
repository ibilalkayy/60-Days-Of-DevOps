On the fifty sixth day, I learned the following things about Cloud Computing.

## 3. Memory Optimized Instance

- Memory optimized instances are designed to deliver fast performance for workloads that process large data sets in memory.

- There are three types of series in it and each of them have subtypes also.

    - R series
        - R4
        - R5
        - R5a
        - R5ad
        - R5d

    - X series
        - X1
        - X1e

    - Z series
        - Z1d

- **R series:** It is used for high performance, ralational(MySQL) and NoSQL(MongoDB, Cassandra) databases.

- Distributed web scale cache stores that provide in-memory caching of key value type data. To process more data in the run time, R series will be used.

- It is used in financial services like Hadoop.

    - vCPU -> 2 to 96
    - RAM -> 16 to 768 GB
    - Instance Storage -> EBS and NVMe SSD

- **X series:** It is well suited for high performance database, memory intensive enterprise applications, relational database workload, and SAP HANA applications.

- It is used in electronic design automation.

    - vCPU -> 4 to 128
    - RAM -> 122 to 3904 GB
    - Instance Storage -> SSD

- **Z series:** Z series delivers a sustained all core frequency upto 4.0 GHz, the fastest of any cloud instances.

- It uses AWS Nitro system, XEON processor and upto 1.8 TB of instances storage.

    - vCPU -> 2 to 48
    - RAM -> 16 to 384 GB
    - Instance Storage -> NVM SSD

- It is used in electronic design, automation and certain databases workloads with high per-core licensing cost.

## 4. Storage optimized instance

- Storage optimized instances are designed for workloads that require high, sequential read and write access to very large data.

- They are optimized to deliver tens of thousands of low latency, random I/O operations per second(IOPS) to application.

- There are three types of series in it.

    - D series
        - D2
    - H series
        - H1
    - I series
        - I3
        - I3en

- **D series:** It is well suited for massive parallel processing (MPP) in data warehouse, map reduce, hadoop distributed computing, and log or data processing app.

    - vCPU -> 4 to 36
    - RAM -> 30.5 to 244 GB
    - Instance Storage -> SSD

- **H series:** This series will provide you upto 16TB of HDD based local storage, high disk throughput(result) and balance of compute and memory of storage.

- Well suited for app requiring sequential access to large amounts of data on direct-attached instance storage.

- There is another storage that is network-attached storage that will be accessible through a network, not directly accessible. EBS is the network-attached storage.

- Application that requires high throughput access to large quantities of data.

    - vCPU -> 8 to 64
    - RAM -> 32 to 256 GB
    - Instance Storage -> HDD

- **I series:** It is well suited for High frequency online transaction processing system(OTPS).

- It is used in relational databases.
    
    - NoSQL databases
    - Distributed file system
    - Data warehousing application

- Spaces used in

    - vCPU -> 2 to 96
    - RAM -> 16 to 768 GB
    - Instance Storage -> NVMe SSD
    - Network Performance -> 25 Gbps to 100 Gbps

- Sequential throughput

    - Read -> 16 GB/s
    - Write -> 64 GB/s (I3)
               8 GB/s (I3en)

## **Explaining it in a video**

Here you can get an explanation in a video. [56/60 Day of DevOps Challenge]()