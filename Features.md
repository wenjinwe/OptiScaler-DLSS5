# Features — 功能总览

> 基于 F5 DLSSNR 基座（v0.1.26-final）+ v1.4.0 组件整合。以下功能对应菜单项与配置键。

## 一、超分辨率（Upscaling）

- DLSS：N 卡 RTX 20+（含超分/去噪/帧生成三件套 nvngx_dlss/d/dg）；
- FSR 3.1 / FSR4：AMD/Intel 卡（amd_fidelityfx 全家桶；FSR4 需 RDNA3+/自定义替换）；
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
- 老卡解锁：dlssg_sm86（SM86 架构，MaxGeneratedFrames=5 → 6X）、dlssg_unlock_3109（RTX 20/30 系，310.9 驱动版）。

## 三、神经渲染（DLSSNR）

- N 卡 RTX 20+；菜单：启用神经网络渲染（默认无快捷键，需自行设置）；
- 曝光/白点校准、模型预设（NetworkModel）、模型精度/通道、HDR 色调映射；
- NR 需要 DX12 桥接（NR needs the D3D12 bridge on D3D11——DX11 游戏请配合超分使用）；
- 模型：Lecram 调优版（v1.3.0 起，f95feb54…）；原版备份 nvngx_dlssnr_orig.dll 可回退。

## 四、平滑运动（SM）与低延迟

- Smooth Motion 解锁（v1.4.0）：sm_unlock 家族——616.92 驱动版（推荐）/ 通用版 / SM86 专用；
- Reflex：ForceReflex / UseGamesReflexMarkers（帧标记补全，改善无原生 FG 游戏）；
- BackBuffer 同步：PreserveSwapChain / SkipResizeBuffers（减少 FG 自动失效）。

## 五、兼容与伪装

- 显卡伪装（fakenvapi）：AMD/Intel 伪装 NVIDIA 以启用 DLSS（默认开启，异常设 Dxgi=false）；
- Vulkan：Vulkan AntiLag / 超分路径（VulkanUpscaler / VulkanExtensionSpoofing）；
- 老卡 MFG 解锁：SM75/SM86（Enable SM86/SM75 MFG (experimental; restart)）。

## 六、UI 与工具

- 菜单面板：Insert 呼出（非标准键盘可改 ShortcutKey）；Page Up 关闭叠加层；
- 调试视图：帧率叠加层、运动矢量/深度可视化（DebugView 系列）；
- 组件即插即用：dlssg_unlock / sm_unlock 为独立替换件，复制到游戏目录使用，异常即删即恢复。

---

*功能与 Config.md、Changelog.md 对应。*
