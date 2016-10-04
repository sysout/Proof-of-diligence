## Command Line
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

```
