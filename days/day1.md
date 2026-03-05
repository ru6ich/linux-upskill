# Day 01 — Server inventory (quick command memo)

Date: 2026-03-04  
Server: `<public-ip-or-dns>`  
Goal: collect “what is this server?” baseline: OS, hardware, load, disk, network.


## 1) General information about the server
* `lsb_release -a` -  Distro name/version (Ubuntu/Debian family; may need `lsb-release`).
* `cat /etc/os-release` -  OS identification fields (works on most distros).
* `uname -a` -  Kernel + arch + build info (quick kernel fingerprint).
* `uptime` -  How long running + load averages + logged in users count.
* `cat /proc/uptime` -  Raw uptime seconds (and idle time) from kernel.
* `whoami` -  Current user (useful in sudo/role context).
* `who` -  Logged-in users + terminals + login time (basic session list).
* `w` - Who is logged in + what they’re doing + load averages.

## 2) Hardware information
* `sudo lshw -short` - Hardware summary (CPU/RAM/disks/NICs) in a compact table.
* `lsblk` - Block devices, partitions, filesystems, and mountpoints (disk layout).
* `lscpu` - CPU details: model, cores/threads, flags, virtualization.
* `lspci` - List PCI devices (NICs, storage controllers, GPUs, etc.).
* `lsusb` - List USB devices (often minimal/empty on VMs).

## 3) Measure memory and CPU usage
* `free -h` - RAM and swap usage (human-readable); pay attention to `available`.
* `vmstat 1 5` - VM/CPU/memory/IO stats sampled every 1s (5 samples).
* `top` - Live process view: CPU/memory usage, load, running processes.
* `htop` - Enhanced interactive process viewer (friendlier `top`, may need install).

## 4) Measure disk usage
* `df -h` - Filesystem space usage by mountpoint (human-readable).
* `du -h -d 1 /path` - Sizes of top-level directories under `/path` (find space hogs).

## 5) Measure network usage
* `ifconfig` - Legacy interface config/status (from `net-tools`; `ip` is preferred).
* `ip address` - Modern view of interfaces + IPv4/IPv6 addresses + state.
* `netstat -i` - Legacy per-interface packet/error counters table (`ip -s link` is modern alternative).
* `ifstat` - Simple per-interface bandwidth monitor (rx/tx rates).
* `sudo iftop -i eth0` - Live “top” for network connections by bandwidth on interface (replace `eth0`).
