---
layout: post
title: How to use CRON Jobs?
---
Lately, I had to integrate data in my systems and I don’t want to have my jobs running every 10 minutes if I receive these data once a week or a day. And as I am working on AWS servers I created CRON Jobs.

### For people who don’t know what is a Cron Job let’s explain what it is.


In Linux, you can configure tasks to run automatically within a specified period of time, on a specified date, or when the system load average is below a specified number.

Cron is a daemon thread that can be used to schedule the execution of recurring tasks according to a combination of the time, day of the month, month, day of the week, and week.

For that, you need to have your system on continuously.


You need to have your crond

Depending on which Linux distro you're using you could either do these commands:

* **redhat distros**

$ sudo /etc/init.d/crond stop

$ sudo /etc/init.d/crond start

Or do these commands:

* **Debian/Ubuntu distros**

$ sudo service cron stop

$ sudo service cron start


Your crontab file configuration of your Cron Job

It is placed here : _/etc/crontab_

You should find something close to that in your file :

```shell
SHELL=/bin/bash

PATH=/sbin:/bin:/usr/sbin:/usr/bin

MAILTO=root

HOME=/

# run-parts

01 * * * * root run-parts /etc/cron.hourly

02 4 * * * root run-parts /etc/cron.daily

22 4 * * 0 root run-parts /etc/cron.weekly

42 4 1 * * root run-parts /etc/cron.monthly
```

Now you have to schedule your Job


Linux crontab have six fields. 1-5 fields denotes time and 6’th fields are used for command/script.

**[Minute] [hour] [Day_of_the_Month] [Month_of_the_Year] [Day_of_the_Week] [command/script]**

### How to List Crontab ?

To view crontab entries of current user use following command.

**crontab –l**

To view crontab entries of other user use following command.

**crontab –u YourUsername –l**

_Useful Crontab Examples for your Cron Job:_

Schedule a cron to execute at 2am daily.
This will be useful for scheduling database backup on daily basis at 2 o’clock.

```0 2 * * * /bin/sh backup.sh```

Schedule a cron to execute twice a day.
Below example command will execute at 5AM and 5PM daily. You can specify multiple time stamp by comma separated.

```0 5,17 * * * /scripts/script.sh```

Schedule a CRON to execute on every minute.
Generally, we don’t require any script to execute on every minute but in some case, you may need to configure it.

```* * * * * /scripts/script.sh```

Schedule a CRON to execute on every Sunday at 5 PM.
This type of CRON are useful for doing weekly tasks, like log rotation etc.

```0 17 * * sun /scripts/script.sh```

Schedule a CRON to execute on every X minutes.
If you want to run your script on X minutes interval, can configure like below. These type of CRONs are useful for monitoring.

```*/X * * * * /scripts/monitor.sh```

*/X: means to on each X minutes. Same as if you want to execute on every 5 minutes use */5.



Schedule a CRON to execute on selected months.
Sometimes we required to schedule a task to be executed for selected months only. Below example script will run in January, May and August months.

```* * * jan,may,aug * /script/script.sh```

Schedule a CRON to execute on selected days.
If you required to schedule a task to be executed for selected days only. Below example will run on each Sunday and Friday at 5PM .

```0 17 * * sun,fri /script/script.sh```


Schedule a CRON to execute on first Monday of every month at 2 AM.
To schedule a script to execute a script on first sunday only is not possible by time parameter, But we can use condition in command fields to do it.

```0 2 * * mon [ $(date +\%d) -le 07 ] && /script/script.sh```


Schedule a CO to execute on every X hours.
If you want to run script on X hours interval. It can be configure like below.

```0 */X * * * /scripts/script.sh```


Schedule a CRON to execute twice on every Sunday and Monday.
To schedule a task to execute twice on Sunday and Monday only. Uthe se following settings to do it.

```0 5,17 * * sun,mon /scripts/script.sh```

Schedule a CRON to execute on every 30 Seconds.
To schedule a task to execute on every 30 seconds is not possible by time parameters, But it can be done by schedule same cron twice like below.

```* * * * * /scripts/script.sh * * * * * sleep 30; /scripts/script.sh```

Schedule multiple tasks in single CRON.
To configure multiple tasks with a single CRON, Can be done by separating tasks by a semicolon ( ; ).

```* * * * * /scripts/script.sh; /scripts/scrit2.sh```

Schedule a task to execute on yearly ( @yearly ).
@yearly timestamp is similar to “0 0 1 1 *”. It will execute the task on the first minute of every year, It may be useful to send new year greetings

```@yearly /scripts/script.sh```

Schedule a task to execute on monthly ( @monthly ).
@monthly timestamp is similar to “0 0 1 * *”. It will execute a task on the first minute of month. It may be useful to do monthly tasks like pay the bills and invoicing to customers.

```@monthly /scripts/script.sh```

Schedule a task to execute on Weekly ( @weekly ).
@weekly timestamp is similar to “0 0 1 * *”. It will execute a task on the first minute of the month. It may be useful to do weekly tasks like the cleanup of system etc.

```@weekly /bin/script.sh```

Schedule a task to execute on daily ( @daily ).
@daily timestamp is similar to “0 0 * * *”. It will execute a task on the first minute of every day, It may be useful to do daily tasks.

```@daily /scripts/script.sh```

Schedule a task to execute hourly ( @hourly ).
@hourly timestamp is similar to “0 * * * *”. It will execute a task in the first minute of every hour, It may be useful to do hourly tasks.

```@hourly /scripts/script.sh```

Schedule tasks to execute on system reboot ( @reboot ).
@reboot is useful for those tasks which you want to run on your system startup. It will be the same as system startup scripts. It is useful for starting tasks in background automatically.

```@reboot /scripts/script.sh```

Enjoy :)