---
layout: post
title: Introduction to the Command Line
excerpt: "Using CLI is important for using our tools and firefighting"
tags: [bash, zsh, command line, cli, shell]
comments: true

---
# Motivation

-   Many of us are new to using \*nix systems
-   This can be a daunting system when thrown in
-   Using CLI is important for using our tools and firefighting

# How to Use the Shell

-   Scroll through old commands: C-n, C-p
-   List your shell history: history
-   Search for old command:  C-r
-   Move to the beginning of a line: C-a
-   Move to the end of a line: C-e

# Basics

## Echo

-   displays provided string or variable

{% highlight bash %}
$ echo "Hello World"
    Hello World
{% endhighlight %}

## List Files
{% highlight bash %}
$ ls
    talk.html talk.org

$ ls -lah
    total 24
    drwxr-xr-x@  4 ngrayson  staff   136B Dec 15 15:13 .
    drwxr-xr-x@ 16 ngrayson  staff   544B Dec 15 14:49 ..
    -rw-r--r--@  1 ngrayson  staff   4.3K Dec 15 15:13 talk.html
    -rw-r--r--@  1 ngrayson  staff   845B Dec 15 15:13 talk.org

$ tree
    .
    ├── talk.html
    └── talk.org

    0 directories, 2 files
    {% endhighlight %}

-   Note tree is likely not installed by default (brew install tree)

## Change Directories

