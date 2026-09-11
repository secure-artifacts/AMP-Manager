# AMP-Manager 更新记录

## V0.29 - 2026-06-19

- 收口 V0.28 之后的 VoiceDStudio 右侧管理栏弹窗模式、发送转发、提示静默与 CL 白名单面板联动优化。
- `VoiceDStudio/pageManager.js` 在右侧管理栏标题栏新增 `弹窗` 按钮，可打开专用 `VoiceDStudio/VoiceDStudioManager.html` 管理栏弹窗，不再打开完整 `VoiceDStudio.html` 设置页。

## V0.28 - 2026-06-17

- 正式合并 `FBMemberAlert` 到 AMP-Manager，新增 `work/FBMemberAlert/` 模块目录，保留原插件的管理页、内容脚本、后台逻辑、样式和图标资源。
- 第 10 个槽位改为 `FB群成员监控`，主界面图标、设置图标、复选框提示和模块切换器全部接入 `FBMemberAlert/FBMemberAlert.html`。

## V0.27 - 2026-06-17

- 修复 TextHighlighter 从 Google 表格导入关键词时可能漏掉第 5 行第一条关键词的问题。
- 导入逻辑现在从第 4 行开始扫描关键词列，并自动过滤空值；第 4 行作为说明/空行不会进入关键词，第 5 行会正常导入。

## V0.26 - 2026-06-16

- 收口 V0.25 之后的界面精修与模块切换器稳定性修复，本版把多次源码确认后的 UI 调整统一发版。
- `AMP-Manager.html` 主界面恢复更接近原来的紫粉渐变气泡提示风格，修复复选框视觉错位和复选框提示、设置提示互相重叠的问题。

## V0.25 - 2026-06-16

- 收口 V0.24 之后的最后一批低风险共享 storage 整理，并完成打包前引用检查。
- `AudioLrc/AudioLrcPlayer.html` 调整脚本顺序，让 `Shared/storage.js` 在 `AudioLrcPlayer.js` 前可用；播放器原有共享 `xlsx` 加载保持不变。

## V0.24 - 2026-06-14

- 收口一批低风险共享化优化，本版把前面多次源码测试通过的改动统一发版。
- 新增 `Shared/storage.js`，提供 `AMP_STORAGE` 共享封装，统一 `local` / `sync` 存储的 Promise 调用方式，并保留原生 `chrome.storage` 回退。
- 合并重复的 `xlsx.full.min.js`，现在只保留 `Shared/vendor/xlsx.full.min.js` 一份；`manifest.json` 和 AudioLrc 都改为加载共享库。

## V0.23 - 2026-06-14

- 继续第二阶段“共享运行时 / 统一动态注入注册表”的整理，把 `checkbox8` GTVideos 纳入 `AMP_RUNTIME_MODULES`。
- GTVideos 保持原有点击时才注入当前网页的方式，不改为全局自动注入，避免影响普通网页加载和已稳定的分段播放器入口。

## V0.22 - 2026-06-13

- 继续第二阶段“共享运行时 / 统一动态注入注册表”的整理，把 `checkbox24` 提示音屏蔽纳入 `AMP_RUNTIME_MODULES`。
- `AMP_RUNTIME_MODULES` 现在支持没有 content script、只通过 `onEnable` / `onDisable` 执行启停逻辑的模块。

## V0.21 - 2026-06-13

- 开始第二阶段“共享运行时 / 统一动态注入注册表”的低风险整理。
- `background.js` 新增 `AMP_RUNTIME_MODULES`，先统一管理已经使用 `chrome.scripting.registerContentScripts` 的 `checkbox3` 高亮工具和 `checkbox6` MWRelay。

## V0.20 - 2026-06-13

- 继续做第五批低风险体验整理，优化共享模块切换器的列表展示。
- `Shared/module-switcher.js` 现在只显示已经接入真实页面 `url` 的模块，预留模块 10-23 不再出现在模块切换器列表中，避免误点“待开发”项。

## V0.19 - 2026-06-13

- 继续做第四批低风险稳定性整理，统一 Options 默认界面选择的数据来源。
- `Shared/modules.js` 新增 `AMP_INTERFACE_OPTIONS`，专门维护“插件图标默认打开哪个界面”的真实可用选项。

