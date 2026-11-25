# 走不走 v0.6.4 / GoGoGo v0.6.4

## 中文

### 本次更新

- **输入不再错乱、空框稳定一行**：H5、Android、微信、抖音的空输入框统一为 44px 单行，不再因长占位、原生内边距或自增高测量出现两行与高度跳动；长文本最多增高到 120px 后内部滚动。
- **中文输入法与光标更可靠**：H5/Android 保留系统输入法，组合输入期间不回写高度或光标，确认候选的回车不会误发送，Shift+Enter 换行；微信/抖音改为半受控输入，键盘回车只换行，发送只由右下按钮触发，并显式关闭键盘确认栏与默认内边距。
- **全部产品文本输入共用安全输入层**：主对话、地点搜索、自定义忌口、群局想法、行程标题、账户邮箱/验证码/密码等入口遵循同一组合输入与显式提交规则；小程序搜索和保存不再依赖键盘回车。
- **等待状态更诚实**：删除流式伪光标，`AgentLiveBar` 成为唯一“正在工作”信号；没有真实内容的空回复不再闪烁光标，零内容结束会按“这次回复中断”处理。
- **顶部提醒统一、可关闭、不挤动页面**：成功/操作错误从顶部悬浮卡片出现，成功约 2.5 秒、错误约 6 秒后自动消失，均可手动关闭；同时只显示一张、队列深度 2，弹窗内也可见，且不改变内容高度或滚动位置。产品内不再使用原生 toast。
- **进入会话就在最新消息**：打开会话、切换会话、切回“拍板”页或从后台恢复，都直接定位到最新消息底部；流式生成只在用户本来就在底部时跟随。
- **上滑阅读不被打断**：用户上滑后暂停自动跟随，出现 44px 圆形下箭头按钮；点击平滑回底并恢复跟随。旧的“查看新消息”长条与未读数量已删除。
- **失败原因看得懂、能恢复**：发送失败只在对应消息下方显示图标、原因与恢复动作，并保留消息内容与草稿；网络状态未知时先“检查发送状态”，确认未送达后才出现“重试”，避免重复消息。401 登录失效与 429 限流直接给出对应说明，不提供盲目重试。助手回复中断使用结构化中断卡；用户文案不暴露错误码，未捕获渲染错误有统一回退界面。
- **复制结果不再假报成功**：H5/APP 复制改走原生 Clipboard API，微信/抖音保留宿主剪贴板；复制失败会明确提示，不再声称“已复制”。H5/APP 不再触发 Taro 内部“内容已复制”toast；小程序宿主自身可能仍显示系统剪贴板提示。
- **触控与弹窗可访问性**：顶部提示移到顶栏下方，不再遮挡历史/定位/新对话按钮；提示关闭、失败重试、检查状态、放回输入框、启动卡胶囊与“加入朋友的群拍板”均达到至少 44×44px。历史对话面板补齐 `dialog`/`aria-modal`、焦点进入与回路、Tab 限制、Escape 关闭和焦点恢复。

### 平台

- **Web H5**：<https://gogogo.plutokeating.beer/>（Pages 生产部署 `b9015b90`）
- **Android**：签名 Universal APK 与 `arm64-v8a` APK，`versionCode 6004`，9,951,090 bytes，支持覆盖安装。两个 APK 当前字节完全相同，因为本版本没有 native `.so` 负载，不代表两者包含不同 ABI 代码。
  - Universal：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.4/GoGoGo-0.6.4-android-universal.apk>，SHA-256 `ee87d57281d2b7a08b49a3becbf036442edbfa84fa9725e49a46b46563c7e7d9`
  - arm64-v8a：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.4/GoGoGo-0.6.4-android-arm64-v8a.apk>，SHA-256 `ee87d57281d2b7a08b49a3becbf036442edbfa84fa9725e49a46b46563c7e7d9`
