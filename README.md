Download Link: https://assignmentchef.com/product/solved-cs550-parallel-sort-using-multiple-processes-and-threads
<br>
<h1>Goal</h1>

In this assignment, you will implement a parallel version of the Bubble Sort algorithm to sort a bunch of numbers using first multiple processes and then multiple threads. You will learn about working with multiple processes, concurrency, race conditions, and simple inter-process and inter-thread synchronization.

Requirements for parts A and B below.

<ul>

 <li>Use only the C language and glibc, so that you can understand low-level behavior or your code. No other languages, libraries or packages are necessary/allowed.</li>

 <li>Do not use any pre-existing bubble-sort implementations/libraries other than the ones provided in this assignment.</li>

 <li>Implement only a parallel version of bubble sort, NOT any other sorting algorithm, even though there may be other (possibly better) parallel sorting algorithms, such as parallel merge sort.</li>

 <li>Use the skeleton program named odd_even_sequential_bubble_sort given by me to work on this assignment.</li>

</ul>




<h1>Part A: <u>Parallel</u> Bubble Sort using <u>Processes</u></h1>

Now, implement a parallel version of the even-odd bubble sort using multiple processes.

<ul>

 <li>Besides N, the parallel bubble sort should take an additional argument P, representing the number of concurrent worker processes. For example, for N=100 and P=5,</li>

</ul>

$ multi_process_bubble 100 5

<ul>

 <li>The initial (parent) process creates a shared memory segment in which it stores an array of N random integers.</li>

 <li>Next, the parent process forks P worker processes. After fork, each worker process automatically inherits the attached shared memory segment that was created by the parent. Hence there is no need for child processes to call the shmat() system call.</li>

 <li>Each worker process should execute the parallel bubble sort operation on (about equal sized) overlapping segments of the array, as <u>explained in the slides</u>.</li>

 <li>Each worker should use a barrier (busy looping for now) to coordinate with ”neighboring” workers at the end of each pass.</li>

 <li>You can also store any additional data in the shared memory that’s needed for interworker synchronization.</li>

 <li>The parent prints out the fully sorted array once all worker processes have finished.</li>

 <li>Is your parallel version faster or slower than the sequential version? Time it using gettimeofday(). Think about how to make a fair comparison.</li>

</ul>

<h1>Part B: <u>Parallel</u> Bubble Sort using <u>Threads</u></h1>

Now implement the same parallel version of even-odd bubble sort using POSIX threads (instead

of multiple processes, as in Part B). The logic is the same, except the following

<ul>

 <li>Name your program multi_thread_bubble</li>

 <li>Create multiple threads using pthread_create() instead of multiple processes using fork().</li>

 <li>There’s no need to create shared memory, since the global memory is shared by default among all threads of a process.</li>

</ul>