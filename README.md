# vagrant-debian-cpp: a Vagrant box for building C/C++ binaries for GNU/Linux (Debian)

# VAGRANT CLOUD

https://app.vagrantup.com/mcandre/boxes/vagrant-freebsd-cpp

# EXAMPLE

```console
$ vagrant up
$ vagrant ssh -c "cd /vagrant && clang++ -o hello hello.cpp && ./hello"
Hello World!
```

# REQUIREMENTS

* [Vagrant](https://www.vagrantup.com)
* A VM provider, such as [VirtualBox](https://www.virtualbox.org), [VMware](https://www.vmware.com), or [libvirt](https://libvirt.org)

# EXPORT

```console
$ vagrant package --output vagrant-debian-cpp.box
```