## V0.18 - 2026-06-13

- 继续做第三批低风险稳定性整理，本版不压缩、不替换任何图标资源，保持图标清晰度。
- `background.js` 新增 `AMP_SIMPLE_WINDOW_ACTIONS` 和 `ampOpenSimpleWindow()`，把多个简单的“打开模块窗口”入口集中到一张映射表维护。

## V0.17 - 2026-06-13

- 继续做第二批低风险稳定性整理，统一主界面复选框状态管理。
- `AMP-Manager.html` 调整脚本加载顺序，现在先加载 `Shared/modules.js`，再加载 `AMP-Manager.js`，最后加载模块切换器。

## V0.16 - 2026-06-13

- 做第一批低风险稳定性整理，为后续模块共用和继续接入新模块打基础。
- `Shared/modules.js` 现在改为挂载到 `globalThis.AMP_MODULES`，同一份模块清单可同时被普通页面和 background service worker 复用。

## V0.15 - 2026-06-13

- 优化共享模块切换器的触发按钮样式，按 Apple 风格进一步简化界面。
- `Shared/module-switcher.css` 中的 `📱` 模块切换按钮已去掉白色毛玻璃背景、边框、圆角容器和阴影，只保留图标本身。

## V0.14 - 2026-06-13

- 调整 VoiceDStudio 右侧管理栏条目主区域的单击行为：现在会根据当前页面自动选择动作。
- 在 `https://www.facebook.com/groupcall/` 通话页面，单击条目主区域保持执行朗读；模板执行“粘贴朗读”，预设执行“朗读”。

## V0.13 - 2026-06-13

- 修复 VoiceDStudio 右侧管理栏“已开启，但之后新打开/刷新 Facebook、Messenger、Instagram 页面不会自动加载”的问题。
- 后台动态脚本注册新增 `amp-voicedstudio-page-manager`，当 `checkbox9` 和 `fbvds_sideManagerEnabled` 同时开启时，Chrome 会在目标页面加载阶段自动注入 `VoiceDStudio/pageManager.js`。

## V0.12 - 2026-06-13

- 修复 VoiceDStudio 右侧管理栏有时无法启动的问题。
- 启动右侧管理栏时现在始终先注入新版 `VoiceDStudio/pageManager.js`，再发送专用消息 `VDS_PAGE_MANAGER_V112_SET_ENABLED`，避免被 `VoiceDStudioContent.js` 中旧的 `VDS_PAGE_MANAGER_SET_ENABLED` 接收器抢先返回成功。

## V0.11 - 2026-06-13

- 调整 VoiceDStudio 的核心注入时机：启用 `checkbox9` 后，后台会动态注册 VoiceDStudio 的页面脚本，让 `VoiceDStudio/pageHook.js` 在 Facebook / Messenger / Instagram 页面加载的 `document_start` 阶段进入 MAIN world。
- 同时注册 `VoiceDStudio/VoiceDStudioContent.js` 在 `document_start` 进入所有 frame，确保 content script 与 MAIN world hook 同页面生命周期启动。

## V0.10 - 2026-06-13

- 修复 VoiceDStudio 已能读取设备列表但切换/注入 TTS 通道时提示“所有 frame 都没有成功响应当前操作”的问题。
- `VoiceDStudio/pageHook.js` 的 MAIN world 消息监听器现在支持自修复安装：即使页面里已有旧的 `__FBVDS_PAGE_HOOK_V028__` 标记，只要新的 `__FBVDS_PAGE_HOOK_HANDLER_V100__` 监听器不存在，重注入时也会重新安装消息监听器。

## V0.09 - 2026-06-13

- 修复 VoiceDStudio 消息被旧 `OpenExtension` 后台监听器抢先错误响应的问题。
- 原旧监听器会对所有没有 `action` 的消息返回 `{ status: "error", message: "无效的请求" }`；VoiceDStudio 使用的是 `type: "FBVDS_ENSURE_CONTENT"` / `type: "FBVDS_RELAY_TO_FRAMES"`，因此可能在真正的 VoiceDStudio 监听器处理前被错误抢答。

## V0.08 - 2026-06-13

