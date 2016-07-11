## 新一代图形API Vulkan 对行业的影响
Vinjn张静
========
### README
* GPU 架构师 / Lead @ NVIDIA 上海
* 负责 OpenGL / Vulkan 性能分析工具
* 游戏行业经验（2K Games、Ubisoft、微软 Xbox 部门）
* 技术书籍译者
* [@github](https://github.com/vinjn) / [@zhihu](https://www.zhihu.com/people/vinjn) / [mail](mailto:vinjn.z@gmail.com)
========
### 议程
* Vulkan 介绍
* 为什么重新造轮子？
* 优点
* 展望未来
* Q & A
========
### Vulkan 介绍
![](media/vulkan-icon.png)
========
### 成立的背景
* 2012 年 10 月，成立 GL Common TSG 重新设计 GL / ES，不了了之
* 2014 年 6 月，项目重启，改名为 GL Next，提升优先级
* 2015 年 GDC，重命名为 Vulkan
* 2016 年 2 月，正式发布
========
### Vulkan 是为今后 20 年准备的图形 API
* 是 OpenGL / ES 的替代者
* 现代、高效的设计
* 开放的工业标准
========
#### OpenGL 被发明于 25 年前
#### 昂贵的工作站
#### 单核 CPU
![](media/gpu-server.png)
========
#### GPU 逐渐移动化、多核化
![](media/gpu-mobile.png)
========
#### GPU 被用于各种领域
#### 无人机、计算机视觉、汽车、深度学习等
![](media/gpu-everywhere.png)
========
### 为什么重新造轮子？
### OpenGL 出了什么问题？
========
### 问题：OpenGL 编程模型与 GPU 硬件不一致
* 尤其在移动端
* 被驱动的黑魔法隐藏
========
### 答案: Vulkan 的编程模型接近硬件实现
* Instance
    * PhysicalDevice
        * Device
            * Resources (Image, Buffer)
            * Memory
            * Queue
            * Command Buffer
========
### OpenGL 和 Vulkan 编程模型上的区别
* TODO: 需展开
* Texture
* Buffer
* shader
========
### 问题：驱动工作量过大，不稳定
* 大量的状态检验
* 资源依赖跟踪
* 难以预测的行为
========
### 原因：OpenGL 允许你
* 在任意时间提供重要信息
* 在任意时间改变这些信息
* 方便，严重影响 GPU 性能
========
### OpenGL 驱动则
* 会延迟工作
* 将工作转移给另一个线程
* 甚至基于猜测，无视你的命令
========
### 答案：通过 Vulkan 实现对硬件的直接控制
* 在合适的时间
* 告诉 Vulkan 驱动你打算做什么
* 提供足够的细节
========
### Vulkan 驱动会
* 在你让它工作时
* 做该做的事情
* 不需要猜测
========
### 问题： 单线程
* 需要创建 context
* context 需要和线程绑定
* 无法高效利用多核 CPU
========
### 答案：Queue, Command Buffer
* TODO: 需展开
![](media/vulkan-threading.png)
========
### Vulkan 对 AR、VR、游戏的帮助
* 支持 Compute Shader，可以进行计算机视觉运算
* 支持异步计算（Async Compute)，充分榨干 GPU 性能
* 多线程的引入使得同屏 drawcall 更多
* Android N 引入 Daydream 和 Vulkan，标志着 Vulkan 将应用在安卓 VR 中 
========
### 省电，CPU 端工作量减少
* TODO: 需展开
* 驱动工作量减少
========
### 稳定的帧率、可预测的性能确保流畅的 VR 体验
* TODO: 需展开
========
### 展望未来，你是否应该使用 Vulkan?
* 挑战
* 机遇
* 现实
========
### 挑战
* 啰嗦、复杂的编程方式
* 容易伤到自己
* 需要重新学习知识
========
### 机遇
* 驱动的负担更轻
* 可以通过多线程进一步降低
* 可预测的性能
* 对移动端友好
========
### 现实
* 生态圈还不如 OpenGL 成熟
* 短时间内依然需要发布 GL / DX 版本
========
### Vulkan vs OpenGL / ES
![](media/gl-to-new-api.png)
========
### Vulkan vs DirectX12 vs Metal
![](media/api-platform-support.png)
========
## Q & A
> https://github.com/vinjn/slides
