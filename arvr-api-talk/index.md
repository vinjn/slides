## 浅析下一代 API 对 AR / VR 的影响
> Vulkan, OpenVX 及 glTF

Vinjn张静 [@github](https://github.com/vinjn) / [@zhihu](https://www.zhihu.com/people/vinjn) / [@mail](mailto:vinjn.z@gmail.com)

========
## Vulkan
* What
* Why
* Who
* How
* TODO: img
========
## What
is Vulkan?
----
### 为今后 20 年准备的图形 API
* 逻辑上，是 OpenGl / OpenGL ES 的后继者
* 现代、高效的设计
* 开放的工业标准
----
### 今年的情况
* 今年二月份发布
* Windows / Linux / Android N
* Samgung Galaxy S7
----
### 和 OpenGL 是不同的
* 设计哲学上本质的改变
* 需要应用开发者做出相应改变
========
## Why
为什么重新造轮子，OpenGL 出了什么问题？
----
### 编程模型与 GPU 硬件不一致
* 尤其在移动端
* 被驱动的黑魔法隐藏
----
### CPU 端工作量过大
* 大量的状态检验
* 资源依赖跟踪
----
### 驱动不稳定
* 逻辑复杂
* 大量 bug
* 难以预测的行为
* 每个 GPU 都有不同的 bug
* 每个 GPU 都有自己推荐的编程方式
----
### 单线程
* 需要创建 context
* context 需要和线程绑定
* 无法高效利用多核 CPU
========
## How
* Instace
    * PhysicalDevice
        * Device
            * Resources
            * Memory
            * Queue
            * Command buffers
========
## 对硬件的显示控制
* 你需要做什么？
* 驱动会做什么?
----
### 你需要
* 在何时的时间
* 告诉 Vulkan 驱动你打算做什么
* 提供足够的细节
* 驱动不需要猜测
----
### OpenGL 则允许你
* 在任意时间提供重要信息
* 在任意时间改变这些信息
* 方便
* 但是影像 GPU 性能
----
### 相应的，Vulkan 驱动保证会
* 在你让它工作时
* 做该做的事情
----
### OpenGL 驱动则
* 会延迟工作
* 将工作转移给另一个线程
* 甚至基于它对你对猜测，无视你的命令
========
## 你是否应该使用 Vulkan
* 挑战
* 机遇
* 现实
----
### 挑战
* 啰嗦而复杂的编程方式
* 容易伤到自己
* 需要学习一堆新知识
----
### 机遇
* 驱动的负担更轻
* 可以通过多线程进一步降低
* 可预测的性能
* 对移动端友好
----
### 现实
* 生态圈还不如 OpenGL 成熟
* 依然需要发布 GL / DX 版本

