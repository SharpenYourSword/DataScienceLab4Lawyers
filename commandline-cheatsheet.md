## Unix 'Simon says' commands

You type the command: | Computer will:
------------------------------|------
`ls`, `ls -alh` | _list_ files in current directory 
`pwd` | show name of _present working directory_
`cd <directory>` | _change directory_ to specified directory
`mkdir <directory>` | _make directory_ empty `<directory>`
`rmdir <directory>` | _remove directory_ empty `<directory>`
`cat <file>` | _catentate_ `<file>` to output (print)
`more <file>` | show _more_ of `<file>` with space key
`less <file>` | show _less_ at a time `<file>` with arrow keys
`head -n 20 <file>` | _head_ `20` lines of `<file>`
`tail -n 20 <file>` | _tail_ `20` lines of `<file>`
`wc -l <file>` | _word count lines_ in `<file>`
`cp <file1> <file2>` | _copy_ `<file1>` to `<file2>`
`mv <file1> <file2>` | _move_ `<file1>` to `<file2>`
`grep <pattern> <file>` | match _global regular expression print_ `<pattern>` in `<file>`
`wget <url>` | _web get_ `<url>`
`wget --no-check-certificate <url>` | _web get_ `<url>` from https (some risk)
`awk -F "," '{ print $2 }' <file>` | _Aho, Weinberger, and Kernighan's_ line filter to get second field of comma-delimited csv `<file>`

also see: 
- http://overapi.com/linux/
- https://kb.iu.edu/d/afsk

## Essential command line key strokes

Key stroke: | Computer will:   | Because:
------------|------------------|----------
`tab`     | autocomplete filename | nobody remembers file names
`up arrow`  | navigate back in command history | nobody remembers command syntax
`down arrow` | navigate forward in command history | nobody up arrows slowly
`delete`      | delete character left | nobody types it right the first time
`left arrow`  | move cursor left | nobody types it right the second time
`right arrow` | move cursor right | few type it right the third time
`ctrl+a`  | move cursor to start of line | right file but wrong command
`ctl+e`   | move cursor to end of line | there's always a fourth time
`ctl+c`   | break process; stop | the computer isn't doing it right

## Connecting commands with pipes
Like water through pipes, output from one command can be input another command.

```bash
# syntax for piping commands
command1 <file> | command2

# how many files in directory?
ls /etc/ | wc -l

# page through directory list
ls -alh /etc/ | more

# which flowers are about love?
cat /usr/share/misc/flowers | grep love

# which flowers are about love and are red?
cat /usr/share/misc/flowers | grep love | grep red

# split rows on ":" and print first "field" of row
awk -F ":" '{ print $1 }' /usr/share/misc/flowers 

# split rows on ":" and print first "field"...
# then split output by "," and print first "field" of that
awk -F ":" '{ print $1 }' /usr/share/misc/flowers | awk -F "," '{ print $1 }'

# split rows on ":" and get first "field"...
# split that by "," and get first "field"...
# sort, uniqu counts, and sort alphanumerically
awk -F ":" '{ print $1 }' /usr/share/misc/flowers | awk -F "," '{ print $1 }' | sort | uniq -c | sort -n

```

## Connecting to remote server via the commandline
syntax: `ssh <username>@<servername>`

example: 
```bash
ssh ubuntu@ec2-54-197-147-122.compute-1.amazonaws.com

The authenticity of host 'ec2-54-197-147-122.compute-1.amazonaws.com (54.197.147.122)' can't be established.
RSA key fingerprint is e2:87:c2:1e:e3:09:ec:a0:a1:53:aa:a6:b3:fa:4a:c5.
Are you sure you want to continue connecting (yes/no)? yes

Warning: Permanently added 'ec2-54-197-147-122.compute-1.amazonaws.com,54.197.147.122' (RSA) to the list of known hosts.

ubuntu@ec2-54-197-147-122.compute-1.amazonaws.com's password:
Welcome to Ubuntu 12.04.2 LTS (GNU/Linux 3.2.0-41-virtual x86_64)
```
