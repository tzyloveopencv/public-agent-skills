# Linux Host

在 Host 执行，按需选择而非一次全跑：
```sh
command -v adb
adb version
adb devices -l
lsusb
lsusb -t
```
设备身份确定后，定向读取描述符，例如 `lsusb -v -d VID:PID`（同 VID/PID 多设备时还需总线和设备号）。权限不足是证据缺口，不自动 sudo 或修改 udev。

内核日志按故障窗口截取，优先已有 journal/dmesg；记录 disconnect、reset、枚举与驱动绑定顺序。命令不可用或日志权限不足时报告实际限制。

USB Host 的权限或接口占用与设备侧 adbd 故障分别验证。usbmon 抓包按内核文档和目标总线设置；启用、加载模块及长期采集依授权，采用大小/时间限制。不要为定位挂载 debugfs 或重置整条 USB 总线。

参考：https://docs.kernel.org/usb/usbmon.html
