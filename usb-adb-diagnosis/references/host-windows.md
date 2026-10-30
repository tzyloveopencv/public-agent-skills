# Windows Host

先用 PowerShell `Get-Command adb -All` 确认实际使用的 adb 路径，记录 `adb version`。使用已选路径调用；设备命令显式 `-s SERIAL`。`adb devices -l` 可能启动 server，不是纯粹的被动观察。

USB 不可见时先区分整机 USB 节点、复合父设备和 ADB 子接口。可使用 `Get-PnpDevice -PresentOnly` 后按已确认实例 ID / VID / PID 过滤；状态与问题码只用于定位，不直接判定驱动根因。保存设备管理器实例路径、硬件 ID、驱动提供者与版本。不要只按友好名称匹配多台同型号设备。

ADB 接口存在但 transport 异常时，再核实 Host adb 版本、server 所属进程和其他 adb 工具是否共用 server。`kill-server` 不是单设备恢复。

需要 USBPcap 时确认安装状态、目标根集线器与设备地址；重新枚举可能改变地址。限制时长与大小，保存抓包开始/故障时间。抓包过滤器必须符合实际链路，不能把抓不到目标流量当作没有传输。

先比较描述符和接口绑定，再考虑驱动重装；重装、禁用设备或拔插前保存现场并确认授权。
