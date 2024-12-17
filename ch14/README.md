# Ubuntu Unleashed, 2019 Edition

## Chapter 14: Automating Tasks and Shell Scripting

### Scheduling Tasks

Three ways to schedule commands:

1. `at` command, which specifies a command run at a specific time and date relativet to today.
1. `batch` command, which is actually a script that redirects you to the at command with some extra options set so your command runs when the system is quiet.
1. `cron` daemon, which is the Linux way of executing tasks at a given time 

#### Using `at` and `batch` to Schedule Tasks for Later

If you want to run a time-intensive task, but you do not want to do it while you are logged in, you can 
tell Ubuntu to run it later with the `at` command, which you must install.

To use `at`, you need to tell itthe time at which you want the task to run and then press Enter.

Run at just after 8:00 pm

```
at now + 7 hours
wget http://www.kernel.org/pub/linux/kernel/v3.0/linux-3.0.tar.bz2
tar xvfjp linux-3.0.tar.bz2
<EOT>
```

You can use the `-f` parameter to have `at` read its commands from a file, like this:

```
echo wget http://www.kernel.org/pub/linux/kernel/v3.0/linux-3.0.tar.bz2 \;
tar xvfjp linux-3.0.tar.bz2> myjob.job
at -f myjob.job tomorrow
```

* You can specify the number of minutes, hours, days or weeks relative to the current time.
* You can also specify several special times, including *tomorrow*, *midnight*, *noon*, or *teatime* (4 pm).
* You can specify an exact date and time using *HH:MM MM/DD/YY* format.

When you schedule a job using `at`, it is placed into queue "a" by default, which means it runs at your specified time and takes up normal amount of resources.

`batch` is really just a shell script that calls `at` with a few extra options.

* -q b - run job on queue b
* -m - mail the user on completion
* run immediately (now)

Jobs on queue b will only be executed when system load falls below 0.8 - thatis, when the system is not running at full load.

Queue jobs normally have a niceness of 2, whereas b queue jobs have a niceness of 4.
Queue c runs at a niceness 6, queue d runs at niceness 8, and so on.

When you submit a job for execution, you are also returned a job number.

If you want to see a list of other jobs you have scheduled to run later, use the `atq` command with no parameters.

If you want to delete a job, use the `atrm` command followed by the ID number of the job you want to delete.

The default configuration for `at` and `batch` is to allow everyone to use it, which is not always the desired behavior. Access is controlled through two files: `/etc/at.allow` and `/etc/at.deny`.

The `at.allow` file does not exist by default. If you have a blank `at.allow` file, no one except root is allowed to schedule jobs.

