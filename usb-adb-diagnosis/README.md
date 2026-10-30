# USB / ADB 异常诊断

适用于不同 AI agent 的共用诊断资料，覆盖 USB 枚举失败、ADB 接口缺失、offline / unauthorized、卡死、传输停滞和重启或休眠后断连。

## 使用

支持 SKILL.md 格式的 agent：将本目录放到该 agent 支持的技能目录，按其发现机制加载。

其他 agent：先读取 SKILL.md，再按当前现场读取其中链接的参考资料。诊断内容不依赖专用工具 API。

可将 assets/usb-adb-config.example.yaml 复制到项目根目录，命名为 .usb-adb-diagnosis.yaml，并填写环境信息。配置由 agent 阅读，目前没有自动解析器或采集脚本。不配置也可使用。

默认只读诊断。配置中的操作偏好不代替用户授权。`.codex-tmp/usb-adb` 只是可修改的私有产物目录名称，不要求安装 Codex。

已完成文档结构检查，尚未经过真实设备验证。平台参考中不包含未经复核的历史根因。
