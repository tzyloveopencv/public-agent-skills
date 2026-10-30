# Android Host

先确认 Android 是 USB Host 还是被调试的 Device。手机上运行 adb client / host 方案需要实际工具与权限支持，不能假定系统预装 adb Host。

通过已存在的调试通道按需读取 `getprop`、限定窗口的 `logcat -d`、USB service 状态；`dumpsys usb` 的可用性和输出取决于版本与权限。Android USB Host API 应用与 adb server 的诊断路径不同，先确定哪一个负责当前连接。

确认 Type-C/OTG 角色、供电关系、应用接口 claim 与权限。如果 Android 是 Device，转读 gadget 参考，不套用 Host 枚举步骤。不要用通用 `setprop` 修改厂商 USB 配置，除非已核实对应版本实现和当前授权。
