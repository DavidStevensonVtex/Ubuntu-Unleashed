# Ubuntu Unleashed, 2019 Edition

## Chapter 14: Automating Tasks and Shell Scripting

### Scheduling Tasks

Three ways to schedule commands:

1. `at` command, which specifies a command run at a specific time and date relativet to today.
1. `batch` command, which is actually a script that redirects you to the at command with some extra options set so your command runs when the system is quiet.
1. `cron` daemon, which is the Linux way of executing tasks at a given time 