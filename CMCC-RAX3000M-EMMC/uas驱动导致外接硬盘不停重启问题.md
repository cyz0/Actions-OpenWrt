在/etc/rc.local加入以下代码
```
ps: 其中{{0634:5602}}为lsusb命令所显示的磁盘id之类的值。示例如下:

root@ImmortalWrt:~# lsusb 
Bus 001 Device 001: ID 1d6b:0002 Linux 5.15.137 xhci-hcd xHCI Host Controller
Bus 002 Device 003: ID 0634:5602 Micron Crucial X6 SSD
Bus 002 Device 001: ID 1d6b:0003 Linux 5.15.137 xhci-hcd xHCI Host Controller

{{2-0:1.0}}部分为磁盘的device VID/PID

```

```
echo 0634:5602:u >/sys/module/usb_storage/parameters/quirks
echo "2-0:1.0" > /sys/bus/usb/drivers/hub/unbind
echo "2-0:1.0" > /sys/bus/usb/drivers/hub/bind

#rmmod uas
```