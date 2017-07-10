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

## htop
More user friendly than top
```bash
$ sudo apt-get install htop
```
* VIRT stands for the virtual size of a process, which is the sum of memory it is actually using, memory it has mapped into itself (for instance the video card’s RAM for the X server), files on disk that have been mapped into it (most notably shared libraries), and memory shared with other processes. VIRT represents how much memory the program is able to access at the present moment.

* RES stands for the resident size, which is an accurate representation of how much actual physical memory a process is consuming. (This also corresponds directly to the %MEM column.) This will virtually always be less than the VIRT size, since most programs depend on the C library.

* SHR indicates how much of the VIRT size is actually sharable (memory or libraries). In the case of libraries, it does not necessarily mean that the entire library is resident. For example, if a program only uses a few functions in a library, the whole library is mapped and will be counted in VIRT and SHR, but only the parts of the library file containing the functions being used will actually be loaded in and be counted under RES.

## netstat
```bash
# p: PID/Program name
# l: listening
# n: Show numerical addresses instead of trying to determine symbolic host, port or user names
# t: tcp
$ sudo netstat -plnt
```

## vmstat
```bash
# si: swapped in
# so: swapped out
$ vmstat 5 10
procs -----------memory-------------  ---swap---- -----io---- --system--  -----cpu------
r  b    swpd    free   buff  cache       si    so    bi    bo   in    cs us sy  id wa st
2  3   138096   3904    140    584    14829 33632 16684 33633 1353 11562 64  9  16 11  0
7  4   156592   3800    132    492    53570 48618 54264 48622 2762 8148  20  5  50 24  0
2  7   258552   3040    128    668    37910 39822 39766 39826 2763 10861 43  8  23 26  0
7  4   261608   4312    116    776    41696 30854 42171 30855 2771 8631  26  6  33 35  0
3  4   259316   3824    112    576    44616 32316 44697 32320 2746 7087  15  4  52 28  0
0  5   257000   3376    116    880    25895 19847 26622 19848 1673 2877   1  2  68 29  0
4  4   263240   3384    124   1424    30018 21066 30497 21070 1732 4559   9  3  64 24  0
2 14   264656   5740    120   1812    27685 19030 28029 19031 2194 5345  11  3  51 35  0
6  3   338044   3764    132   1568    20087 31066 20470 31070 1798 9847  46  6  33 14  0
2  4   325904   4048    108   1172    13251 7190  13812  7190 1193 8838  38  5  24 32  0
```

## TODO strace

## TODO monit

## TODO systemd

## check who accessed your server
```bash
cat /var/log/auth.log|grep "Accepted publickey"
```


## monitor HTTP traffic
```bash
# httpry doesn't record payload
sudo httpry -i eth0
```
### tcpflow
tcpflow may not decompress gzipped payload. In that case, use chrome requestly extension and delete Accept-Encoding header from the http request.
```bash
# print out to console, work with version 1.4.5 or higher. If you are using ubuntu trusty, try install from source
sudo tcpflow -g -p -FT -C -e http -i eth0 '(port 80 or port 8080) and net 204.204.204.204'
# -g: add color 
# -p: no promiscuous mode
# -FT: The -F option is all about the format of the output files, and the ‘T’ prepends each file name with an ISO-8601 timestamp. If you output to the console using the -c option, it will still prepend all the lines of your conversation with the timestamp to the millisecond even though you’re not creating any files.
# -c: The -c option prints to the console instead of creating individual files. By default, TCP Flow creates two files for each TCP conversation – one file for the packets coming in and one for the packets being transmitted. The -c option can be a useful alternative because the console interleaves the input and output packets.
# -C: Console print without the packet source and destination details
# https://aws.amazon.com/blogs/ses/tag/tcp-flow/ 

# write to disk
sudo tcpflow -i eth0 -e http port 80 or port 8080
# once write to the disk, you can decompress the gzipped file, like
cat 010.010.010.010.00080-204.204.204.204.57543-HTTPBODY | gzip -d
```
### mitmproxy
```bash
# mitmproxy looks like a solid option to check gzipped traffic
```
