# Features — 功能总览
> 基于神经渲染基座（0.1.31 光学 F5Low，DLL 哈希 ecafed90）+ v1.4.53 组件整合（232 文件 / 539.6MB）。以下功能对应菜单项与配置键。
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
| MFG 多帧 | 2X~6X：InterpolationCount + UnlockMFG + 解锁组件 |
- 倍率档位：2x / 3x / 4x / 5x / 6x（5x - Enabler、6x - FFX + Enabler 等）；
- **解锁组件（v1.4.51–53，多方案二选一）**：内置 dlssg_sm86（SM86 架构 4X）、dlssg_unlock_3109（RTX 20/30 系 310.9 驱动版）、MFGUnlocker 插件位（plugins/MFGUnlocker.asi，LoadAsiPlugins=true，开箱即用）、DLSSG6X 独立组件（winmm.dll + dlssg_sm86 + ini，20/30 系 6X 独立部署）；
- 内置 MFG 解锁：[DLSSG] AmpereMfgUnlock=true（RTX 20/30 系 4X）。
## 三、神经渲染（NR）
- N 卡 RTX 20+；菜单：启用神经网络渲染；
- **光学 F5Low**（0.1.31 基座）：无升频器游戏中的 DLSS-NR 独立成页；帧生成提速（NativeUpscalerPass 开启时后端不再跑超分遍，NR 直接作用于游戏原画面）；
- **Look Presets 外观预设**（0.1.31 新）：原生 / 自然 / 电影感 / 仅细节 / 人物 / 绘画感 / 柔画布 / 结构感 8 档 + Built on 基底；
- **曝光默认随游戏**（0.1.31 新）：NR 输入页五档来源（自动 / 手动纸白 / 游戏曝光 / 扫描曝光 / 自动曝光），无效控件自动置灰；
- F5Low 低延迟：无 Reflex 游戏 NVIDIA 卡自动装 NVIDIA Reflex，其他经 fakenvapi 装 Anti-Lag 2 / XeLL / LatencyFlex；
- 计算精度三模式：自动 / 标准精度 / FP8，用 `switch_nr_precision.bat` 切换（[DlssNr] Precision=0/1/4）；
- 模型：官方原版（默认，合规不损画质）；**nvngx_dlssnr.dll 不随升级替换**（需要时用户自行手动替换）。
## 四、低延迟
- **低延迟统一层（0.1.31 新）**：帧率页「输出」新增 FrameCapOnly（仅限帧数：把 FPS 上限等待移到游戏读取输入前），与 Reflex / Anti-Lag 2 / XeLL / LatencyFlex 并列可选；
- Reflex：ForceReflex=2（[fakenvapi] 段）；
- Smooth Motion 解锁（v1.4.0）：sm_unlock 家族——616.92 驱动版（推荐）/ 通用版 / SM86 专用；
- BackBuffer 同步：PreserveSwapChain / SkipResizeBuffers（减少 FG 自动失效）。
## 五、兼容与伪装
- 显卡伪装（fakenvapi）：AMD/Intel 伪装 NVIDIA 以启用 DLSS（默认开启，异常设 Dxgi=false）；
- Vulkan：Vulkan AntiLag / 超分路径（VulkanUpscaler / VulkanExtensionSpoofing）；
- 老卡 MFG 解锁：SM75/SM86（Enable SM86/SM75 MFG (experimental; restart)）；
- Streamline 能力识别：[FrameGen] StreamlineIgnoreOTA=true（只用包内 streamline 全家桶，忽略驱动 OTA 缓存）；
- DX11 设备错误修复：[Hooks] D3D11FeatureLevelElevation=auto；
- **Load ASI plugins 复选框（0.1.31 新）**：插件位开关（[Plugins] LoadAsiPlugins，配套 MFGUnlocker.asi / OptiPatcher.asi）；
- 注入链版本一致：dxgi.dll（注入器）与 OptiScaler.dll（核心）尺寸/SHA 必须一致。
## 六、可选增强组件
- D3D12Core.dll（D3D12_OptiScaler\）：DX12 Agility SDK 升级 → Win10 老游戏启用 FSR4；启用 FsrAgilitySDKUpgrade=true；
- plugins/OptiPatcher.asi：ASI 插件，由 OptiScaler 加载（仅名单内游戏生效）；
- ReShade（0.1.31 新）：可作 d3d12-ReShade64.dll 与 OptiScaler 并列使用；
- 两者默认不启用，回退改回 auto。
## 七、UI 与工具
- 菜单面板：Insert 呼出；Page Up 关闭叠加层；
- 调试视图：帧率叠加层、运动矢量/深度可视化（DebugView 系列）；
- 组件即插即用：dlssg_unlock / sm_unlock / DLSSG6X 为独立替换件，复制到游戏目录使用，异常即删即恢复；
- 运行库检查：`Check_DLSS_Runtime.bat` 输出包内组件版本速查；
- 精度切换：`switch_nr_precision.bat` 数字键切换 NR 计算精度。
---
*功能与 Config.md、Changelog.md 对应。*
