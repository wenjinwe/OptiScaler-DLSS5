# Spoofing — 显卡伪装说明

> 除第一代 DLSS2 游戏外，多数游戏有 NVIDIA 验证才启用 DLSS 选项；伪装工具用于绕过检查。
> ⚠️ 仅在单机 / 非反作弊环境使用；不要用于联机游戏（可能导致封号）。

## Windows

### Nvapi（fakenvapi）
- 用途：伪装 Nvapi 调用（《古墓丽影：暗影》等需要）；最新版还支持 AMD AntiLag 2 / LatencyFlex（在支持 Reflex 的游戏中降低输入延迟）；
- 配合 OptiScaler：`nvapi64.dll` 放 OptiScaler 旁，ini 设 `OverrideNvapiDll=true`（仅非 nvngx 方式生效）；
- 单独使用：放入 `%WINDIR%\System32`，**先备份原文件**，用完恢复；
- 链接：[fakenvapi releases](https://github.com/FakeMichau/fakenvapi/releases)

### DXGI（内置）
- OptiScaler 非 nvngx 方式工作时默认启用 DXGI 伪装；
- d3d12-proxy（可选）：把 dxgi.dll 放游戏 exe 旁，报告为 RTX 4090；[链接](https://github.com/cdozdil/d3d12-proxy/releases)

### Vulkan（内置，默认关闭）
```ini
; 为 Vulkan 启用 Nvidia GPU 伪装（auto=false）
Vulkan=auto
; 为 Vulkan 启用 Nvidia 扩展伪装（auto=false）
VulkanExtensionSpoofing=auto
```
- vulkan-spoofer（可选）：version.dll 放游戏 exe 旁，报告为 RTX 4090；兼容性碰运气（《无人深空》可，《毁灭战士：永恒》不可）；[链接](https://github.com/cdozdil/vulkan-spoofer/releases)

## Linux（Wine / Proton）

### DirectX 与 Vulkan（dxvk.conf）
在游戏 exe 旁创建 dxvk.conf：
```ini
dxgi.customVendorId = 10de
dxgi.hideAmdGpu = True
dxgi.hideNvidiaGpu = False
dxgi.customDeviceId = 2684
dxgi.customDeviceDesc = "NVIDIA GeForce RTX 4090"
```

### NVAPI
Proton 下设置环境变量 `PROTON_FORCE_NVAPI=1`。

## Goghor 的 DLSS 解锁器
为许多游戏制作了 DLSS 解锁器模组：[Nexus 主页](https://www.nexusmods.com/spidermanmilesmorales/users/12564231)
（《毁灭战士：永恒》目前唯一启用 DLSS 的方法是其模组）。
