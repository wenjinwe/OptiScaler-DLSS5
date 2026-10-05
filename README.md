# OptiScaler-DLSS5

**OptiScaler 集成重构版（DLSS5 全家桶）——跨 GPU 游戏画质增强工具整合包**

基于 **OptiScaler v0.1.26-final（F5 DLSSNR 深度分支）** 重构：998 条中文汉化词典 + 组件全家桶整合 + XeFG 性能预设 + 安全验证。适合 NVIDIA / AMD / Intel 全系显卡，在支持 DLSS/FSR/XeSS 或原生无超分的游戏中启用**超分 / 帧生成 / 神经渲染**。

> 本项目为文档 + 配置仓库；成品整合包（含二进制组件）经 Releases 分发，文本资产（配置、汉化规范、使用说明）在本仓库维护。

---

## 特性

| 类别 | 内容 |
| --- | --- |
| 超分辨率 | DLSS / FSR 3.1 / XeSS / 原生直通（跨 GPU） |
| 帧生成 | DLSSG / XeFG（XeSS FG）/ FSR3-FG / DLSS Enabler / OptiFG |
| 多帧生成（MFG） | 2X~6X 倍率（RTX 20/30/40/50 系，含老卡解锁） |
| 神经渲染（NR） | DLSSNR 神经网络渲染 + 曝光/白点校准 + 模型预设（N 卡 RTX 20+） |
| 平滑运动（SM） | NVIDIA Smooth Motion 解锁（sm_unlock 家族，616.92 驱动版） |
| 显卡伪装 | fakenvapi（AMD/Intel 伪装 NVIDIA，跑 DLSS） |
| 汉化 | 998 条 UI 串中文汉化（UTF-8 等长替换，豆姐/豆包风格术语） |
| 性能预设 | XeFG 19 键优化（均衡/激进两档，日志降噪 + 帧节奏 Tuning） |

## 快速开始

1. 下载 Releases 中的整合包（如 OptiScaler-集成重构版-v1.4.0-XeFG+SM集成.zip）；
2. 将压缩包内 OptiScaler 文件夹整体复制到游戏运行程序所在目录；
3. 进入游戏，按 Insert 呼出菜单面板，按需配置超分/帧生成；
4. 详细说明见 使用说明.md、Config.md。

## 组件清单（v1.4.0）

```
OptiScaler/
├── OptiScaler.dll / dxgi.dll       # 主程序（汉化版，UTF-8 等长替换）
├── OptiScaler.ini                  # 配置（XeFG 19 键预设）
├── nvngx_dlss.dll / dlssd / dlssg  # DLSS 超分/去噪/帧生成（Streamline 全家桶）
├── nvngx_dlssnr.dll                # DLSSNR 神经渲染模型（Lecram 调优版，可回退 orig）
├── libxess.dll / libxess_fg.dll    # XeSS 超分 / XeSS 帧生成后端
├── fakenvapi.dll                   # 显卡伪装
├── dlssg_sm86/                     # DLSSG SM86 解锁（MaxGeneratedFrames=5 → 6X）
├── dlssg_unlock_3109/              # RTX 20/30 系 DLSSG 解锁（310.9 驱动版）
├── sm_unlock/                      # Smooth Motion 解锁（616_92 / 通用 / SM86 专用）
└── streamline/                     # Streamline SDK 全家桶（sl.* + nvngx_*）
```

## 许可与版权

- 本仓库文档/配置：随上游采用 GPL-3.0（见 LICENSE）；
- 组件版权归原作者：OptiScaler（GPL-3.0）、NVIDIA Streamline/DLSS（专有，随游戏分发）、Intel XeSS（专有）、AMD FidelityFX（MIT）、dlssg_unlock/sm_unlock（第三方开源，见各自目录）；
- 汉化与重构仅为学习交流，请遵守各组件许可；禁止任何渠道付费售卖本整合包。

## 参考与致谢

- 上游：OptiScaler（F5 DLSSNR 分支）
- 构建参考：OptiScalerBuilder、OptiScaler-Aurora
- 汉化基准：汉化基准规范.md（v1.17，豆姐/豆包风格术语表 + 等长替换技术 + 安全验证流程）
