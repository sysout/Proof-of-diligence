# What I want to achieve?
Be able to navigate and admin the file system, process tree, network in linux system from application's perspective

# Command Line
## history
```
$ cat /proc/loadavg
$ echo $(!cat) # run the last cat command
```
## cp
```bash
$ cp -i /etc/passwd ./passwd # interactive mode
```
## dpkg
```bash
$ dpkg -S $(which ps) 
procps: /bin/ps
$ dpkg -L procps # List files `owned' by package(s).
...
$ dpkg -L procps # Display package status details.
...

```
## uptime
rule of thumb: 
* For a single core values should be less than 1
* For dual core less than 2, etc

uptime commmand reads from:
* /proc/uptime
* /proc/loadavg 
```bash
$ cat /proc/uptime
1628906.51 1623296.05 # uptime in seconds, idle time in seconds
```
## p and k
* pgrep, pkill, killall
* default signal is -15 or -term or -sigterm
* really kill -9 -kill -sigkill
```bash
$ ps -l # long listing, [SZ] is the size in pages
$ getconf PAGESIZE # get the Virtual Memory PAGESIZE
$ getconf PAGE_SIZE # same as above
$ ps -f # full listing
$ ps -ef # all process with full listing
$ sleep 900& # create a process running in the background
$ pgrep sleep # search a process
$ pkill sleep # kill a process matching sleep
$ killall sleep # kill all process matching sleep
```
https://groups.google.com/forum/#!topic/comp.unix.solaris/MyGEtlv62hw

Examine the process with 'pmap -x <PID>' and see which particular mapping (or mappings) is growing.  Of course if it is the heap, then you'll have to do the debugging at the Java or library level to see why the memory is continuing to leak.

[anon] just means that the memory isn't backed by any particular file (it wasn't paged in from disk), and it's not part of the heap or stack. So it's memory that that has been allocated to the process, not directly in the heap.  I see that most multi-threaded proceses tend to have quite a number of anon mappings. I presume this is some sort of thread-local storage for each. 

## top
* kill
* renice
* sort & display
```bash
$ top -n 2 -d 3 # n sample, d duration
```
in top, you can toggle:
* uptime with 'l'
* task with 't'
* memory with 'm'
* show fields management with 'f', choose the sort field with 's'
* renice with 'r'
* kill with 'k'
