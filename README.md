# vagrant-debian-cpp: a Vagrant box for building C/C++ binaries for GNU/Linux (Debian)

# DEPRECATED

See https://github.com/mcandre/mucus

# VAGRANT CLOUD

* https://app.vagrantup.com/mcandre/boxes/vagrant-debian-cpp-amd64
* https://app.vagrantup.com/mcandre/boxes/vagrant-debian-cpp-i386
* https://app.vagrantup.com/mcandre/boxes/vagrant-debian-cpp-ppc64el

# EXAMPLE

```console
$ cd amd64/test
$ vagrant up
$ vagrant ssh -c "cd /vagrant && clang++ -o hello hello.cpp && ./hello"
Hello World!
```

# RUNTIME REQUIREMENTS

* [Vagrant](https://www.vagrantup.com)

## Recommended

* [VirtualBox](https://www.virtualbox.org/)
* [VMware](https://www.vmware.com/)
* [qemu](https://www.qemu.org/) 2.12+
* [KVM](https://wiki.qemu.org/Features/KVM)
* [OpenBIOS](https://www.openfirmware.info/OpenBIOS)
* [openhackware](https://github.com/qemu/openhackware)
* [qemu-skiboot](https://github.com/qemu/skiboot)
* [libguestfs-tools](http://libguestfs.org/)
* [vagrant-libvirt](https://github.com/vagrant-libvirt/vagrant-libvirt)
* [vagrant-rsync-back](https://github.com/smerrill/vagrant-rsync-back)
* [Ruby](https://www.ruby-lang.org/en/) (for rake)

# BUILD AND TEST BOXES

```console
$ sudo rake boxes import test
```

Unfortunately, sudo permissions are required for building boxes in order to resolve a discrepancy with how vagrant-libvirt interacts with libvirt.

# PUBLISH

```console
$ sudo rake publish
```

# CLEAN

```console
$ sudo rake clean
```
