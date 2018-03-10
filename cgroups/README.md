# Linux Cgroups

`man cgroup` in Ubuntu.
cgroup - control group based traffic control filter

Cgroup + subsystem + hierachy

## Execute:

```sh
$ cd cgroups/
$ sudo go run cgroup.go
```
```sh
18540current pid 1
stress: info: [7] dispatching hogs: 0 cpu, 0 io, 1 vm, 0 hdd
```

## Play

```sh
$ ps -ef | grep 1854
root     18540 18535  0 20:44 pts/1    00:00:00 /proc/self/exe
root     18545 18540  0 20:44 pts/1    00:00:00 sh -c stress --vm-bytes 200m --vm-keep -m 1
root     18546 18545  0 20:44 pts/1    00:00:00 stress --vm-bytes 200m --vm-keep -m 1
root     18547 18546 41 20:44 pts/1    00:00:09 stress --vm-bytes 200m --vm-keep -m 1
```
```sh
$ top
PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
18547 root      20   0  212284 100304    276 D  40.1  1.2   0:04.63 stress
```