- **微信小程序**：`0.6.4` 体验版已上传（`2026-11-25T08:52:10Z`，产物 SHA-256 `87557f37…56ca8`；回执见 `docs/operations/wechat-mini-program/releases/2026-11-25-0.6.4.json`）。
- **抖音小程序**：`0.6.4` 预览版已上传（回执见 `docs/operations/douyin-mini-program/releases/2026-11-25-0.6.4.json`；预览短链 <https://t.zijieimg.com/i4JpAoU6/>；二维码 `frontend/dist/tt-upload/qrcode-0.6.4.png`，平台未返回明确到期时间）。
- **iOS**：仍缺少 Apple 分发签名配置，本版本没有 IPA。

### 兼容性与迁移

- 无数据库迁移、无 API 契约变化、无后端协议或消息 schema 变化；本轮不需要部署新的 Worker。
- 账户、本机私人档案、本地会话与草稿的存储格式保持不变；升级不需要清理缓存或重新登录。
- H5、Android、微信、抖音共用同一业务代码与 `Plan` v2 行程契约。

### 验证范围与已知限制

- H5：无头端到端与 Node 门禁覆盖输入高度/占位/组合输入、草稿所有权、失败恢复/401/429 分类、顶部提醒（含同 key 成功→失败重绘）、滚动跟随、圆形回底按钮、历史面板焦点语义、44px 触控目标与错误状态行，视口包含 320/390/1440；`h5-canonical` 连续三次通过。
- 微信/抖音：使用正式 API 地址构建，产物门禁检查 `showConfirmBar=false`、`disableDefaultPadding=true`、`fixed=true`、`cursor=-1`、`confirmType="return"`、`adjustPosition=false`、`holdKeyboard=true` 与键盘高度绑定，并确认不存在 composer 的键盘发送路径。
- Android：0.6.4 双签名 APK 通过静态证书、权限、正式资源与版本门禁；在无头 Android 14 模拟器完成 0.6.4 安装、首启隐私页、进程存活、版本号 0.6.4 与零 fatal log 检查。完整 `check:android-startup` 在真实模型生成行程卡阶段超时两次，因此本次不声称“完整 0.6.4 CDP 行程验收”；Task 6 在同一业务代码的 0.6.3 构建上通过过完整 startup。
- **本轮验证仅限无头环境**：没有执行桌面 GUI、微信/抖音开发者工具或可见浏览器人工验收，也没有真机输入法矩阵。视觉复验由 headless Chromium 在 320/390/1440 完成并判定 PASS。
- 尚未覆盖、仍需真机或后续发布补充的项目：
  - 微信/抖音开发者工具与真机的英文/中文输入法、快速输入、中段编辑、键盘不遮挡输入条；
  - 微信 iOS 原生拼音的 `onInput` 抑制、SelectorQuery 回读与候选确认；微信 Android 第三方输入法的光标跳动/旧值闪烁；
  - 账户邮箱、验证码与密码在真实设备、真实账户下的输入；
  - 中文输入法组合过程与候选确认在真实 iOS/Android 键盘上的表现；
  - iOS 微信原生拼音与 iOS 覆盖层/键盘行为；
  - 小程序 `autoHeight` 的 `max-height`、`CustomWrapper` A/B、抖音 `disableDefaultPadding` 真机差异；
  - 小程序 `ScrollView` 的初始底部、流式跟随、`scroll-into-view` 重复触发、状态条出现/消失与图片/卡片高度增长；
  - 小程序键盘打开时发送按钮是否仍可点击、`--keyboard-inset` 是否随宿主键盘正确上移；
  - 小程序 320px 空输入框的真实运行时高度与 mini nav island + 圆形按钮几何；
  - 无可靠 `visualViewport` 事件的 Android WebView 与真实中文 IME 组合；
  - 实体 Android 多 OEM 输入法；
  - 小程序宿主剪贴板自身的系统 toast；
  - 公开 `v0.6.4` Release 与下载页回验：发布后由无认证 latest API、匿名附件下载与下载页检查完成，回验记录写入源码仓库 `docs/operations/github-releases/2026-11-25-0.6.4.md`。

### 发布资源

