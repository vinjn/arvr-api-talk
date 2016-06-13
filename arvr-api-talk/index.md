## 浅析 Vulkan 对 AR / VR 的影响
Vinjn张静 [@github](https://github.com/vinjn) / [@zhihu](https://www.zhihu.com/people/vinjn) / [mail](mailto:vinjn.z@gmail.com)
========
### Vulkan
* Vulkan 介绍
* 为什么重新造轮子？
* How
========
### What is Vulkan?
![](media/vulkan-icon.png)
========
### 背景故事
* 2012 年 10 月，成立 GL Common TSG 重新设计 OpenGL / ES。
* 2014 年 6 月，项目重启，改名为 GL Next，高优先级。
* 2015 年 GDC，重命名为 Vulkan。
* 2015 年 2 月，正式发布。
========
### Vulkan 是为今后 20 年准备的图形 API
* 逻辑上，是 OpenGl / OpenGL ES 的后继者
* 现代、高效的设计
* 开放的工业标准
========
### 和 OpenGL 是不同的
* 设计哲学上本质的改变
* 需要应用开发者做出相应改变
========
### 为什么重新造轮子，OpenGL 出了什么问题？
========
### 25 年前 OpenGL 被发明了
![](media/gpu-server.png)
========
### GPU 逐渐移动化、多核化
![](media/gpu-mobile.png)
========
### GPU 被用于各种领域（图像、计算、视觉、深度学习等等）
![](media/gpu-everywhere.png)
========
### 问题1. OpenGL 编程模型与 GPU 硬件不一致
* 尤其在移动端
* 被驱动的黑魔法隐藏
========
### 问题2. 驱动工作量过大
* 大量的状态检验
* 资源依赖跟踪
========
### 问题3. 驱动不稳定
* 逻辑复杂
* 大量 bug
* 难以预测的行为
* 每个 GPU 都有不同的 bug
* 每个 GPU 都有自己推荐的编程方式
========
### 问题4. 单线程
* 需要创建 context
* context 需要和线程绑定
* 无法高效利用多核 CPU
========
### 对硬件的直接控制
* 你需要做什么？
* 驱动会做什么?
========
### 你需要
* 在何时的时间
* 告诉 Vulkan 驱动你打算做什么
* 提供足够的细节
* 驱动不需要猜测
========
### OpenGL 则允许你
* 在任意时间提供重要信息
* 在任意时间改变这些信息
* 方便，但是严重影像 GPU 性能
========
### 相应的，Vulkan 驱动保证会
* 在你让它工作时
* 做该做的事情
========
### OpenGL 驱动则
* 会延迟工作
* 将工作转移给另一个线程
* 甚至基于它对你对猜测，无视你的命令
========
### Vulkan 的编程模型（简化版）
* Instace
    * PhysicalDevice
        * Device
            * Resources (Image, Buffer)
            * Memory
            * Queue
            * Command Buffer
========
### Queue, Command Buffer
![](media/vulkan-threading.png)
========
### Vulkan 工作组成员
![](media/vk-who.png)
========
### 整个行业的努力
* GPU 和 SoC 供应商
* 游戏开发商
* 引擎和工具开发商
* 平台
* 内容提供商
========
### Vulkan 的生态圈是开放的
* [https://github.com/KhronosGroup](https://github.com/KhronosGroup)
* Loader
* Validation layer
* SPIR-V 工具
* Conformance 测试集
* Specification
========
### 我对生态圈的贡献
* vktrace
* awesome-vulkan
* vkut
========
### vktrace
* https://github.com/LunarG/VulkanTools/tree/master/vktrace
* Vktrace Trace and Replay Tool
* Vktrace is a Vulkan API tracer for graphics applications.
========
### awesome-vulkan
* https://github.com/vinjn/awesome-vulkan
* 整理互联网上关于 Vulkan 的（几乎）所有公开资源。
    * Hardware Support
    * SDK
    * IHV Document
    * Tutorial
    * Apps
    * Samples
    * Libraries
    * Bindings
    * Tools
========
### vkut
* https://github.com/vinjn/vkut
* The Vulkan Utility Toolkit
========
### Vulkan 对 AR 应用的帮助
* 支持 Compute Shader，可以进行计算机视觉运算
* OpenCV CUDA / OpenCL 模块 -> Vulkan 模块
* 支持异步计算（Async Compute)，充分榨干 GPU 性能
* 省电
========
### Vulkan 对 VR 应用的帮助
* 稳定的帧率、可预测的性能确保流程的 VR 体验
* 多线程的引入使得同屏 drawcall 更多
* 省电
========
### 你是否应该使用 Vulkan?
* 挑战
* 机遇
* 现实
========
### 挑战
* 啰嗦而复杂的编程方式
* 容易伤到自己
* 需要学习一堆新知识
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
