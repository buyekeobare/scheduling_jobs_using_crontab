# Scheduling Jobs using Crontab

Cron is a system daemon used to execute desired tasks in the background at designated times.
A crontab file is a simple text file containing a list of commands meant to be run at specified times.
It is edited using the crontab command.

Each line in a crontab file has five time-and-date fields, followed by a command, followed by a newline character (\n).
The fields are separated by spaces.

The five time-and-date fields cannot contain spaces and their allowed values are as follows:

| Field   | Allowed Values     |
| ------- | ------------------ |
| minute  | 0-59               |
| hour    | 0-23, 0 = midnight |
| day     | 1-31               |
| month   | 1-12               |
| weekday | 0-6, 0 = Sunday    |

## Objectives

After completing this task, you will be able to:

1. List cron jobs using crontab -l
2. Add cron jobs using crontab -e
3. Remove your current crontab using crontab -r

## Usage

Instructions on how to use the crontab.

### Add a job in the crontab file

#### To add a cron job, run the command below:

1.             crontab -e

- This will create a new crontab file for you (if you don't have one already).
  Now you are ready to add a new cron job.

#### Add the below line at the end of the crontab file:

2.             0 21 * * * echo "Welcome to cron" >> /tmp/echo.txt

- The above job specifies that the echo command should run when the minute is 0 and the hour is 21.
  It effectively means the job runs at 9.00 p.m every day.

- The output of the command should be sent to a file /tmp/echo.txt.

Press Ctrl + x to save the changes.

Press y to confirm.

Press Enter to come out of the editor.

### List cron jobs using crontab -l

#### Check if the job is added to the crontab by running the following command.

3.             crontab -l

You should see the newly added job in the output.

#### Schedule a shell script

Let us create a simple shell script that prints the current time and the current disk usage statistics.

diskusage.sh:

4.             #! /bin/bash

              # print the current date time
              date

              # print the disk free statistics
              df -h

#### Save the file and verify that the script is working:

5.             chmod u+x diskusage.sh
              ./diskusage.sh

- The script should print the current timestamp and the disk usage stats.

#### Let us schedule this script to be run everyday at midnight 12:00 (when the hour is 0 on the 24 hour clock).

We want the output of this script to be appended to /home/project/diskusage.log

Edit the crontab:

6.             crontab -e

#### Add the following line to the end of the file:

7.             0 0 * * * /home/project/diskusage.sh >>/home/project/diskusage.log

#### Check if the job is added to the crontab by running the following command:

8.             crontab -l

### Remove the current crontab

#### Remove your current crontab using crontab -r

The -r option causes the current crontab to be removed.

- Caution: This removes all your cron jobs. Be extra cautious when you use this command on a production server.

9.             crontab -r

#### Verify if your crontab is removed:

10.           crontab -l

### Practice Exercise:

#### Create a cron job that runs the task date >> /tmp/everymin.txt every minute.

1.            crontab -l

2.            * * * * * date >> /tmp/everymin.txt

## License

This project is licensed under the MIT License.
