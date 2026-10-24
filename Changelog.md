# Changelog
## v1.4.58（2026-10-24）— 基座升级 0.1.27 → 0.1.33（DLSSNR Multipass feat plugins page）+ 五轮审查修复
**基座升级 0.1.27 → 0.1.33（DLSSNR Multipass feat plugins page 分支）**
- 官方新基座全面吸收：Multipass 架构 + Plugins 页面 + DLSSNR 深度优化；
- DLL 译文迁移：桥梁法（0.1.27 官方原版 ↔ 主线汉化版 字节级 diff 提取译文库），新串补译 100+ 条；
- **左侧导航 tab 全量汉化**：严格字节长度控制（中文 UTF-8 每字 3 bytes），利用 null 填充空间扩展短字符串，解决单字按钮问题；
- **ID 保护铁律**：严格区分 ImGui ID（小写、## 后缀）与显示文字（首字母大写），ID 绝对不改，只改显示文字；
- **功能修复 ×3**：
  ① 神经渲染未正常启用 → `[DlssNr] RunBeforeSR=true`（超分前运行 NR，新基座超分后路径有 bug）；
  ② 帧生成只有 2X 没有 6X → `[Plugins] LoadAsiPlugins=true` + `[DLSSG] InterpolationCount=5`（5 次插值 = 6X）；
  ③ 卸载不干净 → 卸载脚本添加删除 `OptiScaler\nvngx_dlssnr.dll`；