- 源码标签：`v0.6.4`；源码提交以 `release-manifest.json` 的 `sourceCommit` 为准。
- 公开发行仓库标签：`v0.6.4`。
- 发行清单 `release-manifest.json` 与 `SHA256SUMS` 作为本 Release 附件提供。
- 正式 Release：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/tag/v0.6.4>

---

## English

### What changed

- **Input no longer corrupts, and an empty box stays one line**: H5, Android, WeChat, and Douyin now render the empty composer as a single 44px line instead of collapsing to two lines or jumping because of a long placeholder, native padding, or auto-height measurement. Long drafts grow only to 120px, then scroll inside the field.
- **More reliable Chinese IME and caret behavior**: H5/Android keep the system input method; height and caret are not rewritten during composition, Enter that confirms an IME candidate does not send, and Shift+Enter inserts a newline. WeChat/Douyin use a semi-controlled native input where the keyboard Return key only inserts a newline and the bottom-right button is the only send path; the keyboard confirm bar and default padding are explicitly disabled.
- **Every product text field shares the safe input layer**: the main composer, location search, custom dietary restrictions, group ideas, itinerary title, and account email/code/password fields follow the same composition-safety and explicit-submit rules. Mini-program search and save no longer depend on the keyboard Return key.
- **Honest waiting state**: the fake streaming caret is removed and `AgentLiveBar` is the only “working” signal. An empty assistant turn no longer blinks a caret; a zero-block completion is treated as an interrupted reply.
- **One top notice surface, dismissible, no layout shift**: success and operation errors appear as a floating top card. Success clears after about 2.5s and errors after about 6s, both can be dismissed manually, only one card is visible with a queue depth of 2, modal contents can still show them, and page height or scroll position never moves. Product screens no longer use native toasts.
- **Conversations open at the latest message**: opening or switching a conversation, returning to the Decide tab, or coming back from the background lands at the latest message without animation. Streaming follows only when the reader was already at the bottom.
- **Reading upward is not interrupted**: scrolling up pauses following and reveals a 44px circular down-arrow button; tapping it scrolls back and resumes following. The old “new messages” bar and unread count are gone.
- **Failures are understandable and recoverable**: a failed send shows an icon, reason, and recovery action directly below that message while preserving its content and draft. When delivery is unknown, “Check status” comes first; “Retry” appears only after the message is confirmed undelivered, avoiding duplicates. 401 auth expiry and 429 rate limits get their own guidance and no blind retry. Interrupted assistant replies use a structured interruption card. User-facing copy never exposes error codes, and uncaught render errors fall back to a structured recovery screen.
- **Copy results are honest**: H5/APP use the native Clipboard API and mini programs keep the host clipboard; a failed copy is reported instead of claiming success. H5/APP no longer trigger Taro's internal “Content copied” toast; a mini-program host may still show its own system clipboard toast.
- **Touch targets and dialog accessibility**: the top notice now sits below the topbar and no longer blocks History/Locate/New-chat. Notice close, failed-send check/retry, put-back-in-box, starter pills, and Join a friend's group all meet a 44×44px minimum. The History sheet now has dialog/aria-modal semantics, focus entry and return, Tab containment, Escape close, and focus restoration.

### Platforms

- **Web H5**: <https://gogogo.plutokeating.beer/> (Pages production deployment `b9015b90`)
- **Android**: signed Universal and `arm64-v8a` APKs, `versionCode 6004`, 9,951,090 bytes, upgrade-safe. Both APK files are currently byte-identical because this release contains no native `.so` payload; this does not imply distinct ABI code.
  - Universal: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.4/GoGoGo-0.6.4-android-universal.apk>, SHA-256 `ee87d57281d2b7a08b49a3becbf036442edbfa84fa9725e49a46b46563c7e7d9`
  - arm64-v8a: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.4/GoGoGo-0.6.4-android-arm64-v8a.apk>, SHA-256 `ee87d57281d2b7a08b49a3becbf036442edbfa84fa9725e49a46b46563c7e7d9`
