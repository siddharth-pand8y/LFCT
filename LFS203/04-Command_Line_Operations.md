# Command Line Operations



### To start, stop or restart the graphical desktop

`sudo systemctl [stop|start|restart] [gdm|lightdm|kdm]`

`sudo telinit 3`

`sudo telinit 5`



### Text terminals on the Graphical Desktop

- **konsole** is the terminal emulator packaged with the **KDE** desktop system
  
  
  
  

### Logging in & out

- You can  via a text terminal or remotely via console
  `$ ssh student@somewhereelse.com` 

- Logging out of a text-mode session is done by typing 
  `$ exit`
  `$ logout`
  
  
  
  

### Rebooting & Shutting Down

* The preferred method to shutdown or reboot is to use `shutdown`.

* The `init` process will then follow its procedure for sutting down or rebooting the system

`shutdown -h` is meant for shutting down the system

`shutdown -r` is for restarting the system



#### Shutting down the system

```bash
sudo halt
sudo poweroff
sudo shutdown -h now
```

- To shudown at a specifed time with a message 
  
  ```bash
  shutdown -h 10:00 "Shutting down for scheduled maintenance."
  ```
  
  

#### Restarting the sytem

```bash
sudo reboot
sudo shutdown -r now
```

---

## Setting Time & Date with `timedatectl`

**timedatectl** is a systemd-supplied program for setting the date, time and timezone, etc.

```bash
$ timedatectl -h

___________________________________________________________________________
timedatectl [OPTIONS...] COMMAND ... 

Query or change system time and date settings.

Commands:
  status                   Show current time settings
  show                     Show properties of systemd-timedated
  set-time TIME            Set system time
  set-timezone ZONE        Set system time zone
  list-timezones           Show known time zones
  set-local-rtc BOOL       Enable or disable network time synchronization

systemd-timesyncd Commands:
  timesync-status          Show status of systemd-timesyncd
  show-timesync            Show properties of systemd-timesyncd

Options:
  -h --help                Show this help message
     --version             Show package version
     --no-pager            Do not pipe output into a pager
     --no-ask-password     Do not prompt for password
  -H --host=[USER@]HOST    Operate on remote host
  -M --machine=CONTAINER   Operate on local container
     --adjust-system-clock Adjust system clock when changing local RTC mode
     --monitor             Monitor status of systemd-timesyncd
  -p --property=NAME       Show only properties by this name
  -a --all                 Show all properties, including empty ones
     --value               When showing properties, only print the value

See the timedatectl(1) man page for details.
```

```bash
timedatectl -a 
```



```bash
$ timedatectl show
$ timedate set-timezone America/Toronto
$ timedatectl set-ntp `
$ timedatectl set-time 2022-05-27
```

---

## Network Time Protocol

- Historically, on older distributions, the standard configuration file for NTP utlities was **etc/ntp.confg**

- On RHEL, CentOS, Fedora & OpenSUSE systems configuration can be done with **etc/sysconfig/chronyd**

```bash
sudo systemctl status chronyd
```



Ubuntu still ships with ntp:

```bash
sudo systemctl status ntpd
sudo systemctl status systemd-timesync.service
```



---

## Locating Applications

Generally 

| Folder   | Type                                             |
| -------- | ------------------------------------------------ |
| /bin     | Essential binary programs and scripts            |
| /usr/bin | Non-essential binary programs and scripts        |
| /sbin    | Non-essential system binary programs and scripts |
| /opt     | Optional software application packages           |

A common way to locate the specific locatin of a program

```bash
$ which emacs
/usr/bin/emacs
```

```bash
$ whereis emacs
emacs: /usr/bin/emacs /usr/libexec/emacs /usr/share/emacs /usr/share/man/man1/emaacs.1.gz
```

On many recent system(ubuntu)

```bash
ls -lF / | grep bin

```

___

## Accessing Directories

#### Present working Directory

```bash
$ pwd
$ echo $PWD
```

#### Change to home directory

```bash
$ cd
$ cd ~
$ cd $HOME
```

#### Previous Directory

```bash
$ cd -
```

## Exploring the FileSystem



#### Root of the filesystem

```bash
$ cd /
```

#### List hidden files and directories

```bash
$ ls -a
```

#### Tree View

```bash
$ tree
```

#### Create symbolic link

```bash
$ ls -s /lib/modules/5.19 5.19
$ cd 5.19
```

#### Examples

```bash
cd / ; ls -F
tree | head -10
/bin/pwd                              #list the present working directory 
```

## Directory History, popd & pushd

```bash
$ pwd
/home/rjsquirrel

$ cd /tmp
$ cd -
/home/rjsquirrel

$ pushd /tmp
/tmp ˜

$ pushd /var/tmp
/var/tmp /tmp ˜

$ dirs
/var/tmp /tmp ˜

$ popd
/tmp ˜

$ pwd
/tmp
```

___

## Wildcards & File Name Matching

|        |                                  |
| ------ | -------------------------------- |
| ?      | matches any single character     |
| *      | matches any string of characters |
| [set]  | matches any charater in set      |
| [!set] | matches any character not in set |


