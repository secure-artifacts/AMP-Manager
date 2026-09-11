# AMP-Manager 更新记录

## V0.29 - 2026-06-19

- 收口 V0.28 之后的 VoiceDStudio 右侧管理栏弹窗模式、发送转发、提示静默与 CL 白名单面板联动优化。
- `VoiceDStudio/pageManager.js` 在右侧管理栏标题栏新增 `弹窗` 按钮，可打开专用 `VoiceDStudio/VoiceDStudioManager.html` 管理栏弹窗，不再打开完整 `VoiceDStudio.html` 设置页。
- 修复 `VoiceDStudioManager.html` 中内联脚本触发 Manifest V3 CSP 报错的问题，改为通过 `?mode=manager` 识别独立管理栏模式。
- 管理栏弹窗的 `发送` 按钮现在会通过后台转发到已打开的 `facebook.com/messages/t/*` 或 `messenger.com/t/*` 页面，由目标页面执行真实粘贴/发送；找不到消息页时会提示并复制到剪切板。
- 右侧管理栏自动注入、页面刷新和新页面加载时不再弹出“右侧管理栏已启用”提示；仅手动切换启用/关闭时显示提示。
- 右侧管理栏收起后的 `📱` 入口去掉渐变圆形背景、边框和阴影，仅保留图标本身，让页面更干净。
- `AMPManager/CLcontent.js` 的多成员说话检测白名单面板新增 `从高亮名单同步`，可读取 TextHighlighter 的 `categories` 关键词名单，只提取名单与分类，不导入颜色、标签等无关配置。
- TextHighlighter 内容脚本新增对 `data-amp-no-highlight="true"` 和 `#volume-whitelist-panel` 的跳过规则，避免 CL 白名单设置面板被关键词高亮污染。
- CL 白名单同步/导入名单支持按分类分组、折叠/展开、取消同步项勾选删除单项，以及点击半透明红色 `×` 删除整个分组及分组下所有名单。
- 本版仍不压缩、不替换任何图标资源，保持图标清晰度。
- `manifest.json` 内部版本更新为合法的 `0.29.0.0`，显示版本 `version_name` 为 `V0.29`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.29.zip`

## V0.28 - 2026-06-17

- 正式合并 `FBMemberAlert` 到 AMP-Manager，新增 `work/FBMemberAlert/` 模块目录，保留原插件的管理页、内容脚本、后台逻辑、样式和图标资源。
- 第 10 个槽位改为 `FB群成员监控`，主界面图标、设置图标、复选框提示和模块切换器全部接入 `FBMemberAlert/FBMemberAlert.html`。
- `checkbox10` 现在真正控制 FB 群成员监控启停：启用时注册并补注入 Facebook `messages/*`、`groupcall/*` 页面内容脚本；关闭时注销脚本并清理已注入页面的人数、气泡、扫描定时器和观察器。
- `FBMemberAlert` 后台以 `FBMA_` 消息前缀接入 AMP-Manager 主后台，通知图标路径适配子目录，避免与其他模块消息和角标逻辑冲突。
- `FBMemberAlert` 管理页接入 AMP-Manager 模块切换器，可从该页面快速切换到其他模块。
- `AMPManager/CLcontent.js` 在 Facebook 通话浮动菜单中新增 `📺 PiP画中画` 按钮，放在视频镜像按钮下方，方便直接切换当前通话视频画中画。
- 收口 V0.27 之后的 GTVideos 目标页面与状态反馈相关修复，继续保持视频分段播放器按 `checkbox8` 启停控制。
- 本版仍不压缩、不替换任何图标资源，保持图标清晰度。
- `manifest.json` 内部版本更新为合法的 `0.28.0.0`，显示版本 `version_name` 为 `V0.28`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.28.zip`

## V0.27 - 2026-06-17

- 修复 TextHighlighter 从 Google 表格导入关键词时可能漏掉第 5 行第一条关键词的问题。
- 导入逻辑现在从第 4 行开始扫描关键词列，并自动过滤空值；第 4 行作为说明/空行不会进入关键词，第 5 行会正常导入。
- TextHighlighter 将原来的 `仅背景高亮` 复选框/三段模式控件改为单个三态切换按钮。
- 高亮模式按钮现在按 `文字和背景 -> 仅背景高亮 -> 仅文本高亮` 循环切换，并分别使用绿色、蓝色、橙色渐变背景。
- 内容脚本继续使用 `highlightMode` 存储值执行三种模式，同时保留旧 `backgroundOnlyHighlight` 字段兼容。
- 高亮模式按钮放回原 `仅背景高亮` 复选框所在的右下角按钮位，保持操作区两行三列布局。
- `manifest.json` 内部版本更新为合法的 `0.27.0.0`，显示版本 `version_name` 为 `V0.27`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.27.zip`

## V0.26 - 2026-06-16

- 收口 V0.25 之后的界面精修与模块切换器稳定性修复，本版把多次源码确认后的 UI 调整统一发版。
- `AMP-Manager.html` 主界面恢复更接近原来的紫粉渐变气泡提示风格，修复复选框视觉错位和复选框提示、设置提示互相重叠的问题。
- 主界面模块设置小图标改为默认隐藏，鼠标悬停到模块图标时再显示，减少 25 个按钮界面的视觉干扰。
- 模块切换器按钮保持右上角原位置，其他右上角按钮避让它，避免和气泡提示、设置按钮抢位置。
- `Shared/module-switcher.js` 改为使用 Shadow DOM 挂载模块切换器，降低不同模块页面全局 CSS 对切换器的影响。
- `Shared/module-switcher.css` 强化样式隔离，固定切换器宽度约 360px、高度约 320px，并统一搜索框、列表行、当前模块蓝色高亮、图标和状态标签显示。
- 模块切换器主页入口图标使用 `🏠`，并保持原始图标清晰度，不做压缩或替换。
- `TextHighlighter/TextHighlighter.html` 清理已被覆盖且不再使用的旧样式，保留当前实际生效的紧凑管理面板样式，并添加参数注释方便后续手动调整。
- 高亮工具顶部统计移到标题后方，字号加大；重复数大于 0 时只把重复数字显示为红色。
- 高亮工具避免插件设置页面被自身关键词高亮，减少配置界面误高亮干扰。
- 高亮工具颜色选择框去掉中间默认边框并增加圆角，滚动条调整为细样式，同时修复宽度频闪问题。
- 高亮工具标签设置改为默认收起；`标签设置` 与 `启用标签` 同行显示，只有启用标签后才能展开配置；标签相关输入改为自动保存，不再需要单独保存按钮。
- 本版仍不压缩、不替换任何图标资源，保持图标清晰度。
- `manifest.json` 内部版本更新为合法的 `0.26.0.0`，显示版本 `version_name` 为 `V0.26`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.26.zip`
## V0.25 - 2026-06-16

- 收口 V0.24 之后的最后一批低风险共享 storage 整理，并完成打包前引用检查。
- `AudioLrc/AudioLrcPlayer.html` 调整脚本顺序，让 `Shared/storage.js` 在 `AudioLrcPlayer.js` 前可用；播放器原有共享 `xlsx` 加载保持不变。
- `AudioLrc/AudioLrcPlayer.js` 中已有的 `storeGet()` / `storeSet()` 通用封装改为优先使用 `AMP_STORAGE`，并保留 `chrome.storage.local` / `localStorage` 兜底；本版不迁移音量、输出设备、断点恢复等深层播放链路。
- `MuteList/MuteListManagement.html` 新增加载 `../Shared/storage.js`，静音黑名单、白名单和默认静音选项读写改为优先使用 `AMP_STORAGE`，键名保持不变。
- `WindowSettings/WindowSettings.html` 新增加载 `../Shared/storage.js`，窗口位置、窗口尺寸、清空设置和窗口排版参数读写改为优先使用 `AMP_STORAGE`。
- `WindowSettings/Windowslayou.js` 的保存链接读取、窗口排版参数、窗口类型复选框、自动返回标签页判断等存储读取改为优先使用共享 storage，窗口排列和标签页移动逻辑保持不变。
- `VoiceDStudio/VoiceDStudioGate.html` 调整脚本顺序为 `modules.js -> storage.js -> VoiceDStudioGate.js -> module-switcher.js`，入口页 `checkbox9` 读取和“启用并打开”改为优先使用 `AMP_STORAGE`。
- 收尾检查确认：manifest / content script / Shared modules 路径正常，模块清单页面和图标路径正常，模块切换器页面共享脚本顺序正常。
- 收尾检查确认：旧 `popup0.html`、`popup5.html`、`Popup/popup.html` 只剩 README 历史记录；`xlsx.full.min.js` 仍只保留 `Shared/vendor/xlsx.full.min.js` 一份。
- 本版仍不压缩、不替换任何图标资源，保持图标清晰度。
- `manifest.json` 内部版本更新为合法的 `0.25.0.0`，显示版本 `version_name` 为 `V0.25`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.25.zip`

## V0.24 - 2026-06-14

- 收口一批低风险共享化优化，本版把前面多次源码测试通过的改动统一发版。
- 新增 `Shared/storage.js`，提供 `AMP_STORAGE` 共享封装，统一 `local` / `sync` 存储的 Promise 调用方式，并保留原生 `chrome.storage` 回退。
- 主界面复选框、Options 默认界面选择、PiP 白名单设置、模块切换器、MWRelay、MuteAlerts、GVideos、GTVideos 独立页、AudioTranscriber 已接入共享 storage。
- 所有带模块切换器的模块页统一加载 `Shared/storage.js`，脚本顺序整理为 `modules.js -> storage.js -> 模块自身脚本 -> module-switcher.js`。
- `Shared/module-switcher.js` 读取模块启用状态时优先使用 `AMP_STORAGE.getLocal()`，各模块页面切换状态来源更统一。
- 合并重复的 `xlsx.full.min.js`，现在只保留 `Shared/vendor/xlsx.full.min.js` 一份；`manifest.json` 和 AudioLrc 都改为加载共享库。
- 删除旧副本 `AMPManager/xlsx.full.min.js` 与 `AudioLrc/xlsx.full.min.js`，避免后续维护三份相同第三方库。
- MuteAlerts 现在在 `blockedItems` 列表增删、导入、排序后会自动通知后台刷新屏蔽规则，不再需要手动关闭再开启开关。
- MuteAlerts 动态规则刷新改为先读取并清理现有动态规则，再写入最新规则，避免删除条目后旧规则残留。
- 后台图标右键“静音选项”复用统一窗口入口 `ampOpenSimpleWindow("muteBlacklist")`，减少重复窗口创建代码。
- 本版仍不迁移 VoiceDStudio、AudioLrc 主流程、AMOpenLink、通话页面内容脚本等复杂链路，避免影响已稳定的音频设备、frame 注入和通话相关功能。
- 本版不压缩、不替换任何图标资源，保持图标清晰度。
- `manifest.json` 内部版本更新为合法的 `0.24.0.0`，显示版本 `version_name` 为 `V0.24`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.24.zip`

## V0.23 - 2026-06-14

- 继续第二阶段“共享运行时 / 统一动态注入注册表”的整理，把 `checkbox8` GTVideos 纳入 `AMP_RUNTIME_MODULES`。
- GTVideos 保持原有点击时才注入当前网页的方式，不改为全局自动注入，避免影响普通网页加载和已稳定的分段播放器入口。
- `checkbox8` 关闭时会通过统一运行时钩子向已注入过 GTVideos 的标签页发送 `GT_HIDE_ALL`，自动隐藏右侧播放器和左侧编辑器面板。
- `GTVideos/GTVContent.js` 新增 `GT_HIDE_ALL` 消息处理，使用现有 `setAllVisible(false)` 收起两侧面板，避免关闭开关后页面上仍残留 GTVideos 界面。
- TextHighlighter、MWRelay、GTVideos、MuteAlerts 现在都进入统一运行时管理，其中 GTVideos 和 MuteAlerts 是无 content script 常驻注册的钩子型模块。
- 本版不压缩、不替换任何图标资源，保持图标清晰度。
- `manifest.json` 内部版本更新为合法的 `0.23.0.0`，显示版本 `version_name` 为 `V0.23`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.23.zip`

## V0.22 - 2026-06-13

- 继续第二阶段“共享运行时 / 统一动态注入注册表”的整理，把 `checkbox24` 提示音屏蔽纳入 `AMP_RUNTIME_MODULES`。
- `AMP_RUNTIME_MODULES` 现在支持没有 content script、只通过 `onEnable` / `onDisable` 执行启停逻辑的模块。
- `checkbox24` 通过 `onEnable: updateRules` 和 `onDisable: updateRules` 接入提示音屏蔽规则更新，原有动态规则生成和清空逻辑保持不变。
- 移除 `checkbox24` 独立的 `chrome.runtime.onInstalled(updateRules)` 与独立 storage change 监听，避免同一次开关变化触发两套重复规则更新。
- TextHighlighter、MWRelay、MuteAlerts 现在都统一由 `AMP_RUNTIME_MODULES` 处理开关同步。
- 本版仍不迁移 VoiceDStudio、GTVideos 的复杂链路，也不压缩或替换任何图标资源。
- `manifest.json` 内部版本更新为合法的 `0.22.0.0`，显示版本 `version_name` 为 `V0.22`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.22.zip`

## V0.21 - 2026-06-13

- 开始第二阶段“共享运行时 / 统一动态注入注册表”的低风险整理。
- `background.js` 新增 `AMP_RUNTIME_MODULES`，先统一管理已经使用 `chrome.scripting.registerContentScripts` 的 `checkbox3` 高亮工具和 `checkbox6` MWRelay。
- 移除旧的 `checkboxScriptsMap` 与 `updateScriptsByCheckbox()` 分散逻辑，改由 `ampSyncRuntimeModule()` / `ampSyncRuntimeModules()` 统一根据模块开关注册或注销 content scripts。
- 启用模块时会先注销同 ID 的旧动态脚本再重新注册，减少 Chrome 报“脚本 ID 已存在”导致脚本状态不同步的情况。
- `checkbox6` 的 Messenger / WhatsApp 转发监听器保留原行为，并通过 `onEnable` / `onDisable` 钩子接入运行时注册表。
- 本版暂不迁移 VoiceDStudio、GTVideos、MuteAlerts 的复杂链路，避免影响已修好的通话注入、右侧管理栏和提示音屏蔽规则。
- `manifest.json` 内部版本更新为合法的 `0.21.0.0`，显示版本 `version_name` 为 `V0.21`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.21.zip`

## V0.20 - 2026-06-13

- 继续做第五批低风险体验整理，优化共享模块切换器的列表展示。
- `Shared/module-switcher.js` 现在只显示已经接入真实页面 `url` 的模块，预留模块 10-23 不再出现在模块切换器列表中，避免误点“待开发”项。
- 主界面 25 个按钮和预留槽位保持不变，后续仍可继续接入新模块；新模块只要在 `Shared/modules.js` 中补上 `url`，就会自动出现在模块切换器里。
- 模块切换器搜索无结果时新增“没有匹配模块”提示，不再显示空白列表。
- `Shared/module-switcher.css` 新增 `.amp-ms-empty` 样式，保持空结果提示与 Apple 风格面板一致。
- `manifest.json` 内部版本更新为合法的 `0.20.0.0`，显示版本 `version_name` 为 `V0.20`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.20.zip`

## V0.19 - 2026-06-13

- 继续做第四批低风险稳定性整理，统一 Options 默认界面选择的数据来源。
- `Shared/modules.js` 新增 `AMP_INTERFACE_OPTIONS`，专门维护“插件图标默认打开哪个界面”的真实可用选项。
- `background.js` 的默认界面切换现在读取 `AMP_INTERFACE_OPTIONS`，不再在后台单独维护一份界面 URL 映射。
- `Options/options.html` 不再硬编码 `interface01~interface20` 空选项，默认界面列表由 `Options/options.js` 根据 `AMP_INTERFACE_OPTIONS` 动态渲染。
- 保留旧编号语义：`interface02` 仍是高亮工具，`interface03` 仍是 MSG 窗口布局，`interface04` 仍是提示音屏蔽，`interface09` 仍是 VoiceDStudio。
- 移除了 Options 中会让用户选到无真实页面的空编号，减少插件图标点击后回退或打开失败的可能。
- `manifest.json` 内部版本更新为合法的 `0.19.0.0`，显示版本 `version_name` 为 `V0.19`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.19.zip`

## V0.18 - 2026-06-13

- 继续做第三批低风险稳定性整理，本版不压缩、不替换任何图标资源，保持图标清晰度。
- `background.js` 新增 `AMP_SIMPLE_WINDOW_ACTIONS` 和 `ampOpenSimpleWindow()`，把多个简单的“打开模块窗口”入口集中到一张映射表维护。
- 已收口的简单窗口入口包括：音频录制、音频播放器、图片管理、主界面弹窗、高亮工具、静音名单、链接设置、MWRelay 设置、提示音屏蔽、使用教程、ReleaseNotes。
- 各模块原有窗口尺寸和打开方式保持不变，只减少重复的 `chrome.runtime.onMessage.addListener` 与重复 `chrome.windows.create` 代码。
- `openMWWindow` 这类需要读取 Messenger / WhatsApp 链接并打开网页标签页的特殊逻辑保持独立，不与简单窗口映射混合。
- 已确认统一映射表中的目标页面都真实存在，避免旧入口打开不存在页面。
- `manifest.json` 内部版本更新为合法的 `0.18.0.0`，显示版本 `version_name` 为 `V0.18`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.18.zip`

## V0.17 - 2026-06-13

- 继续做第二批低风险稳定性整理，统一主界面复选框状态管理。
- `AMP-Manager.html` 调整脚本加载顺序，现在先加载 `Shared/modules.js`，再加载 `AMP-Manager.js`，最后加载模块切换器。
- `AMP-Manager.js` 的 `checkboxIds` 不再手写固定数组，改为优先读取 `globalThis.AMP_MODULES` 中的 `enabledKey`，让主界面开关状态跟随共享模块清单。
- 对当前页面暂未渲染的预留模块复选框会自动过滤，避免后续新增模块前因为 DOM 不存在而报错。
- 增加兜底逻辑：如果共享模块清单加载异常，主界面会自动扫描页面中已有的 `checkbox*` 输入框继续保存/恢复状态。
- 该改动不改变现有 25 个按钮外观，也不改变 GTVideos、VoiceDStudio 等模块的运行逻辑，只减少后续新增模块时的漏改点。
- `manifest.json` 内部版本更新为合法的 `0.17.0.0`，显示版本 `version_name` 为 `V0.17`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.17.zip`

## V0.16 - 2026-06-13

- 做第一批低风险稳定性整理，为后续模块共用和继续接入新模块打基础。
- `Shared/modules.js` 现在改为挂载到 `globalThis.AMP_MODULES`，同一份模块清单可同时被普通页面和 background service worker 复用。
- `background.js` 启动时会通过 `importScripts("Shared/modules.js")` 读取共享模块清单，默认界面切换不再维护完全独立的一份硬编码页面有效性判断。
- 为保证兼容，Options 中已有的 `interface02 / interface03 / interface04 / interface09` 旧编号语义保持不变；后台只会通过共享模块清单确认目标页面存在。
- 修复旧入口 `OpenPopupM` 仍指向不存在的 `Popup/popup.html` 的问题，现在会打开真实存在的 `AMP-Manager.html` 主界面，避免旧页面按钮触发失败。
- 对没有真实页面的预留界面，插件图标默认弹窗会回退到 `AMP-Manager.html`，不再尝试打开不存在的 `popup0.html` 或 `popup5.html`。
- `manifest.json` 内部版本更新为合法的 `0.16.0.0`，显示版本 `version_name` 为 `V0.16`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.16.zip`

## V0.15 - 2026-06-13

- 优化共享模块切换器的触发按钮样式，按 Apple 风格进一步简化界面。
- `Shared/module-switcher.css` 中的 `📱` 模块切换按钮已去掉白色毛玻璃背景、边框、圆角容器和阴影，只保留图标本身。
- 鼠标悬停时不再显示按钮底色，仅保留轻微上移和缩放反馈，让页面右上角更干净。
- 模块切换弹出面板本身保持不变，仍可通过点击 `📱` 或 `Alt+Q` 打开。
- `manifest.json` 内部版本更新为合法的 `0.15.0.0`，显示版本 `version_name` 为 `V0.15`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.15.zip`

## V0.14 - 2026-06-13

- 调整 VoiceDStudio 右侧管理栏条目主区域的单击行为：现在会根据当前页面自动选择动作。
- 在 `https://www.facebook.com/groupcall/` 通话页面，单击条目主区域保持执行朗读；模板执行“粘贴朗读”，预设执行“朗读”。
- 在 `https://www.facebook.com/messages/t/` 和 `https://www.messenger.com/t/` 消息页面，单击条目主区域自动执行发送文本。
- 右侧独立按钮仍保持原功能不变：`发送` 按钮始终发送，`粘贴朗读/朗读` 按钮始终朗读，方便手动强制选择。
- 条目主区域的鼠标提示会随页面类型切换为“单击发送”或“单击朗读”。
- `manifest.json` 内部版本更新为合法的 `0.14.0.0`，显示版本 `version_name` 为 `V0.14`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.14.zip`

## V0.13 - 2026-06-13

- 修复 VoiceDStudio 右侧管理栏“已开启，但之后新打开/刷新 Facebook、Messenger、Instagram 页面不会自动加载”的问题。
- 后台动态脚本注册新增 `amp-voicedstudio-page-manager`，当 `checkbox9` 和 `fbvds_sideManagerEnabled` 同时开启时，Chrome 会在目标页面加载阶段自动注入 `VoiceDStudio/pageManager.js`。
- `fbvds_sideManagerEnabled` 状态变化现在也会触发 VoiceDStudio 动态脚本重新同步，避免只保存开关状态但没有更新自动注入规则。
- Facebook / Messenger / Instagram 页面加载完成后，后台会再执行一次轻量兜底注入并发送 `VDS_PAGE_MANAGER_V112_SET_ENABLED`，防止已打开页面或动态注册时机错过导致 📱 图标不出现。
- 关闭右侧管理栏时，后台通知消息统一改为 `VDS_PAGE_MANAGER_V112_SET_ENABLED`，与 V0.12 的新版 pageManager 消息链路保持一致。
- `manifest.json` 内部版本更新为合法的 `0.13.0.0`，显示版本 `version_name` 为 `V0.13`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.13.zip`

## V0.12 - 2026-06-13

- 修复 VoiceDStudio 右侧管理栏有时无法启动的问题。
- 启动右侧管理栏时现在始终先注入新版 `VoiceDStudio/pageManager.js`，再发送专用消息 `VDS_PAGE_MANAGER_V112_SET_ENABLED`，避免被 `VoiceDStudioContent.js` 中旧的 `VDS_PAGE_MANAGER_SET_ENABLED` 接收器抢先返回成功。
- `pageManager.js` 不再因为页面里残留旧的 `window.__VDS_PAGE_MANAGER_V051__` 标记就直接退出；扩展重载后会继续安装当前版本消息监听器，解决旧监听器失效但新脚本被标记挡住的问题。
- `pageManager.js` 新增 `window.__VDS_PAGE_MANAGER_HANDLER_V112__`，重复注入时会先移除旧监听器再绑定新监听器，避免重复响应。
- 右侧管理栏刷新消息同步改为 `VDS_PAGE_MANAGER_V112_REFRESH`，确保刷新也走新版 `pageManager.js`。
- `manifest.json` 内部版本更新为合法的 `0.12.0.0`，显示版本 `version_name` 为 `V0.12`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.12.zip`

## V0.11 - 2026-06-13

- 调整 VoiceDStudio 的核心注入时机：启用 `checkbox9` 后，后台会动态注册 VoiceDStudio 的页面脚本，让 `VoiceDStudio/pageHook.js` 在 Facebook / Messenger / Instagram 页面加载的 `document_start` 阶段进入 MAIN world。
- 同时注册 `VoiceDStudio/VoiceDStudioContent.js` 在 `document_start` 进入所有 frame，确保 content script 与 MAIN world hook 同页面生命周期启动。
- 关闭 `checkbox9` 时会注销 `amp-voicedstudio-page-hook` 和 `amp-voicedstudio-content` 两个动态脚本，保持第 9 个复选框对模块运行的控制。
- 该修复针对“设备列表可读取，但 TTS 通道注入失败”的场景：通话开始后再动态注入 pageHook 可能已经错过 Messenger 创建 `RTCPeerConnection` / audio sender 的时机，因此需要在进入通话页面前预先 hook。
- 使用方法：重新加载扩展并确认第 9 个复选框已启用后，刷新 Messenger/Facebook 通话页面，重新进入通话，再测试“手动切到 TTS 通道”或“语音朗读”。
- `manifest.json` 内部版本更新为合法的 `0.11.0.0`，显示版本 `version_name` 为 `V0.11`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.11.zip`
## V0.10 - 2026-06-13

- 修复 VoiceDStudio 已能读取设备列表但切换/注入 TTS 通道时提示“所有 frame 都没有成功响应当前操作”的问题。
- `VoiceDStudio/pageHook.js` 的 MAIN world 消息监听器现在支持自修复安装：即使页面里已有旧的 `__FBVDS_PAGE_HOOK_V028__` 标记，只要新的 `__FBVDS_PAGE_HOOK_HANDLER_V100__` 监听器不存在，重注入时也会重新安装消息监听器。
- 重注入时会先移除旧的 `__FBVDS_PAGE_HOOK_HANDLER_V100__`，再绑定新的 `message` 监听器，避免重复监听导致同一条 TTS 请求被多次处理。
- 该修复用于验证并解决 content script 已注入、但 MAIN world pageHook 没有响应 `FBVDS_STATUS` / `FBVDS_INJECT_TTS` 的情况。
- `manifest.json` 内部版本更新为合法的 `0.10.0.0`，显示版本 `version_name` 为 `V0.10`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.10.zip`
## V0.09 - 2026-06-13

- 修复 VoiceDStudio 消息被旧 `OpenExtension` 后台监听器抢先错误响应的问题。
- 原旧监听器会对所有没有 `action` 的消息返回 `{ status: "error", message: "无效的请求" }`；VoiceDStudio 使用的是 `type: "FBVDS_ENSURE_CONTENT"` / `type: "FBVDS_RELAY_TO_FRAMES"`，因此可能在真正的 VoiceDStudio 监听器处理前被错误抢答。
- 该监听器现在只处理 `action === "OpenExtension"` 的消息，其它消息直接忽略，让 VoiceDStudio 的 `FBVDS_*` 消息能正常进入自己的处理链路。
- 保留 V0.08 中参考 GTVideos 的当前活动页读取逻辑，作为 VoiceDStudio 目标页查找第一优先级。
- `manifest.json` 内部版本更新为合法的 `0.9.0.0`，显示版本 `version_name` 为 `V0.09`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.09.zip`
## V0.08 - 2026-06-13

- 参考 GTVideos 分段播放器的当前页面读取方式，修复 VoiceDStudio 从插件图标打开后仍提示未找到 Facebook / Messenger / Instagram 通话页的问题。
- VoiceDStudio 后台目标页查找新增 `ampGetCurrentWindowVoiceDStudioTab()`，优先执行 `chrome.tabs.query({ active: true, currentWindow: true })`，与 GTVideos 的 `AMP_GT_TOGGLE` 当前页获取方式保持一致。
- 只有当前窗口活动标签页不是支持页面时，才继续使用最近聚焦窗口、所有 Facebook / Messenger / Instagram 标签页扫描和历史缓存作为兜底。
- `manifest.json` 内部版本更新为合法的 `0.8.0.0`，显示版本 `version_name` 为 `V0.08`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.08.zip`

## V0.07 - 2026-06-13

- 继续修复 VoiceDStudio 从插件图标弹出时读取音频设备失败的问题。
- VoiceDStudio 后台监听器现在只处理自己的 `FBVDS_*` / `VOTS_*` 消息；对 `AMP_GET_VOICE_DSTUDIO_TARGET_TAB` 等其它消息不再错误地 `return true`，避免前台请求目标标签页时被挂起。
- VoiceDStudio 前台 `ensureFbReady()` 不再先检查当前 popup 窗口的 active tab，而是直接让后台按已记录的 Facebook / Messenger / Instagram 目标标签页注入并通信。
- VoiceDStudio 前台 `activeTab()` 现在会优先读取当前 Chrome 活动标签页；如果当前页就是 Facebook / Messenger / Instagram 通话页，会直接把该 tabId 传给后台。
- VoiceDStudio 的 `FBVDS_ENSURE_CONTENT`、`FBVDS_RELAY_TO_FRAMES`、`FBVDS_REINJECT_PAGE_HOOK` 请求现在都会携带明确的通话页 tabId，避免通过插件图标 popup 打开后后台误判目标页面。
- `manifest.json` 内部版本更新为合法的 `0.7.0.0`，显示版本 `version_name` 为 `V0.07`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.07.zip`
## V0.06 - 2026-06-13

- 修复 VoiceDStudio 合并后在独立 popup 窗口中读取音频设备失败的问题。
- 打开 VoiceDStudio 时会记录当前 Facebook / Messenger / Instagram 目标标签页；后续读取设备、注入页面脚本、TTS 注入和状态检查都会优先使用该目标标签页，而不是 VoiceDStudio 自己的弹窗页面。
- 新增 `AMP_GET_VOICE_DSTUDIO_TARGET_TAB` 后台消息，用于 VoiceDStudio 前台页面获取正确目标标签页。
- VoiceDStudio 后台消息处理改为使用记录的目标标签页，避免 `currentWindow` 指向扩展 popup 窗口导致设备读取失败。
- 整理 `checkbox9` 门禁逻辑到 VoiceDStudio 后台消息入口处，避免在 frame 循环里重复判断。
- `manifest.json` 内部版本更新为合法的 `0.6.0.0`，显示版本 `version_name` 为 `V0.06`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.06.zip`
## V0.05 - 2026-06-13

- 模块切换器按钮从九宫格改为 `📱` 小图标。
- 模块切换器改为 Apple 风格玻璃质感：半透明背景、柔和阴影、圆角和系统字体。
- 模块切换器新增窗口类型判断：在通过插件图标打开的扩展页面中显示；在 `chrome.windows.create({ type: "popup" })` 打开的独立工具窗口中自动隐藏，避免遮挡 GTVideos、VoiceDStudio 等工具窗口内容。
- 保留已接入页面的切换器引用，后续如果某个模块被设置为插件图标默认界面，仍然可以显示切换入口。
- `manifest.json` 内部版本更新为合法的 `0.5.0.0`，显示版本 `version_name` 为 `V0.05`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.05.zip`
## V0.04 - 2026-06-13

- 新增全局模块切换器，支持在已接入的模块页面右上角随时切换到其它模块页面。
- 新增 `Shared/modules.js`、`Shared/module-switcher.css`、`Shared/module-switcher.js`，统一维护 25 个模块位、模块页面路径、图标和对应复选框开关。
- 切换器支持点击右上角九宫格按钮打开，也支持快捷键 `Alt+Q` 打开，支持按编号或名称搜索。
- 切换器顶部固定提供 `AMP Manager 主界面`，方便从任意模块返回主页面。
- 未启用的模块会显示为灰色，点击时提示先在主界面启用对应复选框，不绕过现有复选框管理规则。
- 已接入页面：主界面、Options、图片管理、音频录制、高亮工具、双语翻译、MSG窗口布局、MW消息传递、音频播放器、视频分段播放器、VoiceDStudio、提示音屏蔽、使用教程。
- `manifest.json` 内部版本更新为合法的 `0.4.0.0`，显示版本 `version_name` 为 `V0.04`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.04.zip`
## V0.03 - 2026-06-12

- 修复 Options 默认界面 `interface09` 未接入 VoiceDStudio 的问题。
- `background.js` 的 `setPopupPage()` 现在会将 `interface09` 指向 `VoiceDStudio/VoiceDStudioGate.html`。
- 新增 `VoiceDStudioGate.html` / `VoiceDStudioGate.js`：已启用 `checkbox9` 时自动进入 VoiceDStudio；未启用时提示启用，避免默认界面入口绕过第 9 个复选框总开关。
- Options 默认界面列表中 `09` 更新为 `09 VoiceDStudio`。
- `manifest.json` 内部版本更新为合法的 `0.3.0.0`，显示版本 `version_name` 为 `V0.03`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.03.zip`
## V0.02 - 2026-06-12

- 将 VoiceDStudioV0.99 整合到 AMP-Manager 第 9 个按钮位。
- `checkbox9` 作为 VoiceDStudio 模块总开关：未勾选时主页面不打开 VoiceDStudio，后台也拒绝 VoiceDStudio 注入和 TTS 消息。
- 第 9 个图标按钮和设置按钮都会打开 `VoiceDStudio/VoiceDStudio.html`。
- VoiceDStudio 原 `pageHook.js`、`VoiceDStudioContent.js`、`pageManager.js` 改为按需动态注入，不写入 AMP-Manager 的常驻 `content_scripts`。
- VoiceDStudio 原后台消息、offscreen TTS 生成、缓存统计和页面 frame 转发逻辑已并入 AMP-Manager 后台，并修正为 `VoiceDStudio/...` 子目录路径。
- 取消勾选 `checkbox9` 时，会尝试通知已打开的 Facebook / Messenger / Instagram 页面关闭 VoiceDStudio 右侧管理栏。
- `manifest.json` 增加 VoiceDStudio 需要的 `offscreen` 权限；内部版本更新为合法的 `0.2.0.0`，显示版本 `version_name` 为 `V0.02`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.02.zip`
## V0.01 - 2026-06-12

- 修复 `checkbox8` 之前只保存状态、不能真正控制 GTVideos 的问题。
- 主页面点击「视频分段播放器」前会先检查 `checkbox8`，未勾选时不再发送启动请求。
- 后台 `AMP_GT_TOGGLE` 处理逻辑新增 `checkbox8` 二次校验，防止其它入口绕过主页面开关。
- 从 `manifest.json` 常驻内容脚本中移除 `GTVideos/GTVContent.js`，改为启用后按需动态注入，避免未启用时自动运行。
- `manifest.json` 内部更新版本为合法的 `0.1.0.0`，显示版本 `version_name` 为 `V0.01`。
- 打包输出：`D:\ChromeExtension\AMP-Manager\outputs\AMP-Manager_V0.01.zip`
# AMP-Manager 测试版更新记录

## V1.31 - 2026-06-12

- TextHighlighter 在导入按钮后新增 `仅背景高亮` 选项。
- 开启后，网页高亮只设置背景色，不再强制设置文字颜色和加粗，文字样式保留网页原样。
- `仅背景高亮` 设置会保存到 `chrome.storage.local`，下次打开仍会保留。
- 高亮内容脚本会读取该设置；设置变化后会重新应用当前页面高亮。
- 预览区会根据该选项同步显示仅背景高亮效果。
- `manifest.json` 版本号更新为 `1.31`。
- 打包输出：`D:\ChromeExtension\FB插件\@XJ编写插件\@AMP-Manager工具合集\outputs\AMP-Manager-测试版_V1.31.zip`

## V1.30 - 2026-06-12

- TextHighlighter 表格导入关键词读取起始行从第 4 行改为第 5 行。
- 现在表格结构为：第 1 行分类名称，第 2 行背景色，第 3 行文字色，第 4 行预留/说明，第 5 行开始为关键词内容。
- `manifest.json` 版本号更新为 `1.30`。
- 打包输出：`D:\ChromeExtension\FB插件\@XJ编写插件\@AMP-Manager工具合集\outputs\AMP-Manager-测试版_V1.30.zip`

## V1.29 - 2026-06-12

- TextHighlighter 标题栏右侧新增关键词统计显示。
- 统计当前分类的非空关键词数量，格式为 `共 36 个关键词 / 重复 3 个`。
- 关键词统计会在加载分类、切换分类、输入关键词、保存后自动刷新。
- 重复数量按忽略大小写后的重复行数量计算，空行不计入统计。
- `manifest.json` 版本号更新为 `1.29`。
- 打包输出：`D:\ChromeExtension\FB插件\@XJ编写插件\@AMP-Manager工具合集\outputs\AMP-Manager-测试版_V1.29.zip`

## V1.28 - 2026-06-12

- 重新设计 TextHighlighter 高亮设置界面，改为更紧凑的 360px 管理面板。
- 整理界面视觉层：统一边框、按钮、输入框、颜色选择、预览区和右键菜单样式。
- 将分类选择、增删分类、关键词编辑、颜色预览、保存/导入/导出/表格操作重新排布为更清晰的工具布局。
- 修复自定义标签设置折叠区点击后会破坏标题和箭头结构的问题。
- `manifest.json` 版本号更新为 `1.28`。
- 打包输出：`D:\ChromeExtension\FB插件\@XJ编写插件\@AMP-Manager工具合集\outputs\AMP-Manager-测试版_V1.28.zip`

## V1.27 - 2026-06-12

- 修复 TextHighlighter 高亮逻辑会处理 Facebook/Messenger 输入框的问题。
- 高亮脚本现在会跳过 `input`、`textarea`、`contenteditable`、`role="textbox"` 等可编辑区域。
- 高亮脚本现在会跳过 `combobox`、`listbox`、`option`、提及候选框等节点，避免输入 `@姓名` 时文字马上消失。
- 动态 DOM 监听新增节点时，会先判断是否属于输入区或候选框，再决定是否高亮。
- 异步 tooltip 处理前增加节点状态检查，避免节点已变化后继续替换。
- `manifest.json` 版本号更新为 `1.27`。
- 打包输出：`D:\ChromeExtension\FB插件\@XJ编写插件\@AMP-Manager工具合集\outputs\AMP-Manager-测试版_V1.27.zip`






