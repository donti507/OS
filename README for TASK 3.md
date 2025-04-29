Task 3 
Investigation of page replacement algorithms. 
Formulate the assumptions of the simulation yourself: 
- Virtual memory size (number of pages),
- Size of physical memory (number of frames),
- Length (should be significant - min. 1000) and how the sequence of page references is 
generated (it is necessary to take into account the principle of locality of references). 
Plan: 
- Generate a random sequence of n page references,
- For the generated sequence provide the number of page faults for different page replacement 
algorithms: 
- FIFO 
- OPT
- LRU
- approximated LRU
- RAND (we remove a random page)





tips ---------


Operating systems – Task 3
General comments:
Task 3 – Paging
Analogous to the previous tasks, I remind you that as important as the implementation of the 
algorithms themselves is the preparation of a simulation environment that will enable us to reliably 
verify the performance of the developed algorithms under various randomly generated test cases. As 
before, it is important to be able to control the simulation parameters.
As part of the preparation of the test environment, you should prepare a data structure representing 
the physical memory (most likely an array) where we will store the current pages. In addition, the total 
number of pages in virtual memory (most likely a single integer) should be defined, which will be used 
to generate the page reference sequence. An important consideration for the generated reference 
sequence is to take into account the principle of locality of references. According to this principle, a 
process only uses a limited subset of all pages in each execution phase, so when generating the 
reference sequence it is important to ensure that the generated sequence is divided into certain 
sections (corresponding to the execution phases of the processes), within which only pages from a 
limited subset of all pages will be drawn.
The parameter to be investigated in the running simulation will be the number of page fault. At the 
same time, I will briefly remind you that a page fault occurs when a process refers to a page that is 
not in physical memory and it is necessary to replace one of the pages in physical memory with a 
page from virtual memory.
As part of your algorithm research, please remember to make assumptions about the simulation 
parameters that are reasonable. As an example, I can give a situation where the physical memory will 
be larger than the total number of pages in virtual memory - by taking a moment to analyze such a 
case, no doubt each of you will find that your study is not necessary to determine the results that will 
be obtained.
When carrying out research on algorithms, I suggest testing different numbers of frames (physical 
memory sizes) starting with a very small number and gradually increasing, so the physical memory 
capacity becomes a larger and larger proportion of the total number of pages in the virtual memory 
defined.
As with previous classes, I remind you that we are interested in a reliable simulation and it is important 
that each algorithm operates on the same sequence of references so that they can be compared. 
As part of the ongoing research, a comparison of 5 algorithms is to be carried out. A brief introduction 
to each is given below, while I refer you to the literature and the lecture material for details of their 
operation.
1) FIFO (First In First Out)
A simple-to-implement page replacement algorithm that uses the assumption that if a page fault
occurs, the page that has been in physical memory the longest should be removed. Note that this 
algorithm does not take into account whether references to individual pages have occurred, it 
simply deletes the page that has been in memory the longest. Therefore, as a practical 
implementation, a counter should be defined for each page held in physical memory to count how 
1
2
long it has been in memory (for simplicity, it can be assumed that one handled reference is one 
unit of time).
Below is an example of how the algorithm works in a system where the physical memory consists 
of 4 frames, for a query string: [1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5]
Time unit 1 2 3 4 5 6 7 8 9 10 11 12
Reference 1 2 3 4 1 2 5 1 2 3 4 5
Frame 1 1 1 1 1 1 1 5 5 5 5 4 4
Frame 2 2 2 2 2 2 2 1 1 1 1 5
Frame 3 3 3 3 3 3 3 2 2 2 2
Frame 4 4 4 4 4 4 4 3 3 3
Page fault x x x x x x x x x x
Page faults: 10
2) OPT (optimal)
It is a reference algorithm that is designed to give the best results. Its principle is based on 
removing pages that will not be used for the longest time. As no reliable method of predicting the 
future has yet been developed, the possibilities of implementing it are limited, but it is 
nevertheless a good benchmark for comparing the performance of other algorithms.
Below is an example of how the algorithm works in a system where the physical memory consists 
of 4 frames, for a query string: [1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5]
Time Unit 1 2 3 4 5 6 7 8 9 10 11 12
Reference 1 2 3 4 1 2 5 1 2 3 4 5
Frame 1 1 1 1 1 1 1 1 1 1 1 4 4
Frame 2 2 2 2 2 2 2 2 2 2 2 2
Frame 3 3 3 3 3 3 3 3 3 3 3
Frame 4 4 4 4 5 5 5 5 5 5
Page fault x x x x x x
Page faults: 6
3) LRU (Least Recently Used)
The LRU algorithm is, in a sense, the inverse of the optimal algorithm in terms of its concept of 
operation. When a page fault occurs, this algorithm removes from physical memory the page that 
has not been used for the longest period of time. In this case, when implementing the algorithm, 
attention must be paid to the need to count how long each page in physical memory has been 
unused. Similar to the FIFO algorithm, it can be assumed that one handled reference is one 
quantum of time.
Below is an example of how the algorithm works in a system where the physical memory consists 
of 4 frames, for a query string: [1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5]
3
Time unit 1 2 3 4 5 6 7 8 9 10 11 12
Reference 1 2 3 4 1 2 5 1 2 3 4 5
Frame 1 1 1 1 1 1 1 1 1 1 1 1 5
Frame 2 2 2 2 2 2 2 2 2 2 2 2
Frame 3 3 3 3 3 5 5 5 5 4 4
Frame 4 4 4 4 4 4 4 3 3 3
Page fault x x x x x x x x
Page faults: 8
4) aproksymowany LRU
Due to the need to keep track of page references, practical implementation of the LRU algorithm 
is not a simple task and requires dedicated hardware solutions for effective operation. For this 
reason, the classic LRU algorithm is most often replaced by algorithms approximating its operation. 
An example of such an approximation would be an algorithm that associates each side with its 
corresponding reference bit. The value of this bit is set to 1 each time a page is referenced, while 
the algorithm selects for replacement one of the pages for which this bit has a value of 0.
An example of an algorithm that approximates the operation of the LRU algorithm is the second￾chance algorithm. The algorithm uses a FIFO queue in its operation. Each successive page that is 
loaded into memory is added to the end of the FIFO queue and its reference bit is set to 1. When 
a page fault occurs, the first candidate for deletion is the page at the beginning of the queue.
If the page at the beginning of the queue has the reference bit set to 0 it is immediately replaced 
by the new referenced page and is removed from the queue, while the new page, as described 
earlier, is inserted at the end of the queue with the reference bit set to 1.
Alternatively, if a page at the beginning of the queue is found to have a cancellation bit set to 1, it 
gets a second chance, according to the name of the algorithm. It is not removed from memory, 
but its reference bit is set to 0, and that page is moved to the end of the queue. The algorithm then 
analyses the next page in the queue (which is now at the beginning of the queue) and, similarly, 
this page gets a second chance if its reference bit is set to 1, but if it is set to 0, it is immediately 
removed from memory and is replaced by a new page.
Below is an example of how the algorithm works in a system where the physical memory consists 
of 4 frames, for a sequence of queries: [1, 2, 3, 4, 1, 2, 5, 1, 2, 3, 4, 5]. In addition, the last line 
shows the contents of the FIFO queue (the first element from the left, is the beginning of the 
queue) and the value of the reference bit (in the lower index) for each page after the processing 
of the incoming reference to the page in physical memory has been completed.
4
Moment 
w czasie 1 2 3 4 5 6 7 8 9 10 11 12
Odwołanie 1 2 3 4 1 2 5 1 2 3 4 5
Ramka 1 1 1 1 1 1 1 5 5 5 5 4 4
Ramka 2 2 2 2 2 2 2 1 1 1 1 5
Ramka 3 3 3 3 3 3 3 2 2 2 2
Ramka 4 4 4 4 4 4 4 3 3 3
Błąd strony x x x x x x x x x x
Kolejka 
FIFO
11 11,21 11,21,31 11,21,31,41 11,21,31,41 11,21,31,41 20,30,40,51 30,40,51,11 40,51,11,21 51,11,21,31 10,20,30,41 20,30,41,51
Page faults: 10
Moment 
w czasie 1 2 3 4 5 6 7 8 9 10 11 12
Odwołanie 1 2 3 4 1 2 5 3 2 1 4 5
Ramka 1 1 1 1 1 1 1 5 5 5 5 5 5
Ramka 2 2 2 2 2 2 2 2 2 2 4 4
Ramka 3 3 3 3 3 3 3 3 3 3 3
Ramka 4 4 4 4 4 4 4 1 1 1
Błąd strony x x x x x x x
Kolejka 
FIFO
11 11,21 11,21,31 11,21,31,41 11,21,31,41 11,21,31,41 20,30,40,51 20,31,40,51 21,31,40,51 51,20,30,11 30,11,50,41 30,11,51,41
Liczba błędów strony: 8
5) RAND (losowy)
As you might expect this is the simplest algorithm to implement. When a page fault occurs, we 
remove a random page from physical memory and replace it with the one that was referenced. 
Due to the non-deterministic nature of this page replacement method, an example of how it works 
has been omitted.
