# DWC3 深入诊断

只有已确认使用 DWC3 且上层证据指向控制器/传输链时进入。先确定内核版本、厂商提交及补丁；符号、tracepoint 和 debugfs 路径以该源码与运行环境为准。

把 Host URB、gadget request、端点方向、queue/completion、复位/断连事件放到同一时间线上。USB IN/OUT 以 Host 为参照。短包、取消、复位中的错误码需结合上下文；没有 completion 日志可能是采集缺失，不能直接判定硬件卡死。

若已有 TRB、DMA、IOMMU 或 IRQ 证据，关联请求身份、DMA 地址、长度、端点、状态与回收过程。不能仅凭某个 poison 值推断 use-after-free，不能把另一内核分支的修复直接回移。

新增 trace / dynamic debug 必须先确认版本支持、采集开销、容量和停止条件。避免全量长期打开。寄存器读取也可能有副作用，只使用当前平台已确认安全的调试接口；不猜地址。

实验补丁一次验证一个假设，保留原始证据和补丁身份。报告复现条件、次数、失败次数和观察窗口；有限次数未复现写明统计范围。

来源：https://docs.kernel.org/driver-api/usb/gadget.html
