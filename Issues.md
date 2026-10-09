# Issues — 已知问题与限制

> 以下为集成重构版当前已知问题与上游基座限制（实查确认，非猜测）。
> 全局铁律：不损画质、保兼容 / 稳定 / 准确 / 实用 / 可靠 / 安全、留回退路径、保护个人隐私。

## 一、基座限制（DLL 层，整合包内无法修复）

### 1. NR 计算精度三模式 UI 未实现
- 上游基座（0.1.27.2）菜单只有 `Precision` 数值键，无"自动 / 标准 / FP8 三模式"UI；
- 整合包已用 `switch_nr_precision.bat` 在配置层实现三模式切换（`[DlssNr] Precision=0/1/4`）；
- 切换精度不会自动重建神经渲染（需重启游戏或按上游行为生效）。

### 2. 设置页组件版本列表空白
- 数据在内存中，但基座 UI 无此列表项；用根目录 `Check_DLSS_Runtime.bat` 速查包内组件版本。

### 3. RTX 40 系 5X / 6X 无原生支持
- 基座对 RTX 40 系仅游戏原生 DLSSG（4X）；5X/6X 需外部 dlssg_unlock 替换件；
- 内置解锁（`AmpereMfgUnlock`）只覆盖 RTX 20/30 系 4X，与外部解锁件【二选一】，不可同时使用。

### 4. 光学 F5Low 依赖上游实现
- F5Low（无升频器游戏的 DLSS-NR）在 UE DX11 等部分游戏仍可能有边界情况（上游 0.1.27.2 已大幅改善：运动感/低延迟/曝光原生，但非全场景验证）；
- 反作弊保护的游戏可能拒绝加载（非整合包可解决）。

## 二、使用注意事项

- 神经渲染为实验性功能，成本较高且可能闪烁，建议先开 1 个 Pass 测试；
- 人脸渲染调节在部分光照 / 画风下效果不明显（上游限制，v1.4.27 已尽力优化）；
- 内置 MFG 解锁与外部 dlssg_unlock 替换件不可同时使用；
- 防反作弊：避免在启用反作弊的多人在线游戏中使用（可能导致封号）；
- Vulkan 伪装部分游戏不适用（如《毁灭战士：永恒》）。

## 三、排查路径

- 安装后先跑 `Check_DLSS_Runtime.bat` 检查运行库状态；
- **启动即闪退（游戏）**：核验注入链版本一致（dxgi.dll 与 OptiScaler.dll 尺寸/SHA 必须一致）→ 查 `[Hooks] D3D11FeatureLevelElevation`（DX11 设备错误设 false）→ 检查第三方注入件冲突（REFramework dinput8 / Fakenvapi version.dll）；
- 日志诊断：`OptiScaler.ini` 中 `LogToFile=true`、`LogLevel=2`，复现后查 logs/；
- 一键还原：删除 OptiScaler.ini 让程序重建默认配置；卸载用 `uninstall_optiscaler.bat`（不会误删游戏原文件）；
- 如遇上游 bug，可尝试原版构建：[wilsjo2/OptiScaler-DLSSNR-PreSR-Multipass](https://github.com/wilsjo2/OptiScaler-DLSSNR-PreSR-Multipass)、[janblade/OptiScaler-F5-DLSSNR-Multipass](https://github.com/janblade/OptiScaler-F5-DLSSNR-Multipass)。
