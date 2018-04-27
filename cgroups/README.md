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
2306current pid 1
stress: info: [6] dispatching hogs: 0 cpu, 0 io, 1 vm, 0 hdd
```

## Play

```sh
$ ps -ef | grep 2091
root      2306  2302  0 15:42 pts/1    00:00:00 /proc/self/exe
root      2311  2306  0 15:42 pts/1    00:00:00 sh -c stress --vm-bytes 200m --vm-keep -m 1
```
```sh
$ top
PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
2314 root      20   0  212284 204928    276 R 100.0  6.7   1:19.87 stress --vm-bytes 200m --vm-keep -m 1 
```
