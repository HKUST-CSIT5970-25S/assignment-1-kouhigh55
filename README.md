[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: Li.Cong jiao
### Student Id: 21072745
### Email: cliej@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

    > I used Phoronix Test Suite as my measurement tool.
> For measuring CPU performance, the php-zip function was used to complete pts/compress-7zip task, because compressing and de-compressing is a CPU-intensive task that effectively benchmarks the CPU performance. It ran three times each test, seeking for more stable result. The result contains the average of Million Instructions Per Second for compressing and de-compressing, which is our measurement of CPU performance.

> For measuring Memory performance, the average performance for Integer were test to complete different types of pts/ramspeed task, because it is representative of many real-world workloads, such as database operations, scientific computing. It ran three times each test, seeking for more stable result. The result contains the speed of memory processing on average of copy, scale, add, triad tasks.

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region. Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance (MIPS)   | Memory performance (MB/s) |
    | ----------- |--------------------------|---------------------------|
    | `t2.micro` | 3874(com), 3120(de-com)  | 10760.86                  |
    | `t2.medium`  | 10050(com), 5850(de-com) | 19078.64                  |
    | `c5d.large` | 7503(com), 4868(de-com)  | 13870.12                  |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- |----------------|----------|
    | `t3.medium` - `t3.medium` | 1,034.24           | 0.772    |
    | `m5.large` - `m5.large`   |  5,079.04              | 0.210    |
    | `c5n.large` - `c5n.large` |  5,048.32              | 0.129    |
    | `t3.medium` - `c5n.large` | 1,044.48               | 0.349    |
    | `m5.large` - `c5n.large`  | 3,041.28               | 0.558    |
    | `m5.large` - `t3.medium`  | 1,044.48               | 1.048    |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

2. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- |----------------|----------|
    | N. Virginia - Oregon      | 8,847.36               | 0.313         |
    | N. Virginia - N. Virginia | 33             | 59.486   |
    | Oregon - Oregon           | 5,089.28               | 0.145    |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
