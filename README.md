# vagrant-debian-cpp: a Vagrant box for building C/C++ binaries for GNU/Linux (Debian)

# VAGRANT CLOUD

https://app.vagrantup.com/mcandre/boxes/vagrant-debian-cpp

# EXAMPLE

```console
$ vagrant up
$ vagrant ssh -c "cd /vagrant && clang++ -o hello hello.cpp && ./hello"
Hello World!
```

# RUNTIME REQUIREMENTS

* [Vagrant](https://www.vagrantup.com)
* A supported hypervisor provider in {[VirtualBox](https://www.virtualbox.org), [VMWare](https://www.vmware.com/), [libvirt](https://libvirt.org/)}, along with any relevant Vagrant plugins.

# BUILDTIME REQUIREMENTS

* [Vagrant](https://www.vagrantup.com)
* A supported hypervisor provider in {[VirtualBox](https://www.virtualbox.org), [VMWare](https://www.vmware.com/), [libvirt](https://libvirt.org/)}, along with any relevant Vagrant plugins.
* [make](https://www.gnu.org/software/make/)

# EXPORT

```console
$ make vagrant-debian-cpp.box
```

Unfortunately, VMware-provided Vagrant boxes do not support straightforward packaging for reuse as new Vagrant base boxes, so VirtualBox-provided boxes are preferred here.
