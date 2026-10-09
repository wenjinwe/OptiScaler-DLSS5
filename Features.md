# Features — 功能总览

> 基于神经渲染基座（0.1.27.2 光学 F5Low，DLL 哈希 0d7475ba）+ v1.4.47 组件整合（159 文件 / 419.3MB）。以下功能对应菜单项与配置键。

## 一、超分辨率（Upscaling）

- DLSS：N 卡 RTX 20+（含超分/去噪/帧生成三件套 nvngx_dlss/d/dg）；
- FSR 3.1 / FSR4：AMD/Intel 卡（amd_fidelityfx 全家桶；FSR4 需 RDNA3+ 或自定义替换件）；
- XeSS：Intel + 跨 GPU（libxess.dll / libxess_dx11.dll）；
- 原生直通（无超分游戏也可启用其他管线）。

## 二、帧生成 / 多帧生成（FG / MFG）

| 后端 | 说明 |
| --- | --- |
| DLSSG | RTX 20/30/40 系原生（streamline/nvngx_dlssg.dll） |
| XeFG | XeSS 帧生成（libxess_fg.dll，DX12 游戏；DX11 用 OptiFG 输入） |
| FSR3-FG | amd_fidelityfx_framegeneration（A 卡友好） |
| DLSS Enabler | 无原生 FG 游戏的 DLSSG 桥接（dlss-enabler-headless） |
| OptiFG | 替代帧生成输入（配合 DLSSG 输出） |
| MFG 多帧 | 2X~6X：InterpolationCount + UnlockMFG + 老卡解锁组件 |

- 倍率档位：2x / 3x / 4x / 5x / 6x（5x - Enabler、6x - FFX + Enabler 等）；
- 老卡解锁：dlssg_sm86（SM86 架构，MaxGeneratedFrames=5 → 6X）、dlssg_unlock_3109（RTX 20/30 系，310.9 驱动版）；
- 内置 MFG 解锁（v1.4.2 起）：[DLSSG] AmpereMfgUnlock=true（RTX 20/30 系 4X，与外部解锁件二选一）；AdaMfgUnlock=false（实验性保持）。

## 三、神经渲染（NR）

- N 卡 RTX 20+；菜单：启用神经网络渲染（默认无快捷键，需自行设置）；
- **光学 F5Low**（0.1.27.2 起）：无升频器游戏中的 DLSS-NR 独立成页（F5Low 状态 / Passes 说明 / 曝光 / 自动曝光 / 白点来源 / 校准点 / 模型精度 / 细节重用 / Sigma 下限全套设置）；菜单头一次性提示键 `[Menu] F5LowHint=false`（本包已关闭提示）；
- F5Low 低延迟：无 Reflex 游戏 NVIDIA 卡自动装 NVIDIA Reflex，其他经 fakenvapi 装 Anti-Lag 2 / XeLL / LatencyFlex（默认开启）；
- 曝光新增"原生"起点选项（保持游戏本色）；线性可选作曲线；
- 计算精度三模式（v1.4.40 配置层）：自动 / 标准精度 / FP8，用 `switch_nr_precision.bat` 切换（[DlssNr] Precision=0/1/4），避免错误修改不兼容的 DLSS NR 运行时；
- 模型：官方原版 310.8（默认，合规不损画质）；Lecram 性能版为可选件，需 20% 提升时从原包找回并备份原版；
- 人脸渲染调节（v1.4.27 起）：肤色与人脸区域识别优化，DX11/DX12/Vulkan 同步更新。

## 四、平滑运动（SM）与低延迟

- Smooth Motion 解锁（v1.4.0）：sm_unlock 家族——616.92 驱动版（推荐）/ 通用版 / SM86 专用；
- Reflex：ForceReflex=2（[fakenvapi] 段，DLSSG 所需 Reflex 状态自动补全）；
- BackBuffer 同步：PreserveSwapChain / SkipResizeBuffers（减少 FG 自动失效；仍失效时按需开 ModifyBufferState/ModifySCIndex）。

## 五、兼容与伪装

- 显卡伪装（fakenvapi）：AMD/Intel 伪装 NVIDIA 以启用 DLSS（默认开启，异常设 Dxgi=false）；
- Vulkan：Vulkan AntiLag / 超分路径（VulkanUpscaler / VulkanExtensionSpoofing）；
- 老卡 MFG 解锁：SM75/SM86（Enable SM86/SM75 MFG (experimental; restart)）；
- Streamline 能力识别：[FrameGen] StreamlineIgnoreOTA=true（只用包内 streamline 全家桶，忽略驱动 OTA 缓存）；
- DX11 设备错误修复：[Hooks] D3D11FeatureLevelElevation=auto（启动失败的 DX11 游戏设 false）；
- 注入链版本一致：dxgi.dll（注入器）与 OptiScaler.dll（核心）尺寸/SHA 必须一致（升级后核验）。

## 六、可选增强组件

- D3D12Core.dll（D3D12_OptiScaler\）：DX12 Agility SDK 升级 → Win10 老游戏启用 FSR4；启用 FsrAgilitySDKUpgrade=true；
- OptiPatcher.asi（plugins\）：ASI 插件，由 OptiScaler 加载；启用 LoadAsiPlugins=true；
- 两者默认不启用，回退改回 auto。

## 七、UI 与工具

- 菜单面板：Insert 呼出（非标准键盘可改 ShortcutKey）；Page Up 关闭叠加层；
- 调试视图：帧率叠加层、运动矢量/深度可视化（DebugView 系列）；
- 组件即插即用：dlssg_unlock / sm_unlock 为独立替换件，复制到游戏目录使用，异常即删即恢复；
- 运行库检查（v1.4.40）：`Check_DLSS_Runtime.bat` 输出包内组件版本速查（Streamline 全家桶 / NR 运行时）；
- 精度切换（v1.4.40）：`switch_nr_precision.bat` 数字键切换 NR 计算精度。

---

*功能与 Config.md、Changelog.md 对应。*
