# Ubuntu Unleashed, 2019 Edition

## Chapter 16: System Monitoring Tools

### Console-Based Monitoring

`ps` - report a snapshot of the current processes

`/proc` - file system

[proc documentation](https://docs.kernel.org/filesystems/proc.html)

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