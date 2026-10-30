# 设备侧 Gadget / adbd / FunctionFS

通过仍可用的 AT/UART/网络通道读取状态；ADB 已卡死时，不把全部采集都依赖该 ADB 链路。Linux Gadget 不一定使用 configfs，也不一定有 systemd 或 Android properties；先从现有启动脚本和挂载确认实现。

按需读取 `uname -a`、`ps`、`/proc/mounts`、`/sys/class/udc`。configfs 已挂载时，定向查看已识别 gadget 的 UDC 属性、configs 中 function 链接及已有 FunctionFS 挂载。不要为观察而创建、删除或重绑 gadget。

关联顺序：adbd 启动 / 打开 FunctionFS → 描述符提交 → function 链接与 UDC 绑定 → Host 枚举 → ADB transport。实际先后受实现影响，须读对应源码/脚本。

FunctionFS ep 文件存在不证明请求持续完成；adbd 进程存在不证明其线程无阻塞。需要时读取特定 PID 的线程状态、wchan 和允许读取的 stack，记录权限限制。打开 ep 文件、strace attach 和动态调试会影响现场，不作为默认被动采集。

ADB authorized 状态用平台支持的正式流程处理，不删除密钥、不关闭鉴权。单个传输方向异常时分别记录 shell、小块读取/写入和已有传输结果；新增 push 会写目标文件，须有授权和指定路径。

来源：
- https://docs.kernel.org/usb/gadget_configfs.html
- https://docs.kernel.org/usb/functionfs.html
- https://android.googlesource.com/platform/packages/modules/adb/+/refs/heads/main/docs/user/adb.1.md