- **包体积优化**：包内只存一份 `streamline\nvngx_dlssnr.dll`（263.4 MB），安装脚本自动复制到 `OptiScaler\` 根目录，卸载脚本自动删除；
- **bat 文件编码修复**：全程 GBK (CP936) 编码读写，解决 PowerShell UTF-8 读取 GBK 文件导致中文乱码问题；
- **规范沉淀 §16.181 + §16.182**：
  - §16.181（T95 三步验证法）：原始基准对比 → 严格区分显示文字与 ID → 修改后回读验证；
  - §16.182（v0.1.27→v0.1.33 升级全量问题复盘）：27 类问题（12 类 DLL 汉化技术 + 8 类功能配置 + 7 类脚本工具）+ 12 步升级检查清单 + T96-T99 四条新铁律（字节长度严格控制 / ID 保护 / bat GBK 编码 / 12 步检查清单）；
- 五轮全面审查：R1 全面解析与审查 → R2 修复安装/卸载脚本 → R3 ini 键值深度审查 → R4 重复文件检查 → R5 最终检查，全部通过；
- 200+ 文件 / 596.6 MB（zip）；SHA256 `1266539B61E1BAB91BB22F1DC68A9EAB206F2275D7A8DCA1EF5CDC001A2B5207`。

## v1.4.56（2026-10-17）— UI 汉化三轮深扫（21 处补译）+ 重打包
**UI 汉化三轮（截图驱动 + 新维度，同号重打包）**
- ① 截图驱动 7 处：导航 Image→图像、Input→输入；底部 Close→关闭、开 Wiki→开维基；垂同区 垂直同步设→垂直同步、垂同开→垂直开、垂同关→垂直关（短串等长规则：等长区=串+NUL 填充；规范 §16.151）；
- ② 枚举类 13 处：日志级 Error→错误、Info→信息；底部 自(%3.1f)→自动(%3.1f)；外观 Light/Strong/Faces→明亮/强烈/人脸；比较 Wipe/Zoom→擦除/缩放；引擎 Other→其他；曝光 High/Custom→高/自定义；背景 Full→完整（8B/12B/16B 槽位精扫定位；规范 §16.152）；
- ③ 一致性 + 新维度：Watercolour→水彩（风格化枚举，与擦除/缩放一致）；文件尾未扫区（0x01A30000-EOF，986KB）全扫 0 漏译（均为系统 API 导入名）；Zero/Set 上下文未明判保留；4 个「缺括号」疑似劣译经精确字节搜索**全为完整独立串**（混排扫描 offset 是子串起点非串起点——假阳性澄清；规范 §16.153，铁律 T70）；
- 全量回读 24/24 OK；映射表 map_en_cn 1345 条；SHA256SUMS 同步；DLL SHA12=`3af21dabc309`；
- 重打包：218 文件 / 520.3MB（zip l6），zip↔目录 218/218 匹配 0 多余。

## v1.4.55（2026-10-16）— 运行问题修复 ×2 + 全面复审（同号重打包）
**运行问题修复（实机反馈，非猜测）**
- **修复①：NR 模型 GPU 不匹配**。RTX 4070 实报「NGX 核心拒绝其能力参数」→ 三层证据闭环（现场模型 310.9 + 官方 GPU 表仅 310.8 + NVIDIA DLSS 5 首发 RTX 50）→ streamline `nvngx_dlssnr.dll` 换 **ShortFuse 310.8 兼容版（E67DEE，全系通用）** + 文档 GPU 表补行 + SHA 重算 + 同号重打包；规范 §16.144；
- **修复②：DLSS 帧生成选项消失**。MFGUnlocker 日志成功/失败对照（support query 0→32、GetState 0x0→31）+ provider 候选版本对比（310.9.1 正常 vs 310.9.16 冲突）+ 文件时间戳定案（部署 v1.4.55 换 dlssg 310.9.16）→ 定位 dlssg 运行库与 MFGUnlocker 兼容冲突；**按用户决定目录/包内维持 310.9.16（独立组件路线）**；规范 §16.145；
**全面复审（同号重打包，不升级版本号）**
- DLL：映射表 1335 键全交叉 **0 漏译**；14 条残留单字词甄别全合法（代码符号 / AMD 官方厂商名 / 错误日志）；短串放宽扫描全合法（技术缩写 / 厂商名 / 日志 token）；
- 脚本：4 bat（GBK + 全 CRLF + 无 NUL）✓；5 ps1 语法 0 错误 ✓；setup_windows.bat（865 行）与 uninstall_optiscaler.bat（524 行）全量审查零功能性 bug；runtime_sync.ps1 与「维持 310.9.16」一致（同步源取自包内实际文件）；
- 文档一致性：README 版本号 v1.4.54→v1.4.55；目录↔zip 对齐（补回 `reflex.license.txt`）；使用说明版本上下文全合理；
- 220 文件 / 552MB（zip l9）；SHA256SUMS 219 条 **0 失配**；verifier 5/5；不升级版本号。

## v1.4.54（2026-10-15）— 复审收敛 + 升级版本号
- 19 类 / 20 类问题修复对照总表逐项复审（R1 解析+查 bug+优化安装卸载+优化文件代码；R2 从头复查收敛）；
- 短串 3 项甄别合法 + 多行串修复 3 处 + ini 深度通过 + 冒烟修 2 脚本 bug + 卸载冒烟通过；死键重验 + SHA256SUMS + 官方残留英文串检查 + ps1 审查；
- 升级版本号 v1.4.54 重打包验收交付。

## v1.4.53（2026-10-15）— 基座升级 0.1.30 → 0.1.31（同号重打包）+ DLSSG6X 吸收
**基座升级 0.1.30 → 0.1.31（commit 5d5cdccd，同号 v1.4.53 重打包）**
- 官方集合级 diff 确认仅 11 个同名文件不同，其余运行时组件与 0.1.30 逐字节相同（印证官方"只需换 DLL"）；
- **DLL 汉化收口**（28,445,696B / SHA `ecafed90…`）：桥梁法（0.1.30 官方原版 f4f6e2be ↔ 主线汉化 065ade21 字节级 diff 提取 1798 个唯一 en→cn 对，对 0.1.31 内容匹配写入 1013 串 / 14437 点）；新串补译 23 条（Frame cap only / Load ASI plugins / Detail only / Painterly / Built on: / Soft canvas / Structure 等）；**夹生串修复**（v162h 无边界子串替换产生 237 条夹生：InputCommon→Input常见、vkCmdBlitImage→vkCmdBlit图像 + 4 处 .rdata 外越界污染 → 全部恢复官方，169 块整串恢复）；**B 类 UI 说明串整串重译 67 条**（低延迟说明 / NR 状态行 / Look Presets 说明 / Optical F5Low 状态行 / FG 跟随说明；9 条超长逐条修译文后重跑通过）；最终差异块 13,984 全在 .rdata、等长无越界；0.1.31 新功能 UI 英文残留 0；
- **0.1.31 新功能**：Look Presets 外观预设 8 种 + Built on 基底；曝光默认随游戏（NR 输入页五档）；Optical F5Low 帧生成提速（NativeUpscalerPass 使后端不再跑超分遍）；低延迟统一层 FrameCapOnly；**Load ASI plugins 复选框**（与内置 MFGUnlocker.asi 机制位配套）；NR only 扩展 HDR10/DX11/Vulkan；ReShade 可作 d3d12-ReShade64.dll；FG input DLSSG 跟随游戏 DLSS-FG 开关（2x/3x/4x）；
- **ini 键表**：新增 2 键（`[Framerate] FrameCapOnly=auto`、`[DlssNr] NativeUpscalerPass=auto`）带中文注释合并，0 移除，主线定制值（StreamlineIgnoreOTA / AmpereMfgUnlock / LoadAsiPlugins / Log 静默）保留；
- **根转发器**：`nvngx.dll_dlssnr.dll` 换 0.1.31 新构建（152,064B / c3d70e68）；`nvngx_dlssnr.dll` 按用户约定**不替换**；
- **文档同步**：使用说明.txt（GBK）0.1.31 补记段；必看说明.md（UTF-8）更新；INSTALL-DLSSNR.md diff 确认主线已最新（picture/depth/movement data）；
- **键表交叉 + 6 维检查**全绿：3 新键 ↔ DLL 汉化 UI 串全部对应；兼容/稳定/安全/实用/可靠通过；
- 232 文件 / 539.6MB（zip l9）；SHA256SUMS 231 条；verifier zip-check-entries 10/10；**规范 §16.128 沉淀 + 映射表 v131（1337 条）**。
**DLSSG6X 独立组件吸收（同日，v1.4.53 内）**：吸收 DLSS.Unlocked.XeFG.30X.DLSSG.6X.v0.2.0 中 DLSSG6X 独立组件（winmm.dll + dlssg_sm86 + ini）；卸载 bat 对比优化安装/卸载。

## v1.4.52（2026-10-13）— MFGUnlocker 替换 RTXMFG（内置 MFG 方案）
- 用户拍板：将 MFGUnlocker.dll 放入游戏目录，替换 RTXMFG/（OptiScaler 内置 MFG 方案）；移除 5 项（RTXMFG/ + 专用文档 ×2 + 上游许可）；保留 MFGAmpereUnlock/AdaUnlock 许可；
- **plugins/MFGUnlocker.asi 机制位开箱即用**：组件 DLL 副本改名放 `OptiScaler\plugins` + `[Plugins] LoadAsiPlugins=true`；副本与 DLL 逐字节相同（8,929,280B）；与代理部署/内置解锁互斥声明；
- 引用更新四处对齐；211 文件；verifier zip-check-entries 11/11；SHA256SUMS 210/210；三轮审查（18 类总表 §16.113 逐类对照）通过，不升级版本号。

## v1.4.51（2026-10-13）— 吸收 dlssg-0.4.0 + MFGUnlocker v1.5.0
- 吸收 dlssg-release-0.4.0（DLSSG 独立组件：version.dll + dlssg_sm86 全套 + 文档）+ MFGUnlocker-v1.5.0 构建；216 条目。

## v1.4.50（2026-10-12）— 三轮审查收敛 + 升级版本号
- R1 吸收 REPatch + 全面解析；R2 修复 + 键表交叉 + 优化安装卸载；R3 收敛后升级 v1.4.50。

## v1.4.49（2026-10-11）— 基座升级 0.1.27.2 → 0.1.30（同号重打包）
- **0.1.30 基座**：光学 F5Low 帧生成；Reuse detail 每三帧重用细节；Optical F5Low 低边缘运动；低延迟选择更多；压缩屏幕边缘（实验性）；DXVK DirectX 11 游戏支持；XeFG 与 REFramework 并列；HDR 纸白曝光；
- 0.1.27→0.1.30 升级问题全录沉淀规范（0.1.27.2 官方原版作中间桥梁建完整译文库）；映射表 v130 建立（1217 条）；
- 残余残尾串清理 + DLL 长文补译 + 脚本修复 + 冒烟 + 键表交叉 + 全量甄别收敛 + 六维检查 + 短串放宽扫描 + 文档一致性，多轮收敛后同号重打包 v1.4.49。

## v1.4.48（2026-10-10）— RTXMFG 集成 + 厂商中立 NR 替换件
- 深度解析 RTXMFG.dll（身份 + 行为 + UI 串）并汉化（等长替换），集成 dlssg_sm86.ini + version.dll + RTXMFG.dll 构建 v1.4.48；
- 吸收 Optional-Vendor-Neutral-DLSS5-Forwarder + dlss-unlocked-standalone-NR-v0.9.51 可吸收点（**不替换 nvngx_dlssnr.dll**）；吸收 NeuRotic-Alpha-0.9.8 4 个许可；不制作单文件版。

## v1.4.47（2026-10-09）— 十项串行复审 + 导航单字槽双字化（0.1.27.2 光学 F5Low 基座）
- 6 条半译残尾串等长修复；键表交叉：ini 38 节/396 键双向核对，17 条"缺失"经甄别全为 bat 局部变量误报；短串放宽扫描：1145 条候选全为 UTF-16 误读假阳性（排除规则固化）；六维全绿；
- 导航单字槽修复：左侧导航 `图/输/杂` → `图像/输入/杂项`（槽位容量 8B/12B 足以容纳双字）；状态标签 Error→错误、信→信息；
- DLL 27,751,424B / SHA256 `0d7475ba…`；159 文件 / 419.30MB；verifier zip-check-entries 12/12。

## v1.4.46（2026-10-09）— DLL 长文整串补译 + CRCRLF 闪退修复 + PS 英文残留汉化
- DLL：F5Low/NR 页面 8 条 119~615 字符长说明串整串补译；修复 4 条半译串英文尾巴；
- **CRCRLF 行尾闪退修复**：zip 内 4 个 bat 行尾损坏（0D 0D 0A）→ 双击 setup_windows.bat 闪退真根因，全量重写 CRLF + 字节级核验（此前的"块内 goto"定论经最小实验证伪，16.103→16.104 纠正）；
- runtime_sync.ps1 双语标题英文段汉化；get_streamline.ps1 12 条英文 throw/Write-Host 汉化；五轮复审零发现；
- DLL SHA `AF4E36C4…`；159 文件 / verifier 15/15。

## v1.4.45（2026-10-09）— 安装/卸载第十二轮：异常还原保留备份 + 全量补译
- 安装器：SHA 校验失败且无 .osbak 时自动清理错误注入副本，杜绝半装状态残留；
- 卸载器：运行库还原 exit 1-4（异常）时保留备份并移出，仅 exit 0 才清理同步状态；Check/runtime_sync/get_streamline 英文输出汉化（约 35 处）。

## v1.4.44（2026-10-09）— 安装/卸载：校验失败自动还原 + 组件验证
- SHA 校验失败自动还原游戏原文件；组件复制关键件验证（sl.interposer.dll）；脚本版本号同步。

## v1.4.43（2026-10-08）— 0.1.27.2 基座升级收口（光学 F5Low）
- 基座 0.1.27.1 → 0.1.27.2：DLSS-NR 更名"光学 F5Low"，神经渲染下新增独立页 + 全部设置；F5Low 低延迟（Reflex / Anti-Lag 2 / XeLL / LatencyFlex）；曝光新增"原生"起点；
- 汉化约 190 条新增串，真 UI 区零漏译；DLL 27,751,424B（0.1.27.2 汉化）。

## v1.4.42（2026-10-08）— 单字母尾残 + 多余 %s 格式串 + 串中残渣全量清零
- 单字母尾残 71 处（等长短译未清槽残留官方末位字母）；多余 %s 格式串 3 处 + 串中残渣整串重写 15 处；导航补译 5 处；
- 版本错配排查方法论入交付清单；DLL SHA `B2487512…`；159 文件 / verifier 15/15。

## v1.4.41（2026-10-08）— 0.1.27.2 基座升级 + Insert 闪退修复 + 残渣串三批
- **Insert 闪退修复（重大 bug）**：19 条 UI 状态串等长填充用可见字符而非 NUL → 译文多出 %s/%u/%llu 占位符 → ImGui 按格式串读栈 → 打开 Overlay 即崩溃；全部重写，% 集合与官方完全一致，填充物一律 NUL；
- **残渣串三批修复（400+ 处）**：短标签污染、##ID 污染、串中残渣、乱码重复、半译彩蛋 49 条恢复官方英文原文；0.1.27.2 新增约 190 条 UI 串全量汉化；
- DLL SHA `3F6247B6…` → `524BF00A…` → `9C11E8C7…`；159 文件。

## v1.4.40（2026-10-08）— 三轮解析-修复循环（同版本优化，DLL 基座零改动）
- 脚本层 4 处修复（runtime_sync 路径 bug、Check 英文残留、switch 限定 [DlssNr] 区、引号注入）+ 9 个 bat/ps1 换行 CRLF；
- Check/switch 冒烟 exit 0；DLL 键表 12 键名全被基座识别；文档一致性 + 禁止字样清理；
- 159 文件 / 419.3MB；SHA256SUMS 158 条；DLL 基座零改动（1E386371…）。

## v1.4.39（2026-10-08）— 安装器 `& goto` 陷阱修复 + DX11 键补全
- setup_windows.bat 两处 `& goto` 陷阱修复（goto 无条件执行 → 逐条 if 匹配 + 重输）；ini `[Hooks]` 补 D3D11FeatureLevelElevation=auto；ini 整体恢复 CRLF（1973 行）；
- 158 文件 / 438.13MB；DLL 基座零改动（1E386371…）。

## v1.4.38（2026-10-08）— 8 脚本全量审查 + UI 大小默认自动
- 3 bat + 5 ps1 逐行全量审查（~1596 行）零 bug；UI 大小默认自动（MenuWidth/Height=auto + Scale=auto）；
- 158 文件 / 417.83MB；DLL 基座零改动（147f3738）。

## v1.4.37（2026-10-07）— 清单门控 + 路径加固
- 安装清单按 UNALL 门控写入卸载器 4 件；卸载器清单条目路径安全加固（findstr 拒绝 `..` 与盘符冒号）。

## v1.4.36（2026-10-07）— 深度精简定稿
- 合并重复功能与代码：FSR4 替换件 5→2 版、dlssg_unlock 3101 删除、可选分包取消；158 文件 / 417.83MB（zip l6）。

## v1.4.34 – v1.4.35（2026-10-07）— 组件集成 + 脚本解析
- standalone 组件集成（nvngx.ini 并入主线）；D3D11FeatureLevelElevation 等 F5 线可用修复并入；脚本全面解析与优化。

## v1.4.31 – v1.4.33（2026-10-06）— 代码优化 + 冲突修复
- 子串冲突修复（短串不再覆盖长串/已译串）；DLL UI 区 2231 条全覆盖确认；安装器块内 goto 闪退修复（v1.4.33 发布）。

## v1.4.28 – v1.4.30（2026-10-06）— 全面查 bug（六维审查）
- 版本线六维审查全绿；帧生成专项（后端识别 + 回退机制）；内置 MFG 解锁（20/30 系 4X）；画质保护基线固化进 ini。

## v1.4.25 – v1.4.27（2026-10-06）— 特制构建吸收 + 神经渲染补译
- 吸收 Juij 特制构建优点；神经渲染菜单补译；人物脸部渲染调节修复；FSR 4.1.1b INT8 说明；5X/6X 倍率协商说明。

## v1.4.20 – v1.4.22（2026-10-06）— 神经渲染基座线
- DLSSNR-F5 基座 0.1.27 重建汉化（2231 处 UI 串全量覆盖）；v1.4.22 组装 DLSSNR 基座线。

## v1.4.17 – v1.4.19（2026-10-06）— 安装/卸载器优化
- 数字键选择、安装器块内 goto 闪退修复；v1.4.19 卸载防误删（OriginalFilename 校验 + 拒绝路径穿越）。

## v1.4.8 – v1.4.16（2026-10-06）— 补译系列
- 每版按漏译扫描补译 UI 串（累计 100+ 处）；v1.4.12 切换 40serial-MFG 基座；UI 大小调整轮完成菜单适配。

## v1.4.7（2026-10-06）— UI 美化基线
- 基准蓝主题（AccentColor 0.20/0.44/1.00）、深蓝黑背景、微软雅黑 17.0、FPS 悬浮窗七模式；窗口可缩放、主题自动保存。

## v1.4.6（2026-10-06）— 可选增强组件解析与文档化
- 解析 bygalacos dev 线新构建 899b9488（无神经渲染，不替代基座）；组件查重：D3D12Core.dll + OptiPatcher.asi 包内已含；两组件默认不启用。

## v1.4.5（2026-10-06）— 全面解析 + 合并重复 + 精简体积（-46%)
- 精简：NR 默认切回官方原版 310.8；FSR4 替换件 5→2 版；dlssg_unlock 3101/3109→3109；docs 清理；997MB→694.5MB（RAW -30%）；zip level9 392.8MB（-46%）。

## v1.4.1（2026-10-05）— XeFG + SM + FSR4 替换件集成
- 新增 dlssg_unlock_3101 备用；新增 FSR4 自定义替换件 5 版；其余 109 文件与 v1.4.0 逐字节一致。

## v1.4.0（2026-10-05）— XeFG+SM 集成版
- 新增 dlssg_unlock_3109（RTX 20/30 系 DLSSG 解锁，310.9 驱动版，2X~6X）；新增 sm_unlock 家族；基底 v1.3.0 + 19 键 XeFG 性能预设；109 文件 / 781MB。

## v1.3.1（2026-10-05）— XeFG 性能优化预设
- 均衡档（默认，低风险）：日志关写盘 + 帧节奏 Tuning A + 最小生成帧队列 + XeSS 管线预构建 + ValidNow 关闭；激进档（可选）：UseMutexForSwapchain=false / ForceReflex=2 / FramerateLimit=0。

## v1.3.0（2026-10-05）— Lecram NR 模型
- NR 模型替换为 Lecram 调优版（f95feb54…，号称 20% 提升）；原模型同包备份可回退；其余 101 文件与 v1.2.0 逐字节一致。

## v1.2.0（2026-10-05）— 神经渲染基座
- 基座升级 OptiScaler v0.1.26-final（6d2189f1）；汉化 995 处（871 等长替换 + 124 超长精修）；补齐 streamline 全家桶等 46 项组件；103 文件 / 591MB。

## v1.1.0（2026-10-05）— v97e99b4c 基座
- 基座升级 v10.0.0-dev（97e99b4c）；汉化词典 445 条平移 + 组件补齐 60 文件 / 430MB。

## v1.0.0（2026-10-05）— 集成重构版首发
- 整目录扫描全部 OptiScaler 源包，选定 v97 dev 为基座；组件整合；规范第十五章建立。
---
*变更记录与汉化基准规范（OptiScaler汉化基准规范.md）同步演进。*