- **WeChat Mini Program**: `0.6.4` experience build uploaded (`2026-11-25T08:52:10Z`, artifact SHA-256 `87557f37…56ca8`; receipt at `docs/operations/wechat-mini-program/releases/2026-11-25-0.6.4.json`).
- **Douyin Mini Program**: `0.6.4` preview build uploaded (receipt at `docs/operations/douyin-mini-program/releases/2026-11-25-0.6.4.json`; preview link <https://t.zijieimg.com/i4JpAoU6/>; QR at `frontend/dist/tt-upload/qrcode-0.6.4.png`, no explicit platform expiry).
- **iOS**: no IPA because Apple distribution signing is not configured.

### Compatibility and migration

- No database migration, no API contract change, and no backend protocol or message-schema change; no new Worker deployment is required for this release.
- Account data, on-device private profiles, local conversations, and drafts keep their existing format; upgrading requires no cache clearing or re-login.
- H5, Android, WeChat, and Douyin share the same business code and `Plan` v2 itinerary contract.

### Verification and known limits

- H5: headless end-to-end and Node gates cover composer height/placeholder/composition, draft ownership, failure recovery/401/429 classification, top notices (including same-key success→error repaint), scroll following, the circular back-to-latest button, History dialog focus semantics, 44px touch targets, and structured failure rows at 320/390/1440; `h5-canonical` passed three consecutive runs.
- WeChat/Douyin: built against the production API; artifact gates assert `showConfirmBar=false`, `disableDefaultPadding=true`, `fixed=true`, `cursor=-1`, `confirmType="return"`, `adjustPosition=false`, `holdKeyboard=true`, keyboard-height bindings, and the absence of a keyboard-send path for the composer.
- Android: both signed 0.6.4 APKs pass certificate, permission, production-resource, and version gates; a headless Android 14 emulator completed 0.6.4 installation, first-run privacy screen, process survival, version 0.6.4, and zero fatal-log checks. The full `check:android-startup` timed out twice waiting for a live model itinerary card, so this release does **not** claim a complete 0.6.4 CDP itinerary acceptance; Task 6's complete startup gate passed on the same business code built as 0.6.3.
- **Verification for this iteration is headless only**: no desktop GUI, WeChat/Douyin devtools, or visible-browser manual acceptance was performed, and there is no real-device IME matrix. Headless Chromium visual recheck at 320/390/1440 returned PASS.
- Not yet covered; still requires real devices or later release verification:
  - WeChat/Douyin devtools and real-device English/Chinese IME input, fast typing, mid-string editing, and keyboard-not-covering-the-composer behavior;
  - WeChat iOS native Pinyin `onInput` suppression, SelectorQuery fallback, and candidate confirmation; WeChat Android third-party IME cursor jumps/stale text;
  - account email, verification code, and password entry on real devices with a real account;
  - Chinese IME composition and candidate confirmation on real iOS/Android keyboards;
  - iOS WeChat native Pinyin and iOS overlay/keyboard behavior;
  - mini-program `autoHeight` with `max-height`, `CustomWrapper` A/B, and Douyin `disableDefaultPadding` device differences;
  - mini-program `ScrollView` initial bottom, streaming follow, `scroll-into-view` repeatability, status-slot growth/shrink, and image/card height growth;
  - whether the send button receives a tap while the mini-program keyboard is open, and whether `--keyboard-inset` lifts with the host keyboard;
  - mini-program 320px empty composer runtime height and mini nav island + circular button geometry;
  - Android WebViews without reliable `visualViewport` events and real Chinese IME composition;
  - physical Android devices across OEM input methods;
  - the mini-program host's own clipboard system toast;
  - public `v0.6.4` Release and download-page verification: performed after publication through the unauthenticated latest API, anonymous asset downloads, and the live download page; the verification record is stored at `docs/operations/github-releases/2026-11-25-0.6.4.md` in the source repo.

### Release assets

- Source tag: `v0.6.4`; the exact source commit is recorded as `sourceCommit` in `release-manifest.json`.
- Public release repository tag: `v0.6.4`.
- `release-manifest.json` and `SHA256SUMS` are attached to this Release.
- Release: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/tag/v0.6.4>
