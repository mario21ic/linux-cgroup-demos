# linux-cgroup-demos

Install:
CentOS
```
$ sudo yum install libcgroup libcgroup-tools
```

On Ubuntu or Debian, type:
```
$ sudo apt-get install libcgroup1 cgroup-tools
```

Testing Cgroups
```
sudo mkdir /sys/fs/cgroup/memory/bar
sudo ls -la /sys/fs/cgroup/memory/bar/
echo 500 | sudo tee /sys/fs/cgroup/memory/bar/memory.limit_in_bytes
sh ./test.sh &
echo 1448407 |sudo tee /sys/fs/cgroup/memory/bar/cgroup.procs
ps -o cgroup 1448407
sudo cat /sys/fs/cgroup/memory/bar/memory.usage_in_bytes
sudo tail -f /var/log/syslog
```

Using tools:
```
sudo cgcreate -g memory:demo1
echo 500 |sudo tee /sys/fs/cgroup/memory/demo1/memory.limit_in_bytes
sudo cat /sys/fs/cgroup/memory/demo1/memory.limit_in_bytes
sudo cgexec -g memory:demo1 ./test.sh
sudo cgdelete memory:demo1
```

Steps from https://www.linuxjournal.com/content/everything-you-need-know-about-linux-containers-part-i-linux-control-groups-and-process
