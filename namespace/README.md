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
