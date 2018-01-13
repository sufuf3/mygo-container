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
