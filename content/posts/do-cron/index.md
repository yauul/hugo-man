---
title: "How to Schedule Tasks in Linux Using Crontab "
description: "This is a demo of adding content to the homepage."
date: 2019-03-10
tags: ["automation", "linux"]
series: ["Linux Admin"]
categories: ["TRU ADMIN"]
series_order: 1
---

## Introduction

{{< article link="/posts/linux-journey/pi-hole/" >}}


So you’re tasked to perform routine backup or periodic system updates on a Linux system. You have the script/commands ready but you're are facing difficulties on how to schedule and automate the tasks. I got you! We will be using the cron utility to get the job done.

In this article, I’ll be briefly explaining the concepts around cron, its uses, syntax, and finish up with a couple of real-world examples to put it all together.

## Concepts

Let’s get a few terminologies out of the way before we check out the syntax.

-   **Cron**: is a UNIX/Linux utility that uses the cron daemon, or _crond_, for scheduling repeating tasks at specific intervals. A daemon is simply a system-managed process running silently in the background.
-   **Cron job**: the individual task that is defined by the user. Each cron job is made up of 6 fields. More on this in the next section.
-   **Crontab**: is a UNIX/Linux command that allows you to list, edit and delete your cron job entries which is then stored in a crontab file.

> The word 'cron' is derived from the Greek word _'chronos'_, which translates to time. **#TheMoreYouKnow**

## Crontab Commands
![alt text](feature.jpg "That pic")
Here are the basic crontab configuration commands that you need to know.

### Listing

To list the content of your crontab file, issue the command below.

```bash
crontab -l
```

This will list the cron jobs of your user’s crontab. It’s important to know that every user has their own crontab file. This way each user can schedule their individual tasks. A user's crontab file is stored in /var/spool/cron/**username**.

You can modify another user’s crontab configuration as well, however you’ll need to have root privileges to do so. To list the root user's crontab file, we can use the command below.

```bash
sudo crontab -u root -l
```

### Editing

We can create or edit a crontab file by entering the following command:

```bash
crontab -e
```

To edit your crontab, you’ll need a text editor like vi or nano installed on your system. You’ll be prompted to choose a text editor when you run the command above for the first time.

### Deleting

You can delete all of your entries in your crontab file by using the command:

```bash
crontab -r
```

## Cron job Syntax

To define our scheduled tasks, we have to understand the syntax of a cron job.

A cron job consists of 6 fields as shown below. Let’s explain each.

![Crontab Image](/images/post-images/do-the-cron/cron-job-command.jpg)

The syntax for a cron job is shown above. There are a total of 6 fields. The first 5 fields defines the schedule and the 6th field is where you write the command you want to execute.

An asterisk (\*) means that the command will run at every interval with respect to the field. In the example above, the command is scheduled to run at every minute, of every hour on every day of the month, on every month and on every day of the week.

Let’s have a quick look on these fields.

1. **Minute**: defines the minute field that the job should run on. Acceptable input is between 0 - 59.
2. **Hour**: defines the hour interval of the job. Acceptable input is between 0 - 23. This is in 24 hour format. So if you want to schedule a job for midnight, you’d type 0.
3. **Day of the Month**: defines the day of the month of the job. Acceptable input is between 1 - 31.
4. **Month**: if you want to schedule a job at a specific month of the year. Acceptable inputs are 1 - 12. You can write a shortened 3-character month format like Jan, Feb, Mar, etc instead of numbers.
5. **Day of the Week**: if you want to schedule a job at a specific day of the week. Acceptable inputs are 0 - 6, 0 being Sunday and 6 being Saturday. 7 is also considered a Sunday, although it’s not standard. Similarly, you can also write a shortened 3-character day format like Sun, Mon, Tue, etc.
6. **Command**: the command or script you want to execute. This could be a script you made or Linux commands.
   Use absolute paths to the location of the scripts or command. For example, `/usr/bin/echo hello{:bash}`.

There are special predefined definitions you can use when writing your cron jobs.

| Definition        | Syntax             |
| ----------------- | ------------------ |
| `@hourly{:bash}`  | `0 * * * *{:bash}` |
| `@daily{:bash}`   | `0 0 * * *{:bash}` |
| `@weekly{:bash}`  | `0 0 * * 0{:bash}` |
| `@monthly{:bash}` | `0 0 1 * *{:bash}` |
| `@yearly{:bash}`  | `0 0 1 1 *{:bash}` |

Below is an example of how to the hourly command.

```bash
@hourly /path/to/script
```

### Ranges

We can use a range of numbers separated by a hyphen to define cron jobs. It will run in between every number of that range.

```bash
0 9-12 * * * ping 8.8.8.8
```

In the example above, the ping command will run every day at 9 AM, 10 AM, 11 AM and 12 PM.

### Lists

A list is a comma-separated sequence of values that specifies multiple options for a field. The command below will run the shift_report script at 7 AM, 3 PM and 11 PM everyday.

```bash
0 7,15,23 * * /opt/script/shift_report.py
```

### Step

A step is used to specify a range of values with a certain increment. For example, \*/20 in the minute field would mean that the command should run every 20 minutes starting from 0 minute.

```bash
*/20 * * * * /home/yoel/backup_logs.sh
```

### Examples

1. Run a backup job from Monday to Friday at 11 PM.
    ```bash
    0 23 * * 1-5 /opt/scripts/backup.sh
    ```
2. Weekly system updates
    ```bash
    @weekly sudo apt update && sudo apt upgrade -y
    ```
3. System health checks to after 5:30 PM every day.
    ```bash
    30 17 * * * /opt/scripts/health_check.py
    ```
4. Copy log files every 3 days at midnight.
    ```bash
    0 0 */3 * * cp /var/log/application/* /opt/archive/
    ```

## Conclusion

Cron jobs are an important tool to know if you're serious about using Linux. Whether you're a Linux system admin, web developer, or even in pentesting, it will definitely help you in automating & scheduling your repetitive tasks.

It may look intimidating at first, but you’ll definitely have a better grasp of the concepts once you apply them yourself. You don’t necessarily have to create a complex command to use crontab. Even a simple redirecting standard output to a text file can help.
