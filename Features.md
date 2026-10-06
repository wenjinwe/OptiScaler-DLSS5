# Features — 功能总览

> 基于神经渲染基座（v0.1.26-final）+ v1.4.6 组件整合（91 文件 / 392.8MB）。以下功能对应菜单项与配置键。

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
- 老卡解锁：dlssg_sm86（SM86 架构，MaxGeneratedFrames=5 → 6X）、dlssg_unlock_3109（RTX 20/30 系，310.9 驱动版，v1.4.5 起为默认单一版本）；
- 内置 MFG 解锁（v1.4.2 起）：[DLSSG] AmpereMfgUnlock=true（RTX 20/30 系 4X，与外部解锁件二选一）；AdaMfgUnlock=false（实验性保持）。

## 三、神经渲染（NR）

- N 卡 RTX 20+；菜单：启用神经网络渲染（默认无快捷键，需自行设置）；
- 曝光/白点校准、模型预设（NetworkModel）、模型精度/通道、HDR 色调映射；
- NR 需要 DX12 桥接（NR needs the D3D12 bridge on D3D11——DX11 游戏请配合超分使用）；
- 模型：官方原版 310.8（v1.4.5 起默认，合规不损画质）；Lecram 性能版已移出，需 20% 提升时从原包 nvngx_dlssnr_310.8.Lecram zip 找回并备份原版。

## 四、平滑运动（SM）与低延迟

- Smooth Motion 解锁（v1.4.0）：sm_unlock 家族——616.92 驱动版（推荐）/ 通用版 / SM86 专用；
- Reflex：ForceReflex=2（v1.4.4 起，[fakenvapi] 段，DLSSG 所需 Reflex 状态自动补全）；
- BackBuffer 同步：PreserveSwapChain / SkipResizeBuffers（减少 FG 自动失效；仍失效时按需开 ModifyBufferState/ModifySCIndex）。

## 五、兼容与伪装

- 显卡伪装（fakenvapi）：AMD/Intel 伪装 NVIDIA 以启用 DLSS（默认开启，异常设 Dxgi=false）；
- Vulkan：Vulkan AntiLag / 超分路径（VulkanUpscaler / VulkanExtensionSpoofing）；
- 老卡 MFG 解锁：SM75/SM86（Enable SM86/SM75 MFG (experimental; restart)）；
- Streamline 能力识别（v1.4.2）：[FrameGen] StreamlineIgnoreOTA=true（只用包内 streamline 全家桶，忽略驱动 OTA 缓存）。

## 六、可选增强组件（v1.4.6 文档化）

- D3D12Core.dll（D3D12_OptiScaler\，3.2MB）：DX12 Agility SDK 升级 → Win10 老游戏（赛博朋克 2077 等）启用 FSR4；启用 FsrAgilitySDKUpgrade=true；
- OptiPatcher.asi（plugins\，102KB）：ASI 插件，由 OptiScaler 加载；启用 LoadAsiPlugins=true；
- 两者默认不启用，回退改回 auto；启用/回退说明见 OptiScaler.ini 尾部注释块。

## 七、UI 与工具

- 菜单面板：Insert 呼出（非标准键盘可改 ShortcutKey）；Page Up 关闭叠加层；
- 调试视图：帧率叠加层、运动矢量/深度可视化（DebugView 系列）；
- 组件即插即用：dlssg_unlock / sm_unlock 为独立替换件，复制到游戏目录使用，异常即删即恢复。

---

*功能与 Config.md、Changelog.md 对应。*
