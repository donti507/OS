# OS
Task 2 
Simulation of HDD scheduling algorithms. 
- Disk is in our case a linearly ordered sequence of blocks numbered from 1 to MAX,
- The criterion for evaluating the algorithms will be the sum of disk head movements, as it is 
known, proportional to the execution time of the jobs, 
- Check the FCFS, SSTF, SCAN and C-SCAN algorithms,
- Then assume that there are also real-time applications in the system that need to be served 
by EDF and/or FD-SCAN. How does this affect the results? 
Tips:
It is up to you to formulate the simulation conditions not mentioned above. It means: 
- The size of the disk (number of blocks),
- Number and generation of requests (full queue from the beginning? submissions in progress? 
distribution of requests - even, different?),
- Real-time requests handling,
- Ability to justify the solution adopted would be appreciated




}}}}
Operating systems – task 2
Task 2 – disk scheduling simulation
According to the task assumptions, a disk is a linearly ordered sequence of blocks. As part of the task 
assumptions, I propose that the size of disk is configurable by specifying an appropriate parameter 
when starting the simulation.
As part of the task, I also point out that during the simulation, the algorithms will be evaluated by 
determining the sum of the head movements (for simplicity, we can omit the sector read time for the 
purpose of handling the request). Therefore, in practice, it will be convenient if, when considering real￾time applications, you assume that one unit of time corresponds to moving the head by one disk 
cylinder. In practice, this will mean that if we have a request deadline defined as 72, we are only able 
to fulfil the request if the distance of the requested cylinder on the disk from the head is less than or 
equal to 72.
An important element that should be implemented is the possibility to parameterise the simulation. 
Therefore, parameters such as disk size, number of real-time requests (in scenarios suitable for this) 
or their distribution should be possible to define at least in a restricted range. I would also like to 
remind you that in this class we focus on the simulation of the performance of the algorithms and not 
on the implementation itself, and therefore the collection of statistics (in particular the evaluation 
criterion of the algorithms) from the performance of the algorithms is as important as their 
implementation. Therefore, it is also important that each of the algorithms operates on the same 
sequence of requests, in order to be able to compare them.
Regarding the algorithms themselves, 4 basic algorithms and 2 strategies for handling real-time 
requests have been defined in the task and should be implemented in the simulation. These are briefly 
discussed below, while I refer you to the literature and the lecture material for details.
1) FCFS (First Come First Serve)
This is the simplest disk scheduling algorithm, but it is also a fair algorithm. Disk read requests are 
processed in order of arrival. In order to handle the requests, they are queued in order of arrival, 
and the requests that are at the beginning of the queue are selected for handling in turn.
Below is an image that visualises how this algorithm works. At the moment under analysis, the disk 
head is above cylinder 53 and the request queue is as follows: [98,183,37,122,14,124,65,67] (and 
no new requests are arriving). The sum of moved cylinders for this algorithm in this case is: 640.
1
2) SSTF (Shortest Seek Time First)
The algorithm attempts to minimise head movement by first handling the requests that are closest 
to the current head position. In practice, this means that each successive request arriving at the 
system is added to a queue, and the queue is then sorted in ascending order of the distance of 
each request from the current head position.
Below is an image that visualizes how this algorithm works. At the moment under analysis, the disk 
head is above cylinder 53 and the request queue is as follows: [98,183,37,122,14,124,65,67] (and 
no new requests are arriving). The sum of moved cylinders for this algorithm in this case is: 236.
3) SCAN
In the SCAN method, the disk arm starts from one edge of the disk and moves towards the opposite 
edge, handling orders from the queue along the way. When it reaches the edge of the disk, the 
direction of the head movement changes. In practice, this means that the head continually 
searches (scans) the disk back and forth. This means that when it reaches any of the edges of the 
disk, the requests in the queue to be served are sorted according to the direction in which the 
head will be moving, and if there are new requests that are ‘ahead’ of the head it is inserted into 
the appropriate place in the queue.
2
Below is an image that visualises how this algorithm works. At the moment under analysis, the disk 
head is above cylinder 53 and the request queue is as follows: [98,183,37,122,14,124,65,67] (and 
no new requests are arriving). The sum of scrolled cylinders for this algorithm in this case is: 236.
4) C-SCAN
The C-SCAN algorithm is a variant of the SCAN algorithm. The algorithm works in a similar way to 
the SCAN method with the difference that when the head reaches the edge position, it 
immediately returns to the opposite position (without handling orders along the way).
Below is an image that visualises how this algorithm works. At the moment under analysis, the disk 
head is above cylinder 53 and the request queue is as follows: [98,183,37,122,14,124,65,67] (and 
no new requests are arriving). The sum of the scrolled cylinders for this algorithm in thiscase is: 
183.
And in addition, a brief discussion of two request handling strategies for real-time applications:
5) EDF (Earliest Deadline First)
The EDF algorithm works in a manner analogous to the SSTF algorithm, except that instead of 
selecting the closest request for execution, it greedily selects the request with the shortest 
deadline for execution and heads directly to the cylinder where the requested sector is 
located. Once all such requests have been served, the disk handling system switches to the 
selected standard request handling algorithm until the next real-time request arrives.
3
6) FD-SCAN (Feasible Deadline SCAN)
The FD-SCAN algorithm works in a slightly less ‘mindless’ way than the EDF algorithm. In the 
case of this algorithm, requests with the shortest feasible deadline (hence the ‘feasible’ in the 
name) are executed first. Requests with a deadline shorter than the time it takes to reach them 
are simply rejected by the algorithm. In addition, as the head moves, all requests (normal and 
real-time) that are along the way are executed (hence the ‘SCAN’ in the name). 
It is worth mentioning that the inclusion of a real-time strategy in the simulation requires extending 
the structure describing the request with a flag indicating type of requestand a field describing the 
deadline for the execution of this request.
I case of problems I once again refer to the recommended literature and invite you to contact me.
Images source:
http://www.issi.uz.zgora.pl/pl/didactic/kp/so/wyk7.pdf
4
