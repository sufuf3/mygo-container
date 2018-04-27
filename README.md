# Build my own container with go
Learn how to build the container with go lang.

# Environment
```
$ uname -a
Linux build-container 4.13.0-1002-gcp #5-Ubuntu SMP Tue Dec 5 13:20:17 UTC 2017 x86_64 x86_64 x86_64 GNU/Linux
$ lsb_release -a
No LSB modules are available.
Distributor ID: Ubuntu
Description:    Ubuntu 16.04.3 LTS
Release:        16.04
Codename:       xenial
```

# Install go
According to https://github.com/golang/go/wiki/Ubuntu
```sh
$ sudo add-apt-repository ppa:longsleep/golang-backports
$ sudo apt-get update
$ sudo apt-get install golang-go
```
