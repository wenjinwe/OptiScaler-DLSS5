# Changelog

## v1.4.40（2026-10-08）— 三轮解析-修复循环（同版本优化，DLL 基座零改动）

**第一轮 · 脚本层 4 处修复 + 换行标准化**
- runtime_sync.ps1 路径 bug：nvngx 三组件路径改 StreamlineDir + 旧布局兼容回退；
- Check_DLSS_Runtime.bat 清除两行英文残留；
- switch_nr_precision.bat 全局替换改限定 [DlssNr] 区（其他区零误改）；
- Check/switch 内嵌单引号路径改环境变量传递（防特殊字符注入）；
- 9 个 bat/ps1 换行统一 CRLF。

**第二轮 · 运行冒烟 + 键表交叉验证**
- Check 冒烟 exit 0：中文标题 + 包内组件版本速查正常（Streamline 2.14.1 / 16 组件）；
- switch 冒烟：选 2 → [DlssNr] Precision=4；选 1 → 恢复 0；
- DLL 键表 12 键名全被基座识别（无无效键）；汉化串 UTF-8 全在位（无回退）。

**第三轮 · 文档一致性 + 禁止字样清理**
- 使用说明两处第三方作者人名去除；必看说明「汉化 bug」→「bug」；
- 版本号脚本统一 v1.4.40。

- 验证：159 文件 / 419.3MB；SHA256SUMS 158 条；zip SHA256 `D0226104…`；DLL 基座零改动（1E386371…）。

## v1.4.39（2026-10-08）— 安装器 `& goto` 陷阱修复 + DX11 键补全

- setup_windows.bat 两处 `& goto` 陷阱修复：GPU 选择块与注入文件选择块原 `if ... set ... & goto` 写法使 goto 无条件执行（任意非空输入直接跳过判断，INJFILE 可能为空、无效输入不重输、AMD 选项错位）；改为逐条 if 匹配 + `if not defined ... goto 重输` 正确逻辑（全文件 ` & goto` 残留 0）；
- ini `[Hooks]` 段补 `D3D11FeatureLevelElevation=auto`（0.1.27.1 引入的 DX11 设备错误修复键：启动因设备错误失败的 DX11 游戏可设 false 停用 FeatureLevel 提升，否则保持 auto 开启）；
- ini 换行规范化：整体恢复 CRLF（1973 行）；
- 158 文件 / 438.13MB；zip SHA256 `A98916ED…`；DLL 基座零改动（1E386371…）；SHA256SUMS 全部核验。

## v1.4.38（2026-10-08）— 8 脚本全量审查 + UI 大小默认自动

- 3 bat + 5 ps1 逐行全量审查（~1596 行）零 bug：注入件 OriginalFilename 校验完备、清单门控与路径加固在位、get_streamline 四重防护（SHA256 + Authenticode + 白名单 + 目录限制）、runtime_sync 仅清临时文件且保护 Legacy/Unknown SL、零网络外联/零用户数据读写；
- UI 大小默认自动：MenuWidth/Height=auto + Scale=auto（<900p 自动缩小），可手动固定像素值；使用说明 UI 指南同步；
- 158 文件 / 417.83MB；DLL 基座零改动（147f3738）；SHA256SUMS 0 不符。

## v1.4.37（2026-10-07）— 清单门控 + 路径加固

- 安装清单按 UNALL 门控写入卸载器 4 件（此前无条件写入，复制失败也记录）；
- 卸载器清单条目路径安全加固（findstr 拒绝 `..` 与盘符冒号，异常条目 [跳过]）。

## v1.4.36（2026-10-07）— 深度精简定稿

- 合并重复功能与代码：FSR4 替换件 5→2 版（0.2d + 1.1b）、dlssg_unlock 3101 删除（与 3109 重复）、可选分包取消（单包全功能）；
- 158 文件 / 417.83MB（zip l6）；SHA256SUMS 157 行 0 不符。

## v1.4.34 – v1.4.35（2026-10-07）— 组件集成 + 脚本解析

- standalone 组件集成（nvngx.ini 并入主线）；D3D11FeatureLevelElevation 等 F5 线可用修复并入；
- 安装器/卸载器/运行库同步脚本全面解析与优化。

## v1.4.31 – v1.4.33（2026-10-06）— 代码优化 + 冲突修复

- 子串冲突修复（短串不再覆盖长串/已译串）；DLL UI 区 2231 条全覆盖确认；
- 安装器块内 goto 闪退修复（v1.4.33 发布）；REFramework 注入指南补充。

## v1.4.28 – v1.4.30（2026-10-06）— 全面查 bug（六维审查）

- 版本线六维审查（兼容/稳定/准确/安全/实用/可靠）全绿；
- 帧生成专项：后端识别 + Streamline/NGX 能力识别 + 回退机制；内置 MFG 解锁（20/30 系 4X）；
- 画质保护基线固化进 ini 尾部注释块；全局铁律更新（含个人隐私保护）。

## v1.4.25 – v1.4.27（2026-10-06）— 特制构建吸收 + 神经渲染补译

- 吸收 Juij 特制构建优点；神经渲染菜单补译；人物脸部渲染调节修复；
- FSR 4.1.1b INT8 实验模式说明；5X/6X 倍率协商与运行时状态判断优化说明。

