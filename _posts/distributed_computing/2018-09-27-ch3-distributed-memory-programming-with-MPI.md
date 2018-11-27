---
layout: post
title: ch3 distributed memory programming with MPI
categories: distributed_computing
---
Both distributed memory system and shared memory system have to handle multiple processor. 
Distributed memory system will have more work on load balancing to make sure the jobs are distributed evenly on processors.
Commonly, multiple processors are identified by integer ranks.

### MPI program
MPI, or as message passing interface is one way to communicate with other processors.
Sender request the message and reciever response the requsest. 
Basically mpi programs are run through the network commutication using sockets. 
MPI package is well written in c for the users.

> mpicc -g -Wall -o mpi_hello mpi_hello.c
> mpiexec -n <number of processes> <executable>

Master processor(=main) collects the response from slave processors(=child) and presents to stdout or stderr.
Standard input is available only at master processor in master-slave system. 
Responses could be presented in ascendent order with loop but commonly messages are printed in arrival order. 
If not, other processors might wait until the current rank arrives. 

#### Communicators
A collection of processors to exchange messages. MPI_Init defines communicator for processes that could be used.
**MPI_COMM_WORLD**. Only processes in same communicators could exchange the messages.

#### methods
{% highlight c %}
# include <stdio.h>

MPI_INIT();  // setup

MPI_Comm_Size();

MPI_Comm_rank();

MPI_Send(..tag..);  //tag : type of msg

MPI_Recv(..MPI_Status..); // status : integrity of msg

MPI_Reduce();

MPI_Finalize(); // after work terminates, cleans up the allocated resources

{% endhighlight %}
Sender could send message only to processors in typical communicator with identical tag. 
Reciever checks whether the message integrity by using **MPI_Status** field, containing the source(=sender), tag or the error. 
They could recieve from anonymous sender but could still check the status as a length of message. 
<br>
Before the sender and reciever setups communication they have to set exact definition by MPI iplementation or else it will be hard to 
find out from multiple os. 
In standard, MPI_Recv always blocks until the message arrives (Block communication). 
