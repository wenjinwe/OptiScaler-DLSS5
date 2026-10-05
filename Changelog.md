# Changelog

## v1.4.0（2026-10-05）— XeFG+SM 集成版

- 组件集成：新增 dlssg_unlock_3109（RTX 20/30 系 DLSSG 解锁，310.9 驱动版，2X~6X）；新增 sm_unlock 家族（Smooth Motion 解锁：616_92 驱动版 / 通用版 / SM86 专用）；
- 基底 v1.3.0 + 19 键 XeFG 性能预设（均衡 16 + 激进 3）；DLL 基座零改动；
- 集成前核验 F5 基座支持性（smooth/dlssg_sm86 引用串），libxess_fg 已含不重复集成；
- 109 文件 / 781MB；zip 完整性、DLL 哈希、19 键回读、5 新组件全部验证通过。

## v1.3.1（2026-10-05）— XeFG 性能优化预设

- 均衡档（默认，低风险）：日志关写盘+仅错误+异步（LogToFile=false/LogLevel=4/LogAsync=true）；帧节奏 Tuning A（FPTSafetyMarginInMs=0.75 / FPTVarianceFactor=0.1，平滑优先改善 1% Low）；最小生成帧队列（AllowedFrameAhead=1）；XeSS 管线/堆预构建 + 预编译着色器；ValidNow 系列关闭省显存；
- 激进档（可选）：UseMutexForSwapchain=false（省锁竞争）、ForceReflex=2、FramerateLimit=0；
- 代码级边界如实标注（倍率预热/资源传输热路径/动态负载感知需上游实现）。

## v1.3.0（2026-10-05）— Lecram NR 模型

- NR 模型替换为 Lecram 调优版（f95feb54…，号称 20% 提升）；原模型同包备份 nvngx_dlssnr_orig.dll（e16bcf15…）可回退；
- 代码节 0 差异（纯 .data 权重调优），PE 时间戳/checksum 一致；
- 其余 101 文件与 v1.2.0 逐字节一致。

## v1.2.0（2026-10-05）— F5 DLSSNR 基座

- 基座升级 OptiScaler v0.1.26-final（6d2189f1）（F5 DLSSNR 深度分支，26,933,760 B）；
- 汉化 995 处（871 等长替换 + 124 超长精修），全文件 diff 仅在 UI 字符串区；
- 补齐 streamline 全家桶（含 NR 大模型 165.8MB）、fakenvapi、OptiPatcher、dlssg_sm86、nvfp4、nvsmooth30 等 46 项组件；103 文件 / 591MB。

## v1.1.0（2026-10-05）— v97e99b4c 基座

- 基座升级 v10.0.0-dev（97e99b4c）；汉化词典 445 条平移 + 组件补齐 60 文件 / 430MB。

## v1.0.0（2026-10-05）— 集成重构版首发

- 整目录扫描全部 OptiScaler 源包，选定 v97 dev 为基座；
- 组件整合（Streamline / XeSS / FSR / 老卡解锁 / 伪装 / 注入）；
- 规范第十五章《整目录扫描与集成重构构建》建立。

---

*变更记录与 汉化基准规范.md 同步演进。*
