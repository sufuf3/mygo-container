# UTS Namespace

## Execute:
```sh
$ cd namespace/
$ sudo go run uts.go
```
## play with UTS Namespace
- Get the pid from program
```
# echo $$
9121
```

- Get the ps from host(my computer)
```sh
$ pstree -pl
─bash(5940)───sudo(9098)───go(9099)─┬─uts(9117)─┬─sh(9121)
                                    │           ├─{uts}(9119)
                                    │           └─{uts}(9120)
```

- Check the namespace type and inode number in program 
(ref: http://man7.org/linux/man-pages/man7/namespaces.7.html)
```sh
# readlink /proc/$$/ns/uts
uts:[4026532211]
# readlink /proc/9121/ns/uts
uts:[4026532211]
# readlink /proc/9117/ns/uts
uts:[4026531838]
```
Memo: `# readlink /proc/9117/ns/uts` is chaeck the child process is different from program process.

- Play the hostname with child process `#` & host `$`
```sh
# hostname -b mylittlecontainer
# hostname
mylittlecontainer
```
```sh
$ hostname
build-container
```

# IPC Namespace
- Run program
```sh
$ sudo go run ipc.go
# readlink /proc/$$/ns/uts /proc/$$/ns/ipc
uts:[4026532211]
ipc:[4026532212]
# ipcs -q

------ Message Queues --------
key        msqid      owner      perms      used-bytes   messages

# ipcmk -Q
Message queue id: 0
# ipcs -q

------ Message Queues --------
key        msqid      owner      perms      used-bytes   messages
0x4364496c 0          root       644        0            0

# go run ipc.go
# ipcs -q

------ Message Queues --------
key        msqid      owner      perms      used-bytes   messages
```

- Get the ps from host(my computer)
```
$ pstree -pl
──sudo(15364)───go(15367)─┬─ipc(15390)─┬─sh(15394)───go(15411)─┬─ipc(15429)─┬─sh(15433)
                          │            │                       │            ├─{ipc}(15431)
                          │            │                       │            └─{ipc}(15432)
```

# PID Namespace
```sh
─bash(5940)───sudo(18717)───go(18718)─┬─pid(18736)─┬─sh(18740)
                                      │            ├─{pid}(18738)
                                      │            └─{pid}(18739)
                                      ├─{go}(18719)
                                      ├─{go}(18720)
                                      ├─{go}(18721)
                                      ├─{go}(18726)
                                      ├─{go}(18737)
                                      └─{go}(18741)
```
`$`: PID = 18736
`#`: PID = 1
- Run program
```
sudo go run pid.go
# echo $$
1
```

# Mount Namespace
```sh
$ sudo go run mount.go 
# ls /proc
1     1244   14030  18395  2      27   409   6022  92         driver       key-users    mtrr          sys
10    1245   1483   18396  20     276  410   6722  acpi       execdomains  kmsg         net           sysrq-trigger
1067  1250   15     18397  20008  28   411   7     buddyinfo  fb           kpagecgroup  pagetypeinfo  sysvipc
11    13     1580   18458  20026  32   412   76    bus        filesystems  kpagecount   partitions    thread-self
1104  1365   15915  19     2015   327  413   77    cgroups    fs           kpageflags   sched_debug   timer_list
1105  13788  16     19184  2016   328  414   78    cmdline    interrupts   loadavg      schedstat     tty
1111  13789  1645   19762  21     33   452   79    consoles   iomem        locks        scsi          uptime
112   13930  1660   19810  22     34   456   8     cpuinfo    ioports      mdstat       self          version
1130  1394   17     19811  23     4    5773  8259  crypto     irq          meminfo      slabinfo      version_signature
1155  14     18     19830  24     403  5939  85    devices    kallsyms     misc         softirqs      vmallocinfo
12    14025  18088  19833  25     406  5940  895   diskstats  kcore        modules      stat          vmstat
1228  14026  18304  19841  26     408  6     9     dma        keys         mounts       swaps         zoneinfo
# mount -t proc proc /proc
# ls /proc
1          consoles   execdomains  irq          kpagecount  modules       schedstat  sys            version
4          cpuinfo    fb           kallsyms     kpageflags  mounts        scsi       sysrq-trigger  version_signature
acpi       crypto     filesystems  kcore        loadavg     mtrr          self       sysvipc        vmallocinfo
buddyinfo  devices    fs           keys         locks       net           slabinfo   thread-self    vmstat
bus        diskstats  interrupts   key-users    mdstat      pagetypeinfo  softirqs   timer_list     zoneinfo
cgroups    dma        iomem        kmsg         meminfo     partitions    stat       tty
cmdline    driver     ioports      kpagecgroup  misc        sched_debug   swaps      uptime
# ps -ef
UID        PID  PPID  C STIME TTY          TIME CMD
root         1     0  0 10:20 pts/1    00:00:00 sh
root         5     1  0 10:21 pts/1    00:00:00 ps -ef
```

# Coding Style
`go fmt <filename>`

