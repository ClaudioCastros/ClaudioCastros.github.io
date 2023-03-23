Delete Files Older Than x Hours on Linux
Delete File

It is very important to find and cleanup your old files which are no longer necessary after a certain period of time. Here is a quick way to do that. This brief tutorial walk you through how to find and delete files older than X days in Linux and Unix-like operating systems. Commands

find /path/to/files* -mtime +5 -exec rm {} \;
The first argument is the path to the files. This can be a path, a directory, or a wildcard as in the example above. The second argument, -mtime, is used to specify the number of days old that the file is. If you enter +5, it will find files older than 5 days. The third argument, -exec, allows you to pass in a command such as rm. The {} ; at the end is required to end the command.

1. Delete files older than 1 Hour
find /path/to/files* -mmin +60 -exec rm {} \;
2. Delete files older than 30 days
find /path/to/files* -mtime +30 -exec rm {} \;
3. Delete files modified in the last 30 minutes
find /path/to/files* -type f -mmin 30 -exec rm {} \;
4. Move files older than 30 days to an archive Folder
find /tmp -mtime +30 -exec mv -t {} /archive/directory/ \;
The find utility on linux allows you to pass in a bunch of interesting arguments, including one to execute another command on each file. We’ll use this in order to figure out what files are older than a certain number of days, and then use the rm command to delete them. This should work on Ubuntu, Suse, Redhat, or pretty much any version of linux.

