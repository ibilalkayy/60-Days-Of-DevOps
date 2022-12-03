On the fifty seventh day, I learned the following things about Cloud Computing.

## 5. Accelerated Computing Instances

- Accelerated computing instance families use hardware accelerators or co-processors to perform some functions such as floating point number calculation, graphics processing or data pattern matching more efficiently than it is possible in software running on CPUs.

- This instance is used in AI, ML, and DL. It is also used for live streaming that requires fast processing.

- There are three types of series in it.

    - F series
        - F1
    - P series
        - P2
        - P3
    - G series
        - G2
        - G3

**F series:** 

- F1 instance offers customizable hardware acceleration with Field Programmable Gate Arrays(FPGA). FPGA fastly processes an image and make changes in it.

- Each FPGA contains 2.5 million logic elements(logic gates like AND, NOT gates, etc) and 6800 Digital signal processing(DSP) engines.

- Designed to accelerate computationally intensive algorithms such as data flow or highly parallel operations. Games usually requires parallel processing like button is pressed and action is done live.

- F1 provides local NVM SSD storage.

    - vCPU -> 8 to 64
    - FPGA -> 1 to 8
    - RAM -> 122 to 976 GB
    - Instance storage -> NVMe SSD

- It is used in Genomics research, financial analytics, real time video recording, and big data search.

**P series:** 

- It uses NVIDIA Tesla GPUs

- It provides high bandwidth networking.

- Upto 32GB of memory per GPU which makes them ideal for deep learning and computational fluid dynamics.

- **P2 instance**

    - vCPU -> 4 to 64
    - GPU -> 1 to 16
    - RAM -> 61 to 732 GB
    - GPU RAM -> 12 to 192 GB
    - Network Bandwidth -> 25 Gbps

- **P3 instance**

    - vCPU -> 8 to 96
    - GPU -> 1 to 8
    - RAM -> 61 to 768 GB
    - Storage -> SSD and EBS

- It is used in machine learning, databases, seismic analysis(earthquake study), genomics, molecular modeling(chemistry related), AI, Deep learning.

- **Note:** P3 support CUDA 9 and OpenCL API. P2 supports CUDA 8 and OpenCL 1.2

**G series:**

- It is optimized for graphics intensive applications.

- It is well suited for apps like 3D visualization applications.

- G3 instances use NVIDIA Tesla M60 GPU and provide a cost effective high performance platform for graphic applications.

    - vCPU -> 6 to 64
    - GPU -> 1 to 4
    - RAM -> 30.5 to 488 GB
    - GPU Memory -> 8 to 32 GB
    - Network Performance -> 25 Gbps

- It is used in video creation services, 3D visualization, streaming graphics-intensive application.

## 6. High Memory Instances

- High memory instances are purpose built to run large-in-memory databases, including production development of SAP HANA in the cloud.

- It has only one series that is U-series. U-series has 3 subtypes that U6, U9 and U12.

**Note**

- High memory instances are bare metal instances and do not run on a hypervisor.

- The dedicated host will be provided for running only your server in it.

- The dedicated host is available in purchasing category for 3 years term.

- OS is directly installed on hardware.

**Features**

- Latest generation intel xeon pentium 8176M processor.

- 6, 9, 12 TB of instance memory, the largest of any EC2 instance.

- Powered by the AWS nitro system, a combination of dedicated hardware and lightweight hypervisor.

- Bare metal performance with direct access to host hardware.

- EBS is optimized by default at no additional cost.

- Network performance is 25 Gbps.

- Dedicated EBS bandwidth is 14 Gbps. It will read and write the data from storage fastly.

- Each instance offer 448 logical processor.

## 7. Previous Version Instances

- These are the previous instances that you can still purchase and use them.

- If you bought any one of them previously as a dedicated instance but now they're added to the previous version, the price of these instances won't change. They will be the same

    - T1 
    - M1 
    - C1 
    - CC2 
    - M2 
    - CR1 
    - CG1 
    - i2 
    - HS1 
    - M3 
    - C3 
    - R3

## Important Questions

- **Q.** When the EC2 bill starts and stops or by which mean we have to pay?

    **A.** EC2 instances will start counting the bill if it is booted and it will shut down when you terminate.

- **Q.** If you stop or shutdown the server or instance but didn't terminate, will I have to pay the whole bill?

    **A.** No, but you just have to pay the storage fee of the instance, not the processing fee because the server is not running.

- **Q.** Is the pay per second option available for windows?

    **A.** No, it is currently available for linux servers/instances only. For windows, it is pay per hour.

- **Q.** Will the bill be provided based on seconds usage or minutes or hourly usage?

    **A.** The bill will be provided to you every month and they will be based on the hourly usage. The minutes and seconds will be calculated in those hours.

- **Q.** Does the billing contains the taxes?

    **A.** No, the taxes are excluded from the bills. Only the instance payment is fixed. The taxes depends from country to country.

## **Explaining it in a video**

Here you can get an explanation in a video. [57/60 Day of DevOps Challenge](https://www.youtube.com/watch?v=nUa4XpPx_WA&list=PLptbpfKzsc3BtEki4tHQm5Xmpj8w1_JlM&index=54)