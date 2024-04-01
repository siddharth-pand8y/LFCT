

# Boot Process & System Initilization

### Bootloader

The boot loader is usually stored on one of the hard disks in the system. Either in the boot sector (for traditional BIOS/MBR system) or the EFI partition in EFI/UEFI systems.



GRUB - GRand Unified Bootloader

Das U-Boot (used on embedded system)

ISOLINUX - booting from removable media

### Linux Kernel

The boot loaders loads

- kernel image & passes control to it

- file called intial RAM disk, **initramfs** or **initrd**
  
  

Intital RAM disk contains a very minimal filesystem with some hardware drivers necessary for the system to boot such as driver for dis controlllers



The initramfs must be build individually for each linux system as it must contain the specific device drivers and protocols needed by both the hardware and kernel configuration



Linux distributor can deploy the same kernel for each system but the initramfs should be rebuild every time linux is installed or the kernel is updated or reconfigured.



### /sbin/init

```bash
ls -l $(which init)
```



**systemd** - modern system use systemd to manage the booot and initialization process

- server web pages using **httpd**

- serve files using **vsftpd**

- manage printers using **cupsd**
  
  

To enable or disable a service starting at boot on systemd-based system (add modern systes), you can do 

```bash
$ sudo systemctl enable httpd
$ sudo systemctl disable httpd
```

To turn a service on or off after boot

```bash
$ sudo systemctl start httpd
$ sudo systemctl stop httpd
```



- systemd is backward compatible with SysVinit

- systemd used `.services` files insteaf of bash scripts

- systemd sorts all daemons into their own Linux cgroups(control groups)

### `systemd` Features

- Boots faster than previous init systems

- Provides aggresive parallelization capabilities

- Uses socket and D-Bus for starting services

- Replaces shell script with programs

- Offers on-demand starting of daemons

- keeps track of processes using cgroups

- Maintains mount & automount positions

- Implements an elaborate transactional dependency-based service control logic

- Can work as a drop-in replacement for SysVinit and is compatible with SysVinit scripts

### `systemd` Configuration FIle

`/etc/vconsole.conf` - configures virtual terminal defaults

`/etc/hostname` (DEB) or `etc/sysconfig/network` (RH) `etc/HOSTNAME` (SUSE)



### `systemctl`

**systemctl** is the main utility for managing services. Some **systemctl** commands can be run as non-root user, while others require running as root or with **sudo**

`systemctl` - view status of everything that systemd controls

`systemctl list-units -t service --all` - show all available services

`systemctl list-utnits -t service` - show only active services



```bash
sudo systemctl start foo
sudo systemctl start foo.service
sudo systemctl start /path/to/foo.service
```

where a unit can be a service or a socket

```bash
sudo systemctl stop foo.service
```

To enable or disable a service (control whether a service is started at system boot)

```bash
sudo systemctl enable sshd.service
sudo systemctl disable sshd.service
```

```bash
sudo journalctl -f & <script>
```

##### Reloading things

```bash
sudo systemctl daemon-reload
```


