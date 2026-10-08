# Config — OptiScaler.ini 配置说明

> 仓库内 OptiScaler.ini 为 v1.4.40 关键键示例（节选）；完整版见成品包内 OptiScaler.ini（390 键，中文注释全量，含 XeFG 19 键性能预设 + 画质保护基线注释块）。
> 完整键表以 ini 内注释为准；本页说明常用键与性能预设。

## 一、XeFG 性能预设（v1.3.1 起）

### 均衡档（默认应用，低风险）

| 键 | 值 | 说明 |
| --- | --- | --- |
| LogToFile | false | 日志不写盘（减少磁盘 I/O 开销） |
| LogLevel | 4 | 仅记录错误 |
| LogAsync | true | 异步日志 |
| LogToConsole / LogToNGX / LogToDebug | false | 关闭控制台/NGX/调试日志 |
| EnableXeSSInputs | true | 使用 XeSS 运动矢量输入 |
| FPTSafetyMarginInMs | 0.75 | 帧节奏安全余量（Tuning A） |
| FPTVarianceFactor | 0.1 | 帧时间波动容忍（平滑优先，改善 1% Low） |
| AllowedFrameAhead | 1 | 最小生成帧队列（避免帧堆积延迟） |
| BuildPipelines / CreateHeaps / UsePrecompiledShaders | true | XeSS 管线/堆预构建 + 预编译着色器 |
| DepthValidNow / VelocityValidNow / HudlessValidNow | false | 关闭 ValidNow 系列（省显存） |

### 激进档（可选，风险自担）

| 键 | 值 | 说明 |
| --- | --- | --- |
| UseMutexForSwapchain | false | 减少锁竞争（代价：稳定性下降） |
| ForceReflex | 2 | 强制 Reflex 低延迟 |
| FramerateLimit | 0 | 不限帧率（由 Reflex/XeLL 控制） |

## 二、帧生成专项键（v1.4.2/1.4.4 起）

| 键 | 段 | 值 | 说明 |
| --- | --- | --- | --- |
| AmpereMfgUnlock | [DLSSG] | true | 内置 MFG 解锁（RTX 20/30 系 4X，与外部解锁件二选一） |
| AdaMfgUnlock | [DLSSG] | false | 保持关闭（实验性，RTX 40 未验证） |
| StreamlineIgnoreOTA | [FrameGen] | true | 只用包内 streamline 全家桶，忽略驱动 OTA 缓存 |
| ForceReflex | [fakenvapi] | 2 | DLSSG 所需 Reflex 状态自动补全 |
| PreserveSwapChain / SkipResizeBuffers | — | true | BackBuffer 同步防 FG 自动失效 |
| ModifyBufferState / ModifySCIndex | — | auto | 仍失效时按需开启（问题游戏） |
| Precision | [DlssNr] | 0 | 神经渲染计算精度（0=自动 / 1=标准 / 4=FP8；用 switch_nr_precision.bat 切换） |
| D3D11FeatureLevelElevation | [Hooks] | auto | DX11 设备错误修复（启动失败的 DX11 游戏设 false） |

> v1.4.40 起：`switch_nr_precision.bat` 数字键切换 NR 计算精度（1=恢复自动 Precision=0 / 2=FP8 Precision=4），只改 [DlssNr] 区，其他区零误改。

## 三、可选增强组件（v1.4.6）

| 键 | 段 | 默认 | 说明 |
| --- | --- | --- | --- |
| FsrAgilitySDKUpgrade | [D3D12] | auto | true 启用 D3D12Core.dll（Agility SDK 升级，Win10 老游戏开 FSR4）；回退 auto |
| LoadAsiPlugins | [Plugins] | auto | true 启用 OptiPatcher.asi（ASI 插件）；回退 auto |

- 组件文件已在包内（D3D12_OptiScaler\D3D12Core.dll / plugins\OptiPatcher.asi），默认不启用；
- 两键启用方式与回退路径完整写在 OptiScaler.ini 尾部 v1.4.6 注释块。

## 四、常用键速查

| 键 | 默认 | 说明 |
| --- | --- | --- |
| ShortcutKey | auto | 菜单快捷键（默认 Insert） |
| Enabled | auto | 主开关 |
| UpscalerIndex / FGIndex / NetworkModel | auto | 超分/帧生成后端选择（菜单操作） |
| InterpolationCount | auto | 帧生成倍率（1=2X / 2=3X / 3=4X / 5=6X） |
| UnlockMFG | auto | MFG 解锁 |
| Dxgi | auto | 显卡伪装（AMD/Intel 默认启用；异常设 false） |
| XeSSPath / XeFGPath | auto | XeSS 超分 / XeSS 帧生成 DLL 路径 |
| FGInput / FGOutput | auto | 帧生成输入/输出后端 |
| DisableOTA | auto | 禁用 OTA 检查 |

## 五、倍率与显存建议

- InterpolationCount 1=2X / 2=3X / 3=4X；4X 需显存 ≥12GB 且原生帧率 ≥60；
- 6X 需配合 dlssg_sm86（MaxGeneratedFrames=5）或 MFG 解锁组件；
- 显存压力高时：保持 ValidNow 系列 false + 关闭 HUD 叠加层（Page Up 快捷键）。

## 六、日志诊断回退

- 出问题先看日志：将 LogToFile 改回 true、LogLevel 改回 2，复现后查看 logs/；
- 一键回退：删除 OptiScaler.ini 让程序重建默认配置（或使用备份）。