- 参考 GTVideos 分段播放器的当前页面读取方式，修复 VoiceDStudio 从插件图标打开后仍提示未找到 Facebook / Messenger / Instagram 通话页的问题。
- VoiceDStudio 后台目标页查找新增 `ampGetCurrentWindowVoiceDStudioTab()`，优先执行 `chrome.tabs.query({ active: true, currentWindow: true })`，与 GTVideos 的 `AMP_GT_TOGGLE` 当前页获取方式保持一致。

## V0.07 - 2026-06-13

- 继续修复 VoiceDStudio 从插件图标弹出时读取音频设备失败的问题。
- VoiceDStudio 后台监听器现在只处理自己的 `FBVDS_*` / `VOTS_*` 消息；对 `AMP_GET_VOICE_DSTUDIO_TARGET_TAB` 等其它消息不再错误地 `return true`，避免前台请求目标标签页时被挂起。

## V0.06 - 2026-06-13

- 修复 VoiceDStudio 合并后在独立 popup 窗口中读取音频设备失败的问题。
- 打开 VoiceDStudio 时会记录当前 Facebook / Messenger / Instagram 目标标签页；后续读取设备、注入页面脚本、TTS 注入和状态检查都会优先使用该目标标签页，而不是 VoiceDStudio 自己的弹窗页面。

## V0.05 - 2026-06-13

- 模块切换器按钮从九宫格改为 `📱` 小图标。
- 模块切换器改为 Apple 风格玻璃质感：半透明背景、柔和阴影、圆角和系统字体。

## V0.04 - 2026-06-13

- 新增全局模块切换器，支持在已接入的模块页面右上角随时切换到其它模块页面。
- 新增 `Shared/modules.js`、`Shared/module-switcher.css`、`Shared/module-switcher.js`，统一维护 25 个模块位、模块页面路径、图标和对应复选框开关。

## V0.03 - 2026-06-12

- 修复 Options 默认界面 `interface09` 未接入 VoiceDStudio 的问题。
- `background.js` 的 `setPopupPage()` 现在会将 `interface09` 指向 `VoiceDStudio/VoiceDStudioGate.html`。

## V0.02 - 2026-06-12

- 将 VoiceDStudioV0.99 整合到 AMP-Manager 第 9 个按钮位。
- `checkbox9` 作为 VoiceDStudio 模块总开关：未勾选时主页面不打开 VoiceDStudio，后台也拒绝 VoiceDStudio 注入和 TTS 消息。
- `manifest.json` 增加 VoiceDStudio 所需的 `offscreen` 权限。

## V0.01 - 2026-06-12

- 修复 `checkbox8` 之前只保存状态、不能真正控制 GTVideos 的问题。
- 主页面点击「视频分段播放器」前会先检查 `checkbox8`，未勾选时不再发送启动请求。
- 从 `manifest.json` 常驻内容脚本中移除 `GTVideos/GTVContent.js`，改为启用后按需动态注入，避免未启用时自动运行。

# AMP-Manager 测试版更新记录

## V1.31 - 2026-06-12

- TextHighlighter 在导入按钮后新增 `仅背景高亮` 选项。
- 开启后，网页高亮只设置背景色，不再强制设置文字颜色和加粗，文字样式保留网页原样。

## V1.30 - 2026-06-12

- TextHighlighter 表格导入关键词读取起始行从第 4 行改为第 5 行。
- 现在表格结构为：第 1 行分类名称，第 2 行背景色，第 3 行文字色，第 4 行预留/说明，第 5 行开始为关键词内容。

## V1.29 - 2026-06-12

- TextHighlighter 标题栏右侧新增关键词统计显示。
- 统计当前分类的非空关键词数量，格式为 `共 36 个关键词 / 重复 3 个`。

## V1.28 - 2026-06-12

- 重新设计 TextHighlighter 高亮设置界面，改为更紧凑的 360px 管理面板。
- 整理界面视觉层：统一边框、按钮、输入框、颜色选择、预览区和右键菜单样式。

## V1.27 - 2026-06-12

- 修复 TextHighlighter 高亮逻辑会处理 Facebook/Messenger 输入框的问题。
- 高亮脚本现在会跳过 `input`、`textarea`、`contenteditable`、`role="textbox"` 等可编辑区域。
