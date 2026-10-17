<div align="center">

# OptiScaler-DLSS5

**OptiScaler 集成重构版 —— 跨 GPU 游戏画质增强工具整合包**

**简体中文**

[![集成重构版 v1.4.56](https://img.shields.io/badge/集成重构版-v1.4.56-76b900?style=flat-square)](https://github.com/wenjinwe/OptiScaler-DLSS5/releases)
![基座 0.1.31](https://img.shields.io/badge/基座-0.1.31-7c3aed?style=flat-square)
![汉化 1900+](https://img.shields.io/badge/汉化-1900%2B处-2563eb?style=flat-square)

**[下载 v1.4.56](https://github.com/wenjinwe/OptiScaler-DLSS5/releases) · [更新记录](Changelog.md) · [已知问题](Issues.md)**

</div>

集成重构版是基于 [OptiScaler](https://github.com/optiscaler/OptiScaler) 及社区分支开发的免费整合包，提供超分辨率替换、帧生成、多帧生成、神经渲染与平滑运动等跨 GPU 画质增强能力，并全面汉化 UI、自带安装卸载器与运行库同步。它是社区版本，不是 OptiScaler、NVIDIA、AMD 或 Intel 的官方发行版。

## 主要功能

| 功能 | 说明 |
| --- | --- |
| 超分辨率 | DLSS / FSR 3.1 / FSR4 / XeSS / 原生直通，跨 NVIDIA / AMD / Intel GPU |
| 帧生成 | DLSSG / XeFG（XeSS FG）/ FSR3-FG / DLSS Enabler / OptiFG |
| 多帧生成（MFG） | 2X~6X 倍率链；RTX 20/30 系内置解锁（4X，纯配置）+ MFGUnlocker 插件位 + DLSSG 独立组件（含 6X）；高倍率失败自动回退 |
| 神经渲染（NR） | 光学 F5Low 独立页 + Look Presets 外观预设 + 曝光/白点校准 + 模型精度/多遍数（RTX 20+） |
| 平滑运动（SM） | NVIDIA Smooth Motion 解锁（sm_unlock 家族） |
| 显卡伪装 | fakenvapi（AMD/Intel 伪装 NVIDIA 运行 DLSS） |
| 汉化与 UI | 约 1900+ 处 UI 串中文化（UTF-8 等长替换）；基准蓝主题、窗口可缩放、主题自动保存、FPS 悬浮窗七模式 |

## 快速开始

1. 从上方发行页下载最新整合包并解压；
2. 将解压目录**全部文件**复制到游戏运行程序（.exe）所在目录；
3. 运行 `setup_windows.bat`，按数字键选择加载入口（一般 `dxgi.dll` 即可）；
4. 启动游戏，按 `Insert` 打开面板，先确认基础功能正常，再逐项调整帧生成与神经渲染。

安装完成后建议先运行 `Check_DLSS_Runtime.bat` 检查运行库状态；详细步骤、更新与卸载见成品包内 `INSTALL-DLSSNR.md` 与 `使用说明.txt`。

## v1.4.56 要点

- **UI 汉化三轮深扫（累计 21 处补译）**：截图驱动 7 处（导航 Image→图像、Input→输入；底部 Close→关闭、开 Wiki→开维基；垂同区 垂直同步设→垂直同步、垂同开→垂直开、垂同关→垂直关）→ 枚举类 13 处（日志级 Error→错误、Info→信息；底部 自(1.4)→自动(1.4)；外观 明亮/强烈/人脸；比较 擦除/缩放；引擎 其他；曝光 高/自定义；背景 完整）→ 一致性补译 Watercolour→水彩；文件尾未扫区 986KB 全扫 0 漏译；
- **质量闭环**：全量回读 24/24 OK、映射表 1345 条、SHA256SUMS 同步；DLL SHA12=`3af21dabc309`；
- **重打包**：218 文件 / 520MB，zip↔目录 218/218 匹配 0 多余。

## 文档与反馈

- [更新记录](Changelog.md) · [功能总览](Features.md) · [配置说明](Config.md) · [已知问题](Issues.md) · [显卡伪装](Spoofing.md)。
- [提交问题](https://github.com/wenjinwe/OptiScaler-DLSS5/issues)：请附版本、游戏、显卡/驱动、加载入口、FG 输入/输出、复现步骤与日志。

## 开源与致谢

感谢 [OptiScaler](https://github.com/optiscaler/OptiScaler)、神经渲染社区分支（Dagherbou / janblade / wilsjo2）及相关组件贡献者；构建参考 [OptiScalerBuilder](https://github.com/bygalacos/OptiScalerBuilder)、[OptiScaler-Aurora](https://github.com/abc354402600/OptiScaler-Aurora)。

项目使用 [GPL-3.0](LICENSE)；各随附组件依照各自许可证。整合包为社区学习交流用途，禁止付费售卖。
