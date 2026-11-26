# 走不走 v0.6.9 / GoGoGo v0.6.9

## 中文

### 本次更新

- **行程是一整页**：对话里的行程不再是一张卡片，而是正好铺满顶栏与输入框之间的整个区域。在里面上下滑切换站点，滑过第一站或最后一站回到对话滚动。滚动停下时不会停在半页：露出过半就整页滚入，否则整页滚出。
- **有行程的回复只有行程**：狗狗GO 写出或更新行程后不再附带一段总结文字，行程本身就是回答；以前保存的对话里，行程旁的文字也不再显示。
- **生成途中插的话排在中间**：狗狗GO 还在排行程时你补充一句，这句话会排在已经完成的步骤下面，新的步骤和最新的行程出现在它下面，行程始终在最新位置，刷新后顺序不变。
- **去掉没人读的提示**：行程旁的绿色“已将 A 替换为 B”、黄色警告块、“正在生长／核验路网”状态条和夜间出行提示行全部删除；插话后输入框上方的说明条删除；顶部不再弹出“已保存”“已定位”“已打卡”“已加入”之类的成功确认，也不再提示“已保存在本机，联网后自动同步”。顶部提醒只用于错误，以及点了之后界面上没有其他变化的说明（如复制成功）。
- **小屏更紧凑**：屏幕较矮时，行程页的标题收为一行，确认按钮与微调按钮并为一行，出发地改由顶栏定位按钮修改。

### 平台

- **Web H5**：<https://gogogo.plutokeating.beer/>
- **Android**：签名 Universal APK 与 `arm64-v8a` APK，`versionCode 6009`，10,004,528 bytes，可覆盖安装 0.6.8。两个 APK 当前字节完全相同，因为本版本没有 native `.so` 负载。
  - Universal：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.9/GoGoGo-0.6.9-android-universal.apk>，SHA-256 `e266d80578e6b24650bfa809f8c036505628a21037e952ecf6f6cfa19feb4340`
  - arm64-v8a：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.9/GoGoGo-0.6.9-android-arm64-v8a.apk>，SHA-256 `e266d80578e6b24650bfa809f8c036505628a21037e952ecf6f6cfa19feb4340`
- **微信小程序**：`0.6.9` 开发版本已上传（产物 SHA-256 `2ef544c2…14da0`），依赖已开启的体验内测自动更新；尚未提交审核，不是面向公众的正式上线。
- **抖音小程序**：`0.6.9` 预览版已上传（产物 SHA-256 `2ba3eff3…a0629`，预览短链 <https://t.zijieimg.com/i4Jw2cP5/>，平台未返回到期时间）；尚未提交审核，不是面向公众的正式上线。
- **iOS**：仍缺少 Apple 分发签名配置，本版本没有 IPA。

### 兼容性与迁移

- 无数据库迁移。对话流新增 `assistant-split` 事件（插话时切分回复），其余请求与响应格式不变；后端已随本版本部署。
- 旧版本客户端遇到插话时会丢失本轮之后的增量，刷新会话即可看到完整内容；建议升级。新客户端连接旧后端时，插话在本轮结束后回到原来的排序。
- 账户、本机私人档案、本地会话与草稿的存储格式保持不变；升级不需要清理缓存或重新登录。

### 验证范围与已知限制

- 后端类型检查与 58 个测试文件、352 个用例通过，新增插话切分与“有行程不写文字”的测试。
- 前端类型检查与 H5 Canonical、对话体验、对话界面、本地优先、交互状态机、画布同步、声明式卡片、群拍板、导航驾驶舱、账户登录、对话流终态、对话卡片、选点器、请求错误、小程序输入框等无头回归通过。新增的行程页检查在 390×844 与 360×640 下覆盖：步骤 → 插话 → 行程的顺序、行程旁无文字与提示框、页高等于对话区域、滚动停下后整页滚入或滚出、当前站点的照片、店名与按钮完整可见。
- Android：双签名 APK 通过证书、签名形态、权限、正式资源与版本门禁；在无头 Android 14 模拟器上完成对 0.6.8 的覆盖安装（`versionCode 6009`、`versionName 0.6.9`），以及正式签名包的安装、调试端口关闭、前后台切换进程保持检查。**未执行**调试包的深度交互实测，因此不声称该项通过。
- **小程序里的整页与滚动停靠没有实测**：微信／抖音用宿主的滚动视图测量高度并校正位置，本轮只验证了构建与产物门禁，没有在开发者工具或真机里滚动过。
- **本轮验证仅限无头环境**：没有真机或可见浏览器的人工验收。
- 插话后行程立即移到最新位置并铺满屏幕，所以视图停在新行程上，你的那句话在它上面，需要上滑查看。

### 发布资源

- 源码标签：`v0.6.9`；源码提交以 `release-manifest.json` 的 `sourceCommit` 为准。
- 公开发行仓库标签：`v0.6.9`。
- 发行清单 `release-manifest.json` 与 `SHA256SUMS` 作为本 Release 附件提供。
- 正式 Release：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/tag/v0.6.9>