-   ~ is your homedir
-   \`cd\` == \`cd ~\`
-   . is the current dir
-   .. is one dir 'up'

{% highlight bash %}
$ cd /tmp
$ pwd
    /tmp
$ cd ~
{% endhighlight %}

## Create Directories

{% highlight bash %}
$ mkdir test/testing
    mkdir: test: No such file or directory
$ mkdir -p test/testing
{% endhighlight %}
## Create Files

-   touch, cp, mv, ln

{% highlight bash %}
$ touch file
$ cp file file2
$ mv file file1
$ ln -s file file1
{% endhighlight %}
## Remove Files
{% highlight bash %}
$ rm testing/file
$ rm -rf testing
{% endhighlight %}
## Show files
{% highlight bash %}
$ cat test/testing/file
    This
    is
    a
    file!
$ head -n 1
    This
$ tail -n 1
    file!
{% endhighlight %}
## Wildcards

-   Can be used with most commands
{% highlight bash %}
$ cat test/testing/*
    This
    is
    a
    file!
    Hello World
$ ls /Users/*/banno/cookbooks/node-*
{% endhighlight %}
## Docs

-   man <command>
-   &#x2013;help, -h

## Sudo

-   Runs a command as the super user (root)
{% highlight bash %}
$ sudo whoami
    Password:
    root
{% endhighlight %}
# Environment

-   Variables that customize how you interact with programs

## env

-   Displays all environment variables
{% highlight bash %}
$ env
    HOSTNAME=MacBook-Pro.local
    TERM=xterm
{% endhighlight %}
## PATH

-   Contains paths to directories you want the system to look for executables
-   Setup in .bashrc, .bash_profile, or .zshrc
{% highlight bash %}
$ echo $PATH
    /Users/ngrayson/node_modules/.bin:/Users/ngrayson/.cask/bin:/usr/local/opt/ruby/bin:/Users/ngrayson/bin:/usr/local/share/python:/usr/local/bin:/usr/local/sbin:/usr/local/bin:/usr/bin:/bin:/usr/sbin:/sbin:/Users/ngrayson
{% endhighlight %}
## Export

-   Usually found in your shell profile
-   Sets the value of a variable for use later
{% highlight bash %}
$ export SECRET_CODE=abcdefgh
$ echo $SECRET_CODE
    abcdefgh
{% endhighlight %}
## Reloading Your Environment

-   bash: source ~/.bashrc
-   zsh: run command: reload

# Redirection

## Pipe

-   Redirects all output from one command to another
-   Much like a function call
-   Can be chained together

{% highlight bash %}
$ ls -l|cut -d' ' -f1|grep -v total|sort|uniq -c|sort -nr
       4 -rw-r--r--@
       2 drwxr-xr-x@
{% endhighlight %}
## Redirection Operator

{% highlight bash %}
> overwrites
>> appends

$ cat test/testing/file > test/newfile
$ cat test/newfile
    This
    is
    a
    file!
$ echo "Another line" >> test/newfile
$ cat test/newfile
    This
    is
    a
    file!
    Another line
{% endhighlight %}
## Streams

-   stdin: stream of text going into a program
-   stdout: standard output of a program
-   stderr: typically used to display errors
-   Redirect stderr to stdout: 2>&1

## tee

-   Reads from stdin and writes to stdout or a file

{% highlight bash %}
$ echo "This is a test" | tee
    This is a test
$ echo "This is a test" | tee test
    This is a test
$ cat test
    This is a test
{% endhighlight %}
# Searching

## Grep

-   Search a file or stream from pipe
-   Useful flags: -i, -v, -r

{% highlight bash %}
$ grep is test/testing/file
    This
    is
$ cat test/testing/file | grep -i this
    This
{% endhighlight %}
## Grep Replacements

-   ack-grep
-   ag

{% highlight bash %}
$ ag This
    newfile
    1:This

    testing/file
    1:This
{% endhighlight %}
## Find

-   This could be it's own talk
-   Allow very specific searching and execution

{% highlight bash %}
$ find . -type d -name "*test*"
    ./test
    ./test/testing
$ find . -type f -name "*file*" -exec cat {} \;
    This
    is
    a
    file!
    Another line
    This
    is
    a
    file!
    Hello World
{% endhighlight %}
## Locate

-   Uses system db of file

{% highlight bash %}
$ locate talk.org
    /Users/ngrayson/banno/internal-talks/adam-scala-jenkins-docker-big/talk.org
    /Users/ngrayson/banno/internal-talks/chef-nic-11-02-13/chef-talk.org
{% endhighlight %}
## which

-   outputs the path to an execuctable on your PATH

{% highlight bash %}
$ which knife
    /Users/ngrayson/deploy/bin/knife
$ which -a knife
    /Users/ngraysondeploy/bin/knife
    /usr/local/bin/knife
{% endhighlight %}
# Processing Output

## sort

{% highlight bash %}
$ cat letters
    b
    a
    d
    c
    a
    c
$ cat letters|sort
    a
    a
    b
    c
    c
    d
{% endhighlight %}
## uniq

{% highlight bash %}
$ cat letters|sort |uniq
    a
    b
    c
    d
$ cat letters|sort |uniq -c |sort -nr
       2 c
       2 a
       1 d
       1 b
{% endhighlight %}
## cut

{% highlight bash %}
$ cat words
    first second third
    1st 2nd 3rd
$ cat words|cut -d' ' -f2
    second
    2nd
{% endhighlight %}
## rev

{% highlight bash %}
$ echo "abcde" |rev
    edcba
{% endhighlight %}
## sed

-   Find and replace
-   There is a lot to this tool

{% highlight bash %}
$ echo "Hello World" |sed 's/World/Nic/'
    Hello Nic
{% endhighlight %}
## wc

{% highlight bash %}
$ wc words
           2       6      31 words
$ wc -l words
           2 words
{% endhighlight %}
# Permissions

## chown

-   change owner and/or group of file

{% highlight bash %}
$ chown -R foo.bar test
{% endhighlight %}
## chmod

-   u = user
-   g = group
-   o = other
-   r = read
-   w = write
-   x = execute

{% highlight bash %}
$ chmod u+x file
$ chmod ug-x file
$ chmod 755 file
$ chmod 644 file
{% endhighlight %}
# Interacting with Processes

## ps

-   lists running processes
-   aux, faux

{% highlight bash %}
$ ps aux
    USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
    root         1  2.3  0.0  18172  3368 ?        Ss   22:26   0:00 bash
    root        17  0.0  0.0  15572  2096 ?        R+   22:26   0:00 ps aux
{% endhighlight %}
## kill

-   kill -9 forces the kill if the process is hung

{% highlight bash %}
$ ps aux
    USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
    root         1  1.1  0.0  18172  3340 ?        Ss   22:27   0:00 bash
    root        16  0.0  0.0   4348   656 ?        S    22:27   0:00 sleep 1000
    root        17  0.0  0.0  15572  2152 ?        R+   22:27   0:00 ps aux
$ kill 16
$ ps aux
    USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
    root         1  0.1  0.0  18172  3344 ?        Ss   22:27   0:00 bash
    root        24  0.0  0.0  15572  2032 ?        R+   22:30   0:00 ps aux
{% endhighlight %}
## top

-   Displays list of running process in an interactive way
-   Shift+m sorts by memory usage
-   Shift+p sorts by cpu usage
-   q exits

## htop

-   more in depth version of top, not on all systems

## &

-   Runs a process in the background

{% highlight bash %}
$ sleep 1000 &
    [1] 27187
{% endhighlight %}
## Exit Status

-   When a command finishes it returns a number
-   This is placed in the $? variable
-   0 means the command completed succuessfully
-   More information here: <http://tldp.org/LDP/abs/html/exitcodes.html>

{% highlight bash %}
$ echo "test"
    test
$ echo $?
    0
$ cat notafile
    cat: notafile: No such file or directory
$ echo $?
    1
{% endhighlight %}
# Networking

## ping

-   Sends icmp packets at domain or ip

{% highlight bash %}
$ ping google.com
    PING google.com (74.125.207.113): 56 data bytes
    64 bytes from 74.125.207.113: icmp_seq=0 ttl=49 time=27.630 ms
    64 bytes from 74.125.207.113: icmp_seq=1 ttl=49 time=35.561 ms
    64 bytes from 74.125.207.113: icmp_seq=2 ttl=49 time=32.500 ms
{% endhighlight %}
## host

-   Attempts to lookup a hostname for the ip provided

{% highlight bash %}
$ host 8.8.8.8
    8.8.8.8.in-addr.arpa domain name pointer google-public-dns-a.google.com.
{% endhighlight %}
## dig

-   Looks up the ip associated with a domain name
-   +short displays only the ip address

{% highlight bash %}
$ dig banno.com

    ; <<>> DiG 9.8.3-P1 <<>> banno.com
    ;; global options: +cmd
    ;; Got answer:
    ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 23178
    ;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

    ;; QUESTION SECTION:
    ;banno.com.                     IN      A

    ;; ANSWER SECTION:
    banno.com.              9       IN      A       54.84.218.15

    ;; Query time: 146 msec
    ;; SERVER: 10.3.0.53#53(10.3.0.53)
    ;; WHEN: Tue Dec 16 10:20:13 2014
    ;; MSG SIZE  rcvd: 43
$ dig +short ns banno.com
    ns-1632.awsdns-12.co.uk.
    ns-692.awsdns-22.net.
    ns-347.awsdns-43.com.
    ns-1475.awsdns-56.org.
{% endhighlight %}
## netstat

-   -lpn is most used to display listening ports
-   -lpn only shows the program name if you are root or sudoing
-   Does not work on mac

{% highlight bash %}
    root@mesos-master1:~# netstat -lpn
    Active Internet connections (only servers)
    Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
    tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      1063/sshd
    tcp        0      0 10.10.1.33:5050         0.0.0.0:*               LISTEN      8201/mesos-master
    tcp6       0      0 :::8080                 :::*                    LISTEN      5761/docker-proxy
    tcp6       0      0 :::8081                 :::*                    LISTEN      10375/docker-proxy
    tcp6       0      0 :::22                   :::*                    LISTEN      1063/sshd
    udp        0      0 0.0.0.0:20436           0.0.0.0:*                           587/dhclient
    udp        0      0 0.0.0.0:68              0.0.0.0:*                           587/dhclient
    udp        0      0 172.17.42.1:123         0.0.0.0:*                           1543/ntpd
    udp        0      0 10.10.1.33:123          0.0.0.0:*                           1543/ntpd
    udp        0      0 127.0.0.1:123           0.0.0.0:*                           1543/ntpd
    udp        0      0 0.0.0.0:123             0.0.0.0:*                           1543/ntpd
    udp6       0      0 :::9816                 :::*                                587/dhclient
    udp6       0      0 :::123                  :::*                                1543/ntpd
    Active UNIX domain sockets (only servers)
    Proto RefCnt Flags       Type       State         I-Node   PID/Program name    Path
    unix  2      [ ACC ]     SEQPACKET  LISTENING     7738     402/systemd-udevd   /run/udev/control
    unix  2      [ ACC ]     STREAM     LISTENING     8781     811/dbus-daemon     /var/run/dbus/system_bus_socket
    unix  2      [ ACC ]     STREAM     LISTENING     7171     1/init              @/com/ubuntu/upstart
    unix  2      [ ACC ]     STREAM     LISTENING     11940    1503/docker         /var/run/docker.sock
    unix  2      [ ACC ]     STREAM     LISTENING     9209     1069/acpid          /var/run/acpid.socket
{% endhighlight %}
## ifconfig

-   Lists information about networking on your computer

{% highlight bash %}
$ ifconfig
    eth0      Link encap:Ethernet  HWaddr 02:42:ac:11:00:0e
              inet addr:172.17.0.14  Bcast:0.0.0.0  Mask:255.255.0.0
              inet6 addr: fe80::42:acff:fe11:e/64 Scope:Link
              UP BROADCAST RUNNING  MTU:1500  Metric:1
              RX packets:3 errors:0 dropped:0 overruns:0 frame:0
              TX packets:5 errors:0 dropped:0 overruns:0 carrier:0
              collisions:0 txqueuelen:1000
              RX bytes:258 (258.0 B)  TX bytes:418 (418.0 B)

    lo        Link encap:Local Loopback
              inet addr:127.0.0.1  Mask:255.0.0.0
              inet6 addr: ::1/128 Scope:Host
              UP LOOPBACK RUNNING  MTU:65536  Metric:1
              RX packets:0 errors:0 dropped:0 overruns:0 frame:0
              TX packets:0 errors:0 dropped:0 overruns:0 carrier:0
              collisions:0 txqueuelen:0
              RX bytes:0 (0.0 B)  TX bytes:0 (0.0 B)
{% endhighlight %}
# Information Collection

## df

-   Displays system wide disk usage
-   -h displays 'human readable'

{% highlight bash %}
$ df -h
    Filesystem      Size  Used Avail Use% Mounted on
    rootfs           96G   36G   55G  40% /
    none             96G   36G   55G  40% /
    tmpfs           2.0G     0  2.0G   0% /dev
    shm              64M     0   64M   0% /dev/shm
    /dev/sda1        96G   36G   55G  40% /etc/hosts
    tmpfs           2.0G     0  2.0G   0% /proc/kcore
{% endhighlight %}
## du

-   Displays an estimate of file space usage

{% highlight bash %}
    /var# du -sh *
    4.0K    backups
    2.7M    cache
    9.1M    lib
    4.0K    local
    0       lock
    292K    log
    4.0K    mail
    4.0K    opt
    0       run
    20K     spool
    4.0K    tmp
{% endhighlight %}
## free

-   Shows current memory usage
-   -m display in megabytes
-   Does not work on Mac

{% highlight bash %}
    free -m
                 total       used       free     shared    buffers     cached
    Mem:          3910       2391       1518        202        197       1760
    -/+ buffers/cache:        433       3476
    Swap:         1877          2       1874
{% endhighlight %}
## w

-   Shows which users are logged in currently

{% highlight bash %}
$ w
    10:29  up 5 days, 18:12, 2 users, load averages: 2.24 1.99 1.89
    USER     TTY      FROM              LOGIN@  IDLE WHAT
    ngrayson console  -                 8:55    1:34 -
{% endhighlight %}
## lastlog

-   Shows a list of users and when they have logged in

{% highlight bash %}
$ lastlog
    Username         Port     From             Latest
    root                                       **Never logged in**
    daemon                                     **Never logged in**
    bin                                        **Never logged in**
    sys                                        **Never logged in**
    sync                                       **Never logged in**
    games                                      **Never logged in**
    man                                        **Never logged in**
    lp                                         **Never logged in**
    mail                                       **Never logged in**
    news                                       **Never logged in**
    uucp                                       **Never logged in**
    proxy                                      **Never logged in**
    www-data                                   **Never logged in**
    backup                                     **Never logged in**
    list                                       **Never logged in**
    irc                                        **Never logged in**
    gnats                                      **Never logged in**
    nobody                                     **Never logged in**
{% endhighlight %}
# Working with Files

## tar

-   Archiving utility

{% highlight bash %}
$ tar cfvz test.tar.gz test
    a test
    a test/file1
    a test/file2
    a test/newfile
    a test/testing
    a test/testing/file
    a test/testing/file2
$ tar xfvz test.tar.gz
    x ./._test
    x test/
    x test/._file1
    x test/file1
    x test/._file2
    x test/file2
    x test/._newfile
    x test/newfile
    x test/._testing
    x test/testing/
    x test/testing/._file
    x test/testing/file
    x test/testing/._file2
    x test/testing/file2
{% endhighlight %}
## zip & unzip

-   Created or unzips files

{% highlight bash %}
$ zip test.zip test/*
      adding: test/file1 (stored 0%)
      adding: test/file2 (stored 0%)
      adding: test/newfile (stored 0%)
      adding: test/testing/ (stored 0%)
$ unzip test.zip
    Archive:  test.zip
     extracting: test/file1
     extracting: test/file2
     extracting: test/newfile
       creating: test/testing/
{% endhighlight %}
## rsync

-   Used to sync two directory
-   Can go over ssh

{% highlight bash %}
$ rsync -plarv test/ test2/
    building file list ... done
    created directory test2
    ./
    file1
    file2
    newfile
    testing/

    sent 315 bytes  received 98 bytes  826.00 bytes/sec
    total size is 29  speedup is 0.07
{% endhighlight %}
## scp

-   Uses ssh to copy a file to another computer

{% highlight bash %}
$ scp test.tar.gz stagingapps.foo.com:/home/ngrayson/
    test.tar.gz                                                                                                                                   100%  906     0.9KB/s   00:00
{% endhighlight %}
# Customizing Your Shell

## alias

-   Create resusable shortcut
-   Place in your profile file to always have them

{% highlight bash %}
$ ls
    talk.html   talk.org    test        test.tar.gz test.zip    test2
$ alias ll="ls -lah"
$ ll
    total 96
    drwxr-xr-x@  8 ngrayson  staff   272B Dec 16 10:52 .
    drwxr-xr-x@ 16 ngrayson  staff   544B Dec 15 15:23 ..
    -rw-r--r--@  1 ngrayson  staff    23K Dec 16 10:52 talk.html
    -rw-r--r--@  1 ngrayson  staff    14K Dec 16 10:52 talk.org
    drwxr-xr-x@  6 ngrayson  staff   204B Dec 16 10:48 test
    -rw-r--r--@  1 ngrayson  staff   906B Dec 16 10:47 test.tar.gz
    -rw-r--r--@  1 ngrayson  staff   653B Dec 16 10:48 test.zip
    drwxr-xr-x@  6 ngrayson  staff   204B Dec 16 10:48 test2
{% endhighlight %}
## zsh + oh_my_zsh

-   <https://github.com/robbyrussell/oh-my-zsh>

# Questions?
