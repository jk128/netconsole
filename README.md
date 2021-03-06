netconsole service
==================

netconsole is a Linux kernel module that sends all kernel log messages over
the network to another computer. It was designed to be as instantaneous as
possible, to enable the logging of even the most critical kernel bugs. It
works from IRQ contexts as well, and does not enable interrupts while sending
packets. Due to these unique needs, only IP networks, UDP packets and Ethernet
devices are supported. More information can be found in
[networking/netconsole.txt](https://www.kernel.org/doc/Documentation/networking/netconsole.txt)
of the Linux kernel documentation.

This project provides a netconsole service that dynamically configures
netconsole by configuring one or more hosts by their names or IP addresses.

`netconsole-setup` eases the configuration of the netconsole by just taking
the target hostname or IP address. It determines all the needed configuration
values from the running network device (like network interface, target IP and
MAC address). Multiple target hosts can be specified. Each host can be prefixed
with a target port and a plus sign to enable extended console support.

Examples
========

```
netconsole-setup loghost
```

sends all kernel log messages to host `loghost`.

```
netconsole-setup +4444@loghost
```

sends all kernel log messages to host `loghost` on port `4444` using the
extended console support.

```
netconsole-setup loghost1 4444@loghost2
```

sends all kernel log messages to host `loghost1` on the default port and to
host `loghost2` on port `4444`.

Alternatives
============

The `initscripts` package on CentOS 7 provides a `/etc/init.d/netconsole`
initscript that can configure netconsole by just configuring `SYSLOGADDR`.
The functionality is similar, but this project provides also a systemd service
and allows to specify multiple log hosts.

Dependencies
============

Following commands need to be available for `netconsole-setup`:

* `arping` from the [iputils](https://github.com/iputils/iputils) project
(provided by the `iputils-arping` package on Debian-based systems)
* `ip` from the [iproute2](https://wiki.linuxfoundation.org/networking/iproute2)
project
* `modprobe` (provided by the `kmod` package on Debian-based systems)
* `mount`

`pandoc` is required for generating the man page for netconsole-setup.

Contributing
============

Contributions are welcome. Please follow
[How to Write a Git Commit Message](https://chris.beams.io/posts/git-commit/)
for writing good commit messages.
