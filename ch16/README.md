# Ubuntu Unleashed, 2019 Edition

## Chapter 16: System Monitoring Tools

### Console-Based Monitoring

`ps` - report a snapshot of the current processes

`/proc` - file system

* [proc documentation](https://docs.kernel.org/filesystems/proc.html)
* [proc documentation](https://tldp.org/LDP/Linux-Filesystem-Hierarchy/html/proc.html)

```
$ ps
    PID TTY          TIME CMD
  61242 pts/0    00:00:00 bash
  61903 pts/0    00:00:00 gedit
  61981 pts/0    00:00:00 ps
```

`ps -e` - lists all processes running on the system

`ps aux | grep bash`

```
$ ps aux | grep bash
dsteven+   61242  0.0  0.0  11252  5660 pts/0    Ss   12:31   0:00 /bin/bash --init-file /usr/share/code/resources/app/out/vs/workbench/contrib/terminal/common/scripts/shellIntegration-bash.sh
dsteven+   62085  0.0  0.0   9492  3344 ?        S    12:40   0:00 /bin/bash /usr/share/code/resources/app/out/vs/base/node/cpuUsage.sh 61242 61903
dsteven+   62092  0.0  0.0   9032   720 pts/0    R+   12:40   0:00 grep --color=auto bash
```

```
$ ps 61903
    PID TTY      STAT   TIME COMMAND
  61903 pts/0    Sl     0:00 gedit
```

```
dstevenson@dstevensonlinux1:~/Ubuntu/Ubuntu-Unleashed/ch15$ kill 61903
dstevenson@dstevensonlinux1:~/Ubuntu/Ubuntu-Unleashed/ch15$ 
[1]+  Terminated              gedit
dstevenson@dstevensonlinux1:~/Ubuntu/Ubuntu-Unleashed/ch15$
```

#### Using the `kill` Command to Control Processes

`$ kill option PID`

`$ kill PID`

Using a signal for `kill` tha cannot be caught (i is the number of the SIGKILL signal):
Using this does not allow a process to shut down gracefully, and shutting down gracefully is usually preferred because it closes things that the process might have been using and ensures that logs are written beforet the process disappears.

`$ kill -9 PID`

Try this first:

`$ kill -1 PID`

This is the signal to "hang up" -- stop -- and then clean up all associated processes as well (1 is the number of the SIGHUP signal).

* kill -15 - Sends a SIGTERM, which is a clean shutdown that flushes data that needs to be written to disk
* kill -1 - Sends a SIGHUP, which cleans up and usually causes the system to restart.
* kill -2 - Sends a SIGINT, which is an interrupt from the keyboard, the equivalent of sending `Ctrl+C`.
* kill -11 - Sends a SIGSEGV, which causes the process to experience a segmentation fault and close.
* kill -9 - Sends a SIGKILL, which should be a last resort because it does not sync any data. Nothing is written to disk - no logging, no debugging, nothing.

`killall gedit` - kills all gedit processes

#### Using Priority Scheduling and Control

Two useful applications are the `nice` and `renice` commands.

`time` - get an idea of how much time abd what proportion of a system's resources are required for a task, such as a shell script.

`sudo time -p find / -name dstevenson`

`htop` - one option for monitoring resource usage is called

#### Displaying Free and Used Memory with `free`

```
$ free
              total        used        free      shared  buff/cache   available
Mem:        8118604     1886204     2799888      267840     3432512     5658892
Swap:       2097148           0     2097148
```

`watch free`

`vmstat 5 10` - Virtual Memory Statistics, run very 10 seconds for 10 iterations

#### Disk Space

`df`

Display disk space used in (M)egabytes or (G)igabytes, etc.

`$ df -h`

#### Disk Quotas

#### Checking Log Files

Most log files can be found in `/var/log/` or its subdirectories.

`sudo tail /var/log/boot.log`

`sudo cat /var/log/dmesg | grep pnp`

Most commonly used log files:

* /var/log/apport.og - system crashes and reports
* /var/log/auth.log - information about system access and when a user uses sudo
* /var/log/boot.log - log during the computer startup
* /var/log/kern.log - kernel messages, such as warnings and errors
* /var/log/syslog - system events
* /var/log/ufw.log - Ubuntu Firewall
* /var/log/apt/history.log

* faillog - reads from /var/log/faillog
* lastlog - reads from /var/log/lastlog

GUI - Logs

#### Rotating Log Files

`logrotate` utility

Ubuntu comes with logrotate installced.

Script at /etc/cron.daily/logrotate

Configuration at /etc/logrotate.conf

### Graphical Process and System Management Tools

Remote: X11 environment variable: $DISPLAY

or use ssh clien't -X option when conneting to the remote host.


#### System Monitor

System Monitor is a graphical monitoring tool that is informative, easy to use and understand and very useful.
#### Conky

[Conky Documentation](https://github.com/brndnmtthws/conky)

#### Other Graphical Process and System-Monitoring tools

* vncviewer - AT&T's remote session manager
* gnome-nettool 
* wireshark

### KDE Process and System Monitoring tools

* kdf - displays free disk space and enables you to mount and unmount file systems
* ksysguard - provides CPU load and memory use in animated graphs
* 