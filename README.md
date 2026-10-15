<div align="center">
# OptiScaler-DLSS5
**OptiScaler 集成重构版 —— 跨 GPU 游戏画质增强工具整合包**
**简体中文**
[![集成重构版 v1.4.53](https://img.shields.io/badge/集成重构版-v1.4.53-76b900?style=flat-square)](https://github.com/wenjinwe/OptiScaler-DLSS5/releases)
![基座 0.1.31](https://img.shields.io/badge/基座-0.1.31-7c3aed?style=flat-square)
![汉化](https://img.shields.io/badge/汉化-约1900+处UI-2563eb?style=flat-square)
![组件](https://img.shields.io/badge/组件-232项-16a34a?style=flat-square)
**[下载 v1.4.53](https://github.com/wenjinwe/OptiScaler-DLSS5/releases)** · [安装](INSTALL.md) · [更新记录](Changelog.md) · [已知问题](Issues.md) · [汉化基准规范](汉化基准规范.md)
</div>
集成重构版是**基于 OptiScaler 社区分支的免费整合包**：整合超分 / 帧生成 / 多帧生成 / 神经渲染 / 平滑运动等跨 GPU 画质增强能力，全面汉化 UI，自带安装卸载器与运行库同步。它不是 OptiScaler、NVIDIA、AMD 或 Intel 的官方发行版。
## 主要功能
| 功能 | 说明 |
| --- | --- |
| 超分辨率 | DLSS / FSR 3.1 / FSR4 / XeSS / 原生直通，跨 NVIDIA / AMD / Intel GPU |
| 帧生成 | DLSSG / XeFG（XeSS FG）/ FSR3-FG / DLSS Enabler / OptiFG |
| 多帧生成（MFG） | 2X~6X 倍率链；RTX 20/30 系内置解锁（4X，纯配置）+ MFGUnlocker 插件位 + DLSSG6X 独立组件；高倍率失败自动回退 |
| 神经渲染（NR） | 光学 F5Low 独立页 + Look Presets 外观预设 + 曝光/白点校准 + 模型精度/多遍数（RTX 20+） |
| 平滑运动（SM） | NVIDIA Smooth Motion 解锁（sm_unlock 家族） |
| 显卡伪装 | fakenvapi（AMD/Intel 伪装 NVIDIA 运行 DLSS） |
| 汉化 | 约 1900+ 处 UI 串中文汉化（UTF-8 等长替换，基准规范术语表 + 映射表持续更新） |
| UI | 基准蓝主题、窗口可缩放、主题自动保存、FPS 悬浮窗七模式、UI 大小默认自动 |
| 安装卸载 | setup_windows.bat 数字键选择；卸载前校验 OriginalFilename 防误删游戏原文件 |
## v1.4.53 要点（基座升级 0.1.30 → 0.1.31 + DLSSG6X 吸收）
- **0.1.31 光学 F5Low 基座**：Look Presets 外观预设 8 种（原生/自然/电影感/仅细节/人物/绘画感/柔画布/结构感 + 基底）；曝光默认随游戏（NR 输入页五档来源）；Optical F5Low 帧生成提速（NativeUpscaler 开启时后端不再跑超分遍）；低延迟统一层（FrameCapOnly）；Load ASI plugins 复选框（与内置 MFGUnlocker.asi 机制位配套）；ReShade 可作 d3d12-ReShade64.dll
- **DLL 汉化收口**：以 0.1.30 官方原版↔主线汉化字节级 diff 作桥梁迁移 1013 串；新串补译 23 条；夹生串 169 块整串恢复（0.1.31 改写串无边界匹配污染修复）；B 类 UI 说明串整串重译 67 条；最终差异块全在 .rdata、等长无越界
- **DLSSG6X 独立组件吸收**：winmm.dll + dlssg_sm86 + ini（20/30 系 6X 解锁独立部署，与内置 dlssg_unlock 二选一）
- **ini 键表同步**：新增 `FrameCapOnly=auto`、`NativeUpscalerPass=auto`（中文注释），主线定制值保留
- **根转发器**：换 0.1.31 新构建（152,064B）；`nvngx_dlssnr.dll` 按用户约定不替换（需要时自行手动替换）
- **DLL 基座**：OptiScaler.dll 28,445,696B / SHA `ecafed90…`（0.1.31 汉化，等长替换文件大小不变）
- 232 文件 / 539.6MB（zip l9），SHA256SUMS 全量核验，verifier zip-check-entries 10/10
## 版本线（Releases）
| 版本 | 内容 |
| --- | --- |
| **v1.4.53（最新）** | 基座升级 0.1.30→0.1.31（Look Presets / 曝光随游戏 / F5Low 提速 / 低延迟统一层）；DLL 汉化收口（迁移 1013 + 新串 23 + 夹生 169 恢复 + B 类 67 重译）；DLSSG6X 独立组件；ini 2 新键；转发器换 0.1.31；映射表 v131 |
| v1.4.52 | MFGUnlocker 替换 RTXMFG（内置 MFG 方案）：plugins/MFGUnlocker.asi 机制位开箱即用，移除 RTXMFG/ 组件 + 专用文档 + 许可 |
| v1.4.51 | 吸收 dlssg-0.4.0 + MFGUnlocker v1.5.0（DLSSG 独立组件 + MFG 解锁） |
| v1.4.50 | 三轮审查收敛后升级（吸收 REPatch 组件） |
| v1.4.49 | 基座升级 0.1.27.2→0.1.30（光学 F5Low 帧生成 / 细节复用每三帧 / 压缩屏幕边缘 / DXVK 低延迟）；升级问题全录沉淀规范；同号重打包 |
| v1.4.48 | RTXMFG 集成 + 汉化；厂商中立 NR 替换件 + v0.9.51 可吸收点（不替换 nvngx_dlssnr.dll）；NeuRotic 4 许可吸收 |
| v1.4.47 | 十项串行复审：6 条半译残尾修复 + 导航单字槽双字化（图像/输入/杂项）；0.1.27.2 光学 F5Low 基座 |
| v1.4.46 | DLL 长文整串补译 8 条 + 半译尾巴 4 条 + CRCRLF 行尾闪退修复 + PS 英文残留汉化 |
| v1.4.45 | 安装/卸载异常还原保留备份；运行库还原 exit 1-4 不再误清理备份 |
| v1.4.44 | SHA 校验失败自动还原游戏原文件，杜绝半装状态残留 |
| v1.4.43 | 0.1.27.2 基座升级收口：光学 F5Low 独立页 + 约 190 条新增汉化 |
| v1.4.42 | 单字母尾残 71 处 + 多余 %s 格式串 + 串中残渣 15 处全量清零；导航补译 |
| v1.4.41 | 0.1.27.2 基座升级（光学 F5Low）；Insert 闪退修复（19 处格式符污染）；残渣串三批 400+ 处 |
| v1.4.40 | 三轮解析-修复循环：脚本 4 处修复 + 运行冒烟 + 键表交叉 + 禁止字样清理 |
| v1.4.38 | 8 脚本全量审查零 bug；UI 大小默认自动；158 文件 / 417.83MB |
| v1.4.36 | 深度精简定稿：合并重复、FSR4 替换件 2 版、去除冗余组件 |
| v1.4.33 | 安装器块内 goto 闪退修复；子串冲突修复；补译收尾 |
| v1.4.27 | 神经渲染菜单补译；人物脸部渲染调节修复 |
| v1.4.19 | 卸载防误删（OriginalFilename 校验）；数字键选择 |
| v1.4.12 | 40serial-MFG 基座切换 |
| v1.4.6 | 可选增强组件解析与文档化 |
| v1.4.0 | XeFG + SM 集成（dlssg_unlock_3109 + sm_unlock） |
| v1.2.0 | 神经渲染基座 + 995 处汉化 |
完整版本记录见 [Changelog.md](Changelog.md)。
## 快速开始
1. 从 [Releases](https://github.com/wenjinwe/OptiScaler-DLSS5/releases) 下载最新整合包并解压；
2. 将 `OptiScaler` 文件夹整体复制到游戏运行程序所在目录；
3. 运行 `setup_windows.bat`，按数字键选择加载入口（一般 `dxgi.dll` 即可）；
4. 启动游戏，按 `Insert` 打开菜单面板，按需配置超分 / 帧生成 / 神经渲染。
> 安装完成后运行 `Check_DLSS_Runtime.bat` 可检查 DLSS / Streamline 运行库状态；卸载运行 `uninstall_optiscaler.bat`（不会误删游戏原文件）。
## 组件清单
| 组件 | 说明 |
| --- | --- |
| OptiScaler.dll | 主程序（0.1.31 汉化版，UTF-8 等长替换，28,445,696B） |
| streamline/ | NVIDIA Streamline 全家桶（sl.* + nvngx_dlssg / dlssd / dlssnr） |
| nvngx_dlssnr.dll | DLSS 神经渲染模型（官方，**不替换**，需要时自行手动替换） |
| libxess.dll / libxess_fg.dll | XeSS 超分 / 帧生成后端 |
| amd_fidelityfx_* | FSR 超分 / 帧生成后端 |
| dlssg_sm86/ | RTX 20/30 系内置 MFG 解锁组件（sideload，4X 上限） |
| dlssg_unlock_3109/ | 外部 MFG 解锁替换件（与内置解锁二选一） |
| plugins/MFGUnlocker.asi | MFGUnlocker 插件位（开箱即用，LoadAsiPlugins=true；与代理部署/内置解锁互斥） |
| DLSSG6X独立组件/ | DLSSG 6X 独立部署（winmm.dll + dlssg_sm86 + ini；20/30 系 6X 解锁，与内置二选一） |
| MFGUnlocker/ | MFGUnlocker 官方组件（DLL + README，插件位副本与 DLL 逐字节相同） |
| FSR4自定义替换件/ | FSR4 0.2d / 1.1b 两版替换件（按需手动替换） |
| fakenvapi.dll | 显卡伪装（AMD/Intel 运行 DLSS） |
| D3D12_OptiScaler/ | DX12 Agility SDK 升级组件（可选） |
| plugins/OptiPatcher.asi | ASI 插件（可选，仅名单内游戏生效） |
| dxgi.dll / winmm.dll / version.dll / dinput8.dll | 注入入口（按游戏 API 选择） |
| Check_DLSS_Runtime.bat | 运行库检查：DLSS / Streamline / NR 组件版本速查 |
| switch_nr_precision.bat | NR 计算精度三模式切换（自动 / 标准 / FP8） |
| get_streamline.ps1 / runtime_sync.ps1 | Streamline 获取 / 运行库同步（四重防护） |
## 注意事项
- **防反作弊**：避免在启用反作弊的多人在线游戏中使用（可能导致封号）；
- **备份**：安装前备份游戏目录原有 mod 文件；卸载器仅删除注入件，不会误删游戏原文件；
- **MFG 解锁互斥**：内置解锁 / dlssg_unlock 替换件 / MFGUnlocker 插件位 / DLSSG6X 独立组件【多方案二选一】，不可同时使用；
- **nvngx_dlssnr.dll**：包内为官方原版，不随升级替换（需要时用户自行手动替换）；
- **神经渲染**：实验性功能，成本较高且可能闪烁，建议先开 1 个 Pass 测试；
- **注入链版本一致**：升级后核验 dxgi.dll 与 OptiScaler.dll 尺寸/SHA 一致（版本错配会启动闪退）；
- **UI 大小**：默认自动（Scale=auto，<900p 自动缩小）；可手动改 `MenuWidth` / `MenuHeight` / `Scale` 固定值；
- **画质保护基线**：禁止为性能改动画质键（Precision / 细节强度 / 倍率 auto 保持官方默认）。
## 文档导航
- [INSTALL.md](INSTALL.md)：安装 / 卸载 / 运行库检查 / 常见问题
- [使用说明.md](使用说明.md)：包内安装与按键说明
- [Config.md](Config.md)：配置键说明
- [Features.md](Features.md)：功能总览
- [Changelog.md](Changelog.md)：完整版本记录
- [Issues.md](Issues.md)：已知问题与限制
- [Spoofing.md](Spoofing.md)：显卡伪装说明
- [汉化基准规范.md](汉化基准规范.md)：汉化术语表 / 铁律 / 版本线（索引版）
## 许可与免责声明
- 本仓库文档 / 配置随上游采用 GPL-3.0（见 [LICENSE](LICENSE)）；
- 组件版权归原作者：OptiScaler（GPL-3.0）、NVIDIA Streamline / DLSS（专有）、Intel XeSS（专有）、AMD FidelityFX（MIT）等，见各组件许可证；
- 本整合包为社区学习交流用途，未获上游任何项目认可，不承担使用风险；禁止付费售卖。
## 致谢
- 上游：[OptiScaler](https://github.com/optiscaler/OptiScaler) 及神经渲染社区分支（Dagherbou / janblade / wilsjo2 线）
- 构建参考：[OptiScalerBuilder](https://github.com/bygalacos/OptiScalerBuilder)、[OptiScaler-Aurora](https://github.com/abc354402600/OptiScaler-Aurora)、[F5-DLSSNR-Multipass](https://github.com/janblade/OptiScaler-F5-DLSSNR-Multipass)、[DLSSNR-PreSR-Multipass](https://github.com/wilsjo2/OptiScaler-DLSSNR-PreSR-Multipass)
- 汉化基准：[汉化基准规范.md](汉化基准规范.md)（术语表 + 等长替换 + 安全验证流程）
