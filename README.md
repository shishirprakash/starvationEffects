# starvationEffects
Here's a c program I use to check for issues with scheduling a program to run reliably.

Compile it like this:
 
[root@node01 untar]# gcc -o starvationEffects starvationEffects.c

[root@node01 untar]#
 
 
Then run it like this:
 
 
[root@node01 untar]# ./starvationEffects 100000 100

100004 events processed in 1.00 seconds, backlog: 5 events, time runnable: 6.12%

100003 events processed in 1.00 seconds, backlog: 5 events, time runnable: 6.12%

100000 events processed in 1.00 seconds, backlog: 5 events, time runnable: 6.12%

100001 events processed in 1.00 seconds, backlog: 5 events, time runnable: 6.08%

 
It should always print fairly consistent output. If there is a delay in scheduling the program to run, it would print a line like this:
 

89684 events processed in 1.20 seconds, backlog: 30163 events, time runnable: 4.52%
 

You'd see a big spike in the backlog and/or see that it didn't print a status for something like 1.2 seconds instead of printing it precisely at 1.00 seconds, or the time runnable could spike a lot of drop a lot.
 

If you see anything like that it would indicate that scheduling is inconsistent. The program is not getting sufficient CPU time to run.
