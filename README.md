# vagrant-debian-cpp: a Vagrant box for building C/C++ binaries for GNU/Linux (Debian)

# VAGRANT CLOUD

* https://app.vagrantup.com/mcandre/boxes/vagrant-debian-cpp-amd64
* https://app.vagrantup.com/mcandre/boxes/vagrant-debian-cpp-i386

# EXAMPLE

```console
$ cd amd64/test
$ vagrant up
$ vagrant ssh -c "cd /vagrant && clang++ -o hello hello.cpp && ./hello"
Hello World!
```

# RUNTIME REQUIREMENTS

* [Vagrant](https://www.vagrantup.com)
* The [VirtualBox](https://www.virtualbox.org) hypervisor provider

## Recommended

* [vagrant-rsync-back](https://github.com/smerrill/vagrant-rsync-back) assists in copying artifacts from the guest to the host

# BUILDTIME REQUIREMENTS

* [Vagrant](https://www.vagrantup.com)
* The [VirtualBox](https://www.virtualbox.org) hypervisor provider

# BUILD AND TEST BOXES

```console
$ rake boxes import test
```

# PUBLISH

```console
$ rake publish
```

# CLEAN

```console
$ rake clean
```
