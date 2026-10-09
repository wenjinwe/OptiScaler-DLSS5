# INSTALL — 安装与卸载

> 适用：OptiScaler-集成重构版 v1.4.47（Windows）
> 全局铁律：不损画质、保兼容 / 稳定 / 准确 / 实用 / 可靠 / 安全、留回退路径。

## 一、安装

1. 从 [Releases](https://github.com/wenjinwe/OptiScaler-DLSS5/releases) 下载最新整合包并解压；
2. 将解压目录整体复制到游戏运行程序（exe）所在目录；
3. 运行 `setup_windows.bat`，按数字键选择加载入口：
   - `dxgi.dll`（DX11 / DX12 通用，默认推荐）
   - `winmm.dll` / `version.dll` / `dinput8.dll`（按游戏 API / 注入习惯选择）
4. 启动游戏，按 `Insert` 打开菜单，配置超分 / 帧生成 / 神经渲染。

> NR 提示：神经渲染运行库（`nvngx_dlssnr.dll`）已包含在包内 `OptiScaler/streamline/`，无需自备。
> 安装完成后建议先运行 `Check_DLSS_Runtime.bat` 检查运行库状态。

## 二、升级与版本一致

- 从旧版升级时，用新包**全部文件**覆盖游戏目录（不要只替换 dxgi.dll）；
- 升级后核验注入链版本一致：`dxgi.dll`（注入器）与 `OptiScaler.dll`（核心）的**字节尺寸与 SHA 必须一致**（官方注入器=核心 DLL 同一文件改名）——版本错配会启动即闪退；
- 旧版备份可改名保留（如 `OptiScaler.dll.bak_v0.1.27`）以便回退。

## 三、卸载

- 运行游戏目录中的 `uninstall_optiscaler.bat`，按提示选择即可；
- 卸载器只删除注入件，删除前校验 `OriginalFilename='OptiScaler.dll'`，拒绝路径穿越（`..` / 盘符冒号），**不会误删游戏原文件**；
- 若安装了外部替换件（dlssg_unlock / sm_unlock / FSR4 替换件），手动删除对应文件即恢复原版。

## 四、运行库检查与工具

| 工具 | 说明 |
| --- | --- |
| `Check_DLSS_Runtime.bat` | 检查 DLSS / Streamline / NR 运行库状态，输出包内组件版本速查 |
| `get_streamline.ps1` | 获取 Streamline 全家桶（SHA256 + Authenticode + 白名单 + 目录限制四重防护） |
| `runtime_sync.ps1` | 运行库同步（仅清临时文件，保护 Legacy / Unknown SL） |
| `switch_nr_precision.bat` | NR 计算精度三模式切换（自动 / 标准精度 / FP8） |

## 五、环境要求

- Windows 10 1809+（推荐 Win10 22H2 / Win11）；
- NVIDIA 驱动 546+（RTX 20/30/40/50 系；神经渲染需 RTX 20+）；
- AMD / Intel 卡可用 FSR / XeSS 路径（部分功能受基座限制）；
- 首次安装如遇 Windows App Runtime 缺失：运行包内对应运行库安装程序（PRI / Windows App Runtime）。

## 六、常见问题

- **菜单没出现**：确认注入文件在 exe 目录、游戏为 DX11 / DX12 / Vulkan、按 `Insert`；
- **启动即闪退（游戏）**：先核验注入链版本一致（dxgi.dll 与 OptiScaler.dll 尺寸/SHA）；再查 `[Hooks] D3D11FeatureLevelElevation`（DX11 设备错误时设 false）；第三方注入件（REFramework dinput8 / Fakenvapi version.dll）确认与 OptiScaler 入口不冲突；
- **启动即闪退（bat）**：`setup_windows.bat` 请勿双击直接运行——在游戏目录打开命令行 / 右键"以管理员身份运行"，按数字键操作；若仍闪退，检查文件行尾是否为 CRLF（包内文件已规范，重解压即可）；
- **帧生成开了自动失效**：BackBuffer 同步（`PreserveSwapChain` / `SkipResizeBuffers`）已默认开启；仍失效再开 `ModifyBufferState` / `ModifySCIndex`；
- **想还原默认**：删除 OptiScaler.ini（程序重建默认配置）。
