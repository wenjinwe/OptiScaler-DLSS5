# INSTALL — 安装、卸载与使用
> 适用：OptiScaler-集成重构版 v1.4.55（Windows）
> 全局铁律：不损画质、保兼容 / 稳定 / 准确 / 实用 / 可靠 / 安全、留回退路径。
## 一、安装
1. 从 [Releases](https://github.com/wenjinwe/OptiScaler-DLSS5/releases) 下载最新整合包并解压；
2. 将解压目录**全部文件**复制到游戏运行程序（exe）所在目录（与游戏 exe 同目录）；
3. 运行 `setup_windows.bat`，按数字键选择加载入口：
   - `dxgi.dll`（DX11 / DX12 通用，默认推荐）
   - `winmm.dll` / `version.dll` / `dinput8.dll`（按游戏 API / 注入习惯选择）
4. 启动游戏，按 `Insert` 打开菜单，配置超分 / 帧生成 / 神经渲染。
> 若游戏中无中文（显示方块）：确认 Windows 装有微软雅黑字体（Win10/11 自带，一般无需处理）。
> NR 提示：神经渲染运行库（`nvngx_dlssnr.dll`）已包含在包内 `OptiScaler/streamline/`（ShortFuse 310.8 兼容版，全系通用），**不随升级替换**（需要更新时自行手动替换）。
## 二、常用按键
| 按键 | 功能 |
| --- | --- |
| Insert | 打开/关闭设置菜单 |
| Page Up | 显示/隐藏 FPS 悬浮窗 |
| Page Down | 切换 FPS 显示模式 |
| End | 开关帧生成 (FG) |
## 三、升级与版本一致
- 从旧版升级时，用新包**全部文件**覆盖游戏目录（不要只替换 dxgi.dll）；
- 升级后核验注入链版本一致：`dxgi.dll`（注入器）与 `OptiScaler.dll`（核心）的**字节尺寸与 SHA 必须一致**（官方注入器=核心 DLL 同一文件改名）——版本错配会启动即闪退；
- **nvngx_dlssnr.dll**（神经渲染模型）按约定不随升级替换：需要更新时自行手动替换（旧版工作不受影响）；
- 旧版备份可改名保留（如 `OptiScaler.dll.bak_v0.1.31`）以便回退。
## 四、卸载
- 运行游戏目录中的 `uninstall_optiscaler.bat`，按提示选择即可；
- 卸载器只删除注入件，删除前校验 `OriginalFilename='OptiScaler.dll'`，拒绝路径穿越（`..` / 盘符冒号），**不会误删游戏原文件**；
- 若安装了外部替换件（dlssg_unlock / sm_unlock / FSR4 替换件 / DLSSG 独立组件 / MFGUnlocker 代理部署），手动删除对应文件即恢复原版。
## 五、运行库检查与工具
| 工具 | 说明 |
| --- | --- |
| `Check_DLSS_Runtime.bat` | 检查 DLSS / Streamline / NR 运行库状态：Check（速查）/ Install（自动替换需更新运行库）/ Restore（还原备份） |
| `get_streamline.ps1` | 获取 Streamline 全家桶（SHA256 + Authenticode + 白名单 + 目录限制四重防护） |
| `runtime_sync.ps1` | 运行库同步（仅清临时文件，保护 Legacy / Unknown SL） |
| `switch_nr_precision.bat` | NR 计算精度三模式切换（自动 / 标准精度 / FP8） |
## 六、环境要求
- Windows 10 1809+（推荐 Win10 22H2 / Win11）；
- NVIDIA 驱动 546+（RTX 20/30/40/50 系；神经渲染需 RTX 20+）；
- AMD / Intel 卡可用 FSR / XeSS 路径（部分功能受基座限制）；
- 首次安装如遇 Windows App Runtime 缺失：运行包内对应运行库安装程序（PRI / Windows App Runtime）。
## 七、配置与常见问题
- 菜单里改完设置，选"保存设置"后重启游戏生效；`OptiScaler.ini` 键名均为英文（勿改）；
- UI 大小默认自动（MenuWidth/Height=auto + Scale=auto，<900p 自动缩小）；可手动改 `MenuWidth` / `MenuHeight` / `Scale` 固定值锁定大小；
- MFG 解锁多方案【二选一】：内置解锁 / dlssg_unlock 替换件 / MFGUnlocker 插件位 / DLSSG 独立组件，不可同时使用；
- 帧生成需要游戏本身支持或通过 mod 注入；神经渲染 (NR) 为实验性，默认部分关闭，按需开启；若 FSR-FG 提示缺少 dll，检查 amd_fidelityfx_* 系列文件；
- **菜单没出现**：确认注入文件在 exe 目录、游戏为 DX11 / DX12 / Vulkan、按 `Insert`；
- **启动即闪退（游戏）**：先核验注入链版本一致（dxgi.dll 与 OptiScaler.dll 尺寸/SHA）；再查 `[Hooks] D3D11FeatureLevelElevation`（DX11 设备错误时设 false）；第三方注入件（REFramework dinput8 / Fakenvapi version.dll）确认与 OptiScaler 入口不冲突；
- **启动即闪退（bat）**：`setup_windows.bat` 请勿双击直接运行——在游戏目录打开命令行 / 右键"以管理员身份运行"，按数字键操作；若仍闪退，检查文件行尾是否为 CRLF（包内文件已规范，重解压即可）；
- **帧生成开了自动失效**：BackBuffer 同步（`PreserveSwapChain` / `SkipResizeBuffers`）已默认开启；仍失效再开 `ModifyBufferState` / `ModifySCIndex`；
- **帧生成下拉无 DLSS 选项**：核对 dlssg 运行库版本与 MFGUnlocker 兼容性（规范 §16.145 排查路径；包内 streamline `nvngx_dlssg.dll` 维持 310.9.16 独立组件路线）；
- **想还原默认**：删除 OptiScaler.ini（程序重建默认配置）；避免在反作弊多人在线游戏中使用。