## v1.4.20 – v1.4.22（2026-10-06）— 神经渲染基座线

- DLSSNR-F5 基座 0.1.27 重建汉化（2231 处 UI 串全量覆盖）；
- v1.4.22 组装 DLSSNR 基座线；UI 神经渲染区对比集成优化。

## v1.4.17 – v1.4.19（2026-10-06）— 安装/卸载器优化

- 数字键选择、安装器块内 goto 闪退修复；
- v1.4.19 卸载防误删：删除前校验 OriginalFilename='OptiScaler.dll'，拒绝路径穿越（.. / 盘符冒号），F 分支防御性跳过 OptiScaler.ini/fakenvapi。

## v1.4.8 – v1.4.16（2026-10-06）— 补译系列

- 每版按漏译扫描补译 UI 串（累计 100+ 处，含长说明、独立标签、DLSSNR UI、神经渲染菜单）；
- v1.4.12 切换 40serial-MFG 基座；UI 大小调整轮完成菜单适配。

## v1.4.7（2026-10-06）— UI 美化基线

- 基准蓝主题（AccentColor 0.20/0.44/1.00）、深蓝黑背景、微软雅黑 17.0、FPS 悬浮窗七模式；
- 窗口可缩放、主题自动保存、轻量过渡动画。

## v1.4.6（2026-10-06）— 可选增强组件解析与文档化

- 解析 bygalacos dev 线新构建 899b9488（无神经渲染，不替代基座）；
- 组件查重结论：D3D12Core.dll + OptiPatcher.asi 包内已含（上游通用），本轮完整解析 + 文档化（体积 +0）；
- D3D12Core.dll（3.2MB）：DX12 Agility SDK 升级 → Win10 老游戏（赛博朋克 2077 等）启用 FSR4；启用 FsrAgilitySDKUpgrade=true，回退 auto；
- OptiPatcher.asi（102KB）：ASI 插件，由 OptiScaler 加载；启用 LoadAsiPlugins=true，回退 auto；
- 两组件默认不启用，启用/回退写入 OptiScaler.ini 尾部注释块；91 文件 / 392.8MB 不变。

## v1.4.5（2026-10-06）— 全面解析 + 合并重复 + 精简体积（-46%）

- 全面解析：DLL 占 95%，无字节级重复，冗余在功能重叠组件；
- 精简（均保留回退路径）：NR 默认切回官方原版 310.8（Lecram 性能版移出，需 20% 提升从原包找回）；FSR4 替换件 5→2 版（0.2d + 1.1b）；dlssg_unlock 3101/3109→3109；docs 清理 ~600KB；
- 体积：997MB→694.5MB（RAW，-30%）；121→91 文件；zip level9 392.8MB（-46%）。

## v1.4.1（2026-10-05）— XeFG + SM + FSR4 替换件集成

- 新增 dlssg_unlock_3101 备用（早期稳定版，与 3109 二选一）；
- 新增 FSR4 自定义替换件 5 版（非 RDNA3/4 显卡可用 FSR4：4.0.2 / 4.0.2b / 4.0.2c / 4.0.2d / 4.1.1b，PE 结构 + 行为特征审查通过）；
- 其余 109 文件与 v1.4.0 逐字节一致（基座/汉化/19 键预设不变）。

## v1.4.0（2026-10-05）— XeFG+SM 集成版

- 组件集成：新增 dlssg_unlock_3109（RTX 20/30 系 DLSSG 解锁，310.9 驱动版，2X~6X）；新增 sm_unlock 家族（Smooth Motion 解锁：616_92 驱动版 / 通用版 / SM86 专用）；
- 基底 v1.3.0 + 19 键 XeFG 性能预设（均衡 16 + 激进 3）；DLL 基座零改动；
- 集成前核验基座支持性（smooth/dlssg_sm86 引用串），libxess_fg 已含不重复集成；
- 109 文件 / 781MB；zip 完整性、DLL 哈希、19 键回读、5 新组件全部验证通过。

## v1.3.1（2026-10-05）— XeFG 性能优化预设

- 均衡档（默认，低风险）：日志关写盘+仅错误+异步（LogToFile=false/LogLevel=4/LogAsync=true）；帧节奏 Tuning A（FPTSafetyMarginInMs=0.75 / FPTVarianceFactor=0.1，平滑优先改善 1% Low）；最小生成帧队列（AllowedFrameAhead=1）；XeSS 管线/堆预构建 + 预编译着色器；ValidNow 系列关闭省显存；
- 激进档（可选）：UseMutexForSwapchain=false（省锁竞争）、ForceReflex=2、FramerateLimit=0；
- 代码级边界如实标注（倍率预热/资源传输热路径/动态负载感知需上游实现）。

## v1.3.0（2026-10-05）— Lecram NR 模型

- NR 模型替换为 Lecram 调优版（f95feb54…，号称 20% 提升）；原模型同包备份 nvngx_dlssnr_orig.dll（e16bcf15…）可回退；
- 代码节 0 差异（纯 .data 权重调优），PE 时间戳/checksum 一致；
- 其余 101 文件与 v1.2.0 逐字节一致。

## v1.2.0（2026-10-05）— 神经渲染基座

- 基座升级 OptiScaler v0.1.26-final（6d2189f1）（神经渲染深度分支，26,933,760 B）；
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
