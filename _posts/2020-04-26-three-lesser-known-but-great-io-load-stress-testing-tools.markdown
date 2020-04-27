---
layout: posts
title:  "Three Lessor Known But Great IO Load/Stress Testing Tools"
date:   2020-04-26 20:52:00 -0700
categories: qa
---
I have not used a whole lot of load testing tools, but there are some that really stood out to me, largely used among my colleagues that have proven to be great. Today I would like to introduce 3 of them that are fairly easy to use, provide a good number of options for testers to customize as they want, and provide detailed reports. 

A little bit of background… I used to do software testing on data storage, which requires the system to endure large amounts of I/O within an extended period of time. The focus is a little different from web or mobile/desktop applications, where we care more about the IOPS, bandwidth of the system as a whole, rather than an application. Despite the difference, the concept is still transferable, and I hope these tools can be made a good use in your testing environment as well.

## FIO(Flexible IO)

*GitHub repo [here](https://github.com/ColinIanKing/stress-ng)*

This is one of the mostly used tools throughout my career. FIO is a I/O tester that spawns a custom number of threads to perform tailored workload to the system. It supports both command-line and profile input: the command-line input is for one-time use, and it is suitable for short and quick workload tests; the profile allows users to add more extensive parameters and complex configuration, it can be saved to a file for share and repeated use. 

For data storage testing, one scenario is to configure the storage system and export some space (we call it LUNs) to a Linux or Windows host, then use FIO to run workload on the space (which would be seen as raw disks on Linux or data block on Windows). Some common parameters are: number of threads, IO engine, IO pattern, block size, IO size, runtime. There are many more parameters for advanced users, they can be referred to in the [documentation](https://fio.readthedocs.io/en/latest/). 

FIO is very powerful in that it gives control to the users to decide how they want the workload to look like. When used in the right way, it can even dig out some operating system bugs! However, FIO could be a little intimidating to beginners. It does not have any friendly graphic interfaces, and it requires some basic knowledge in how data read/write works to design a good IO profile.

A simple FIO profile would look like this:

{% highlight bash %}
[global]
ioengine=libaio
bs=4k
direct=1
rw=randwrite
verify=crc32c
iodepth=16

[thread1]
filename=/dev/sdb
{% endhighlight %}

This is a basic IO profile running on a Linux system, with the block /dev/sdb setup in advance. The first line “global” indicates all parameters below are global parameters that will be applied to all threads. Each thread can have its own parameters, marked as “thread-name”. 

Parameter “ioengine” allows users to indicate which IO engine to use, in this case it is libaio, a Linux-based asynchronous IO engine. Note that the selected IO engine needs to be installed before being used in FIO. “bs” is short for block size; “rw” is short for “readwrite”, besides randwrite, there are other combinations such as randread, readwrite, trimwrite, etc., up to 9 options; “verify” indicates a verify pattern, it can also be a literal pattern, but that would expect the same pattern being written as well. 

*Use cases: disk benchmarking, storage benchmarking, OS testing*

## Stress-NG

*GitHub repo [here](https://github.com/ColinIanKing/stress-ng)*

As the name indicates, stress-ng is a small yet powerful tool for CPU and memory stress testing. Stress-NG lets users configure exact operations for the CPU and memory to keep them occupied at a certain level. Just like FIO, there is no GUI in Stress-NG, and it also supports both command-line and profile approach for parameter configurations.

We used stress-ng to stress the CPU and memory of the data storage, and run workloads articulated with FIO. The learning curve of stress-ng is much smoother than FIO. While there are parameters for advanced tailoring, users can easily get it started with a few basic settings. One nice thing is that it supports stress percentage, for example, users can set 75% of CPU being occupied and 50% of memory in use. 

Another bonus about this tool is that the author is super responsive and willing to take suggestions. There were some functionalities that we wished to have, and he quickly responded to our emails, uploaded the new version based on our requests in two days. 

Here is an example of a stress-ng job file.

{% highlight bash %}
run sequential

verbose

metrics-brief

cpu 0  
cpu-load 85% 
cpu-method all
timeout 60s
{% endhighlight %}

The purpose is very simple, it runs only one stressor (can be seen as a test or task), which is to stress the CPU to 85%, sequentially using all methods, and the test will be run for 60 seconds. 

Note that the author has cautioned users not to use this tool for benchmarking, it can only be used for a rough stress testing. If you need to do performance testing, this is probably not the right tool to go for.

*Use cases: CPU stress testing, memory stress testing, CPU profiling*

## HammerDB

*Official Website [here](https://hammerdb.com)*

HammerDB covers a completely different spectrum of testing than FIO and StressNG, it is majorly used for database testing, or web testing if configured right. How did we cross paths with HammerDB though? Well, we used it as a real-world workload generator for data storage testing, which is probably not expected by the HammerDB team. 

HammerDB supports a variety of most commonly used databases, including Oracle, SQL Server, MySQL, PostgresSQL and Redis. It comes with a GUI as well as command-line support, which is good for both manual and automated testing. 

![screenshot of hammerdb user interface!](/assets/images/hammerdb-screenshot.png "Souce: https://hammerdb.com/docs/ch02s01.html")

The usage is pretty straightforward: first, make sure the environment is set up with the target database; second, open HammerDB, and create a schema to populate the database, it supports a customized number of users as well as entry size; third, start the workload by specifying a load drive script.

HammerDB includes a set of load drive scripts that simulate real-world database use cases. The scripts follow the [TPC benchmarks](http://www.tpc.org/information/benchmarks.asp) where two of the popular ones are TPCC and TPCH. TPCC simulates an e-commercial database system by performing a series of actions such as creating new orders, making payments, checking order status, etc.; TPCH simulates a decision support system where users perform a lot of concurrent queries and data modifications. Simply put, TPCC involves a mix of reads and writes, while TPCH is heavily on reads and a moderate amount of writes. 

Note that TPCC, TPCH and all other TPC benchmarks are not exclusive to HammerDB, they are independent standards for database benchmarking, anyone can implement them by following the instructions. The TPC website also provides sample implementations for [download](http://www.tpc.org/tpc_documents_current_versions/current_specifications.asp).

While we didn’t get to use HammerDB for its most common purposes, the experience was overall positive. It is easy to set up, provides enough parameters for tuning, the report is clear and concise. Besides built-in TPC implementations, HammerDB also allows users to customize drive scripts using Tcl, for example, one can write an HTTP requests script for web testing. 

*Use cases: database testing, web testing, customer scenario simulation*

The 3 tools introduced above, besides their benefits, are all still under active development and maintenance. While the sharing stops here, my journey continues. There are many more tools out there yet to be discovered that provide great support to exploit and analyze software. 

