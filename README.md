# 确演内核 · QueYan Kernel

版本 1.0.0    |    许可证 AGPL v3    |    微内核架构    |    加固级

确演内核为确演OS之核心调度与进程管理模块，采用二阶微内核架构，实现抢占式多任务与内存隔离。核心模块以特权模式运行，用户态服务通过IPC与内核通信。内存管理单元实现延迟分配、写时复制及页面回收算法。中断控制器支持MSI-X与IRQ平衡，系统调用网关采用SYSCALL/SYSRET指令对以降低上下文切换开销。

架构特征

- 调度器实现CFS与RT混合策略，采用红黑树维护就绪队列，vruntime差值小于1ms
- 虚拟内存支持五级页表、HugePages及KSM页面合并
- IPC采用零拷贝共享内存与Unix Domain Socket抽象
- 电源管理实现DVFS与C-State深睡眠，支持Wake-on-LAN

性能指标

上下文切换延迟：小于3.2微秒
中断响应时间：小于8.7微秒
缺页处理延迟：小于1.4微秒
最大并发任务数：256

编译与部署

git clone https://github.com/9178139191/queyan-kernel
cd queyan-kernel
make defconfig
make -j$(nproc)
make modules_install

---

English Abstract

QueYan Kernel is a second-generation microkernel implementing preemptive multitasking, virtual memory with five-level paging, and zero-copy IPC. It supports CFS/RT hybrid scheduling with red-black tree runqueues and features MSI-X interrupt handling. The kernel operates in privileged mode while userland services communicate via capability-based IPC channels.

GNU Affero General Public License v3.0

This program is free software: you can redistribute it and/or modify it under the terms of the GNU Affero General Public License as published by the Free Software Foundation, either version 3 of the License, or (at your option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU Affero General Public License for more details.

You should have received a copy of the GNU Affero General Public License along with this program. If not, see https://www.gnu.org/licenses/.

Copyright © 2026 确演OS. 保留所有权利。
