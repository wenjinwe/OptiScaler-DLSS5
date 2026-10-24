<div align="center">

# OptiScaler-DLSS5

**OptiScaler 集成重构版 —— 跨 GPU 游戏画质增强工具整合包**

**简体中文**

[![集成重构版 v1.4.58](https://img.shields.io/badge/集成重构版-v1.4.58-76b900?style=flat-square)](https://github.com/wenjinwe/OptiScaler-DLSS5/releases)
![基座 0.1.33](https://img.shields.io/badge/基座-0.1.33-7c3aed?style=flat-square)
![汉化 2000+](https://img.shields.io/badge/汉化-2000%2B处-2563eb?style=flat-square)

**[下载 v1.4.58](https://github.com/wenjinwe/OptiScaler-DLSS5/releases) · [更新记录](Changelog.md) · [已知问题](Issues.md)**

</div>

集成重构版是基于 [OptiScaler](https://github.com/optiscaler/OptiScaler) 及社区分支开发的免费整合包，提供超分辨率替换、帧生成、多帧生成、神经渲染与平滑运动等跨 GPU 画质增强能力，并全面汉化 UI、自带安装卸载器与运行库同步。它是社区版本，不是 OptiScaler、NVIDIA、AMD 或 Intel 的官方发行版。

## 主要功能

| 功能 | 说明 |
| --- | --- |
| 超分辨率 | DLSS / FSR 3.1 / FSR4 / XeSS / 原生直通，跨 NVIDIA / AMD / Intel GPU |
| 帧生成 | DLSSG / XeFG（XeSS FG）/ FSR3-FG / DLSS Enabler / OptiFG |
| 多帧生成（MFG） | 2X~6X 倍率链；RTX 20/30 系内置解锁（4X，纯配置）+ MFGUnlocker 插件位 + DLSSG 独立组件（含 6X）；高倍率失败自动回退 |
| 神经渲染（NR） | 光学 F5Low 独立页 + Look Presets 外观预设 + 曝光/白点校准 + 模型精度/多遍数（RTX 20+）；超分前运行修复（RunBeforeSR=true） |
| 平滑运动（SM） | NVIDIA Smooth Motion 解锁（sm_unlock 家族） |
| 显卡伪装 | fakenvapi（AMD/Intel 伪装 NVIDIA 运行 DLSS） |
| 汉化与 UI | 约 2000+ 处 UI 串中文化（UTF-8 等长替换，严格字节长度控制）；基准蓝主题、窗口可缩放、主题自动保存、FPS 悬浮窗七模式 |

## 快速开始

1. 从上方发行页下载最新整合包并解压；
2. 将解压目录**全部文件**复制到游戏运行程序（.exe）所在目录；
3. 运行 `setup_windows.bat`，按数字键选择加载入口（一般 `dxgi.dll` 即可）；
4. 启动游戏，按 `Insert` 打开面板，先确认基础功能正常，再逐项调整帧生成与神经渲染。

安装完成后建议先运行 `Check_DLSS_Runtime.bat` 检查运行库状态；详细步骤、更新与卸载见成品包内 `INSTALL-DLSSNR.md` 与 `使用说明.txt`。

## v1.4.58 要点

- **基座升级 0.1.27 → 0.1.33（DLSSNR Multipass feat plugins page）**：Multipass 架构 + Plugins 页面 + DLSSNR 深度优化；
- **左侧导航 tab 全量汉化**：严格字节长度控制（中文 UTF-8 每字 3 bytes），利用 null 填充空间扩展短字符串，解决单字按钮问题；ID 保护铁律：严格区分 ImGui ID 与显示文字，ID 绝对不改；
- **功能修复 ×3**：
  ① 神经渲染未正常启用 → `[DlssNr] RunBeforeSR=true`（超分前运行 NR，新基座超分后路径有 bug）；
  ② 帧生成只有 2X 没有 6X → `[Plugins] LoadAsiPlugins=true` + `[DLSSG] InterpolationCount=5`（5 次插值 = 6X）；
  ③ 卸载不干净 → 卸载脚本添加删除 `OptiScaler\nvngx_dlssnr.dll`；
- **包体积优化**：包内只存一份 `streamline\nvngx_dlssnr.dll`（263.4 MB），安装脚本自动复制到 `OptiScaler\` 根目录；
- **bat 文件编码修复**：全程 GBK (CP936) 编码读写，解决中文乱码问题；
- **规范沉淀**：§16.181（T95 三步验证法）+ §16.182（v0.1.27→v0.1.33 升级全量问题复盘，27 类问题 + 12 步检查清单 + T96-T99 四条新铁律）；
- **五轮全面审查**：R1 全面解析与审查 → R2 修复安装/卸载脚本 → R3 ini 键值深度审查 → R4 重复文件检查 → R5 最终检查，全部通过；
- 200+ 文件 / 596.6 MB（zip）；SHA256 `1266539B61E1BAB91BB22F1DC68A9EAB206F2275D7A8DCA1EF5CDC001A2B5207`。

## 文档与反馈

- [更新记录](Changelog.md) · [功能总览](Features.md) · [配置说明](Config.md) · [已知问题](Issues.md) · [显卡伪装](Spoofing.md)。
- [提交问题](https://github.com/wenjinwe/OptiScaler-DLSS5/issues)：请附版本、游戏、显卡/驱动、加载入口、FG 输入/输出、复现步骤与日志。

## 开源与致谢

感谢 [OptiScaler](https://github.com/optiscaler/OptiScaler)、神经渲染社区分支（Dagherbou / janblade / wilsjo2）及相关组件贡献者；构建参考 [OptiScalerBuilder](https://github.com/bygalacos/OptiScalerBuilder)、[OptiScaler-Aurora](https://github.com/abc354402600/OptiScaler-Aurora)。

项目使用 [GPL-3.0](LICENSE)；各随附组件依照各自许可证。整合包为社区学习交流用途，禁止付费售卖。