---

## English

### What changed

- **The itinerary is a page**: in chat the itinerary is no longer a card; it fills exactly the area between the top bar and the message box. Swipe up or down inside it to move between stops; past the first or last stop the conversation scrolls. Scrolling never rests on half a page: when more than half is showing the page slides fully in, otherwise fully out.
- **A reply with an itinerary is just the itinerary**: once 狗狗GO writes or updates a plan it no longer adds a closing paragraph; the plan is the answer. Text next to itineraries in earlier conversations is hidden too.
- **Messages sent mid-reply land in place**: if you add something while 狗狗GO is still planning, your message sits below the steps already taken, the new steps and the latest itinerary appear under it, and the itinerary always stays at the newest position, also after a refresh.
- **Notices nobody reads are gone**: the green “replaced A with B” note, yellow warning block, “growing the plan / checking routes” status pills and late-night travel lines next to itineraries are removed, as is the strip above the message box after a mid-reply message. The top no longer shows success confirmations such as “Saved”, “Located”, “Checked in” or “Joined”, nor “Saved on this device, will sync when online”. Top notices are now only for errors and for taps that otherwise show no change (such as a copy).
- **Tighter on short screens**: on shorter screens the plan title takes one line, the confirm button and follow-up chips share a row, and the starting point is changed from the location button in the top bar.

### Platforms

- **Web H5**: <https://gogogo.plutokeating.beer/>
- **Android**: signed Universal and `arm64-v8a` APKs, `versionCode 6009`, 10,004,528 bytes, installs over 0.6.8. Both files are currently byte-identical because this release has no native `.so` payload.
  - Universal: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.9/GoGoGo-0.6.9-android-universal.apk>, SHA-256 `e266d80578e6b24650bfa809f8c036505628a21037e952ecf6f6cfa19feb4340`
  - arm64-v8a: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.9/GoGoGo-0.6.9-android-arm64-v8a.apk>, SHA-256 `e266d80578e6b24650bfa809f8c036505628a21037e952ecf6f6cfa19feb4340`
- **WeChat Mini Program**: `0.6.9` development build uploaded (artifact SHA-256 `2ef544c2…14da0`), delivered through the enabled internal-test auto update; not submitted for review, so not a public launch.
- **Douyin Mini Program**: `0.6.9` preview build uploaded (artifact SHA-256 `2ba3eff3…a0629`, preview link <https://t.zijieimg.com/i4Jw2cP5/>, no expiry returned by the platform); not submitted for review, so not a public launch.
- **iOS**: no IPA because Apple distribution signing is not configured.

### Compatibility and migration

- No database migration. The conversation stream gains an `assistant-split` event (a reply split around a mid-reply message); all other request and response formats are unchanged. The backend is deployed with this release.
- Older clients lose the rest of a reply's live updates after a mid-reply message; reopening the conversation shows everything. Upgrading is recommended. A new client talking to an older backend puts the message back in its old position when the reply ends.
- Account data, on-device private profiles, local conversations and drafts keep their format; upgrading needs no cache clearing or re-login.

### Verification and known limits

- Backend type check and 58 test files / 352 tests pass, including new tests for the reply split and for itinerary replies carrying no text.
- Frontend type check and the headless regressions for H5 Canonical, the conversation experience and interface, local-first storage, the interaction state machines, canvas sync, declarative cards, group outings, the navigation cockpit, account sign-in, the conversation-stream terminal state, conversation cards, the location picker, request errors and the mini-program composer pass. The new itinerary-page check covers, at 390×844 and 360×640: the steps → message → itinerary order, no text or notice boxes next to the itinerary, page height equal to the chat area, scrolling settling the page fully in or out, and the current stop's photo, name and buttons fully visible.
- Android: both signed APKs pass the certificate, signature-scheme, permission, production-resource and version gates; on a headless Android 14 emulator the build installed over 0.6.8 (`versionCode 6009`, `versionName 0.6.9`) and the signed release passed the install, debug-port-closed and background/foreground process checks. The deep interaction run of the debug build was **not** executed and is not claimed.
- **The full-height page and scroll settling inside the mini programs were not exercised**: WeChat and Douyin measure the height and correct the position through the host's scroll view; this round verified only the builds and artifact gates, not scrolling in devtools or on a device.
- **Verification is headless only**: no real-device or visible-browser manual acceptance.
- After a mid-reply message the itinerary moves to the newest position and fills the screen, so the view rests on the new plan and your message sits above it; scroll up to see it.

### Release assets

- Source tag: `v0.6.9`; the exact source commit is recorded as `sourceCommit` in `release-manifest.json`.
- Public release repository tag: `v0.6.9`.
- `release-manifest.json` and `SHA256SUMS` are attached to this Release.
- Release: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/tag/v0.6.9>
