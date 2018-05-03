# Virtual-disk-driver
A device driver is a program that controls a particular type of device that is attached to your
computer. There are device drivers for printers, displays, CD-ROM readers, diskette drives, and
so on.
Virtual disk and virtual drive are software components that emulate an actual disk storage
device.Virtual disks and virtual drives are common components of virtual machines in hardware
virtualization, but they are also widely used for various purposes unrelated to virtualization, such
as for the creation of logical disks.
In this project we have tried to implement a Driver for Virtual Hard disk in 
i)linux,Ubuntu 16.04.1 
ii) version (can be found  by using command uname -r in terminal): 4.13.0-39-generic (the code might need slight modification if your using other versions)

# Implementation details
A Virtual Hard Disk is created using vmalloc() function. This function allocates the memory in
logical address space. Each location is initialized to 0 using the function memset().
Next we have to tried to develop a device driver for this Virtual Hard Disk.
First we register this Device driver with the kernel along with its major number which is allotted
dynamically.
The second step is to provide the device file operations, through the struct
block_device_operations(prototyped in <linux/blkdev.h>) for the registered major
number device files.
These following things should be provided along with block operations

• The request queue for queuing the read/write requests

• The spin lock associated with the request queue to protect its concurrent access

• The request function to process the requests in the request queue

The request queue contains struct request which has details of direction of transfer , starting
sector of the data transfer , size of the sector and number of sectors.
Each request in the queue maybe either read or write. Read / write is implemented using
memcpy() API.




