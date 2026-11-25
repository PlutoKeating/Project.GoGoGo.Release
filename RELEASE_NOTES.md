# 走不走 v0.6.8 / GoGoGo v0.6.8

## 中文

### 本次更新

- **一站一卡**：对话里的行程卡、行程页和导航抽屉不再是很长的列表。一个地点一张卡，上下滑动切换前后站点，左右滑动切换这一站的其他选择（平行方案和备选店排成一排），滑到哪家就换成哪家。
- **操作收在卡片上**：看评价、现场核验、上移、下移、移除、后面加一站、换交通方式都在每张卡的“更多”里；锁定按钮在卡片头部。行程页不再有「调整行程」开关。
- **行程卡更短**：路线图移到卡片堆叠的最后一张，底部的次要按钮合并为一行。
- **行程页加站更直接**：卡片堆叠的最后一张就是“顺路加一站”，可以搜索，也可以让狗狗GO 挑。
- **开场更干净**：开场卡删去“帮我随便安排一下”按钮，只留四张灵感卡。
- **空的行程页一屏显示**：不需要滚动。
- **顶栏**：左上角的小狗标志移除，定位按钮靠左；加入朋友群拍板的按钮换成“两个小人加加号”图标，新对话按钮换成“对话气泡加加号”图标。

### 平台

- **Web H5**：<https://gogogo.plutokeating.beer/>
- **Android**：签名 Universal APK 与 `arm64-v8a` APK，`versionCode 6008`，10,008,624 bytes，可覆盖安装 0.6.7。两个 APK 当前字节完全相同，因为本版本没有 native `.so` 负载。
  - Universal：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.8/GoGoGo-0.6.8-android-universal.apk>，SHA-256 `d3d959a1d566b3f28b0a36b853a35352bd669ba5789a5282e916f89d505e798f`
  - arm64-v8a：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.8/GoGoGo-0.6.8-android-arm64-v8a.apk>，SHA-256 `d3d959a1d566b3f28b0a36b853a35352bd669ba5789a5282e916f89d505e798f`
- **微信小程序**：`0.6.8` 开发版本已上传（产物 SHA-256 `4e5090ce…ba432`），依赖已开启的体验内测自动更新；尚未提交审核，不是面向公众的正式上线。
- **抖音小程序**：`0.6.8` 预览版已上传（产物 SHA-256 `3ec5ff6c…24fed`，预览短链 <https://t.zijieimg.com/i4JTBVA1/>，平台未返回到期时间）；尚未提交审核，不是面向公众的正式上线。
- **iOS**：仍缺少 Apple 分发签名配置，本版本没有 IPA。

### 兼容性与迁移

- 无数据库迁移，接口请求与响应格式不变，后端代码没有变化。
- 账户、本机私人档案、本地会话与草稿的存储格式保持不变；升级不需要清理缓存或重新登录。

### 验证范围与已知限制

- 前端类型检查，以及 H5 Canonical、对话体验、本地优先、交互状态机、群拍板、导航驾驶舱、声明式卡片、账户登录、选点器、请求错误、微信头部与资料页布局等无头回归通过。
- 新增的无头浏览器检查覆盖：手指左右滑动换店、上下滑动切站；程序或布局引起的滚动不会改动行程；翻动卡片不产生任何行程改动；卡片“更多”面板的开合与上移、移除；空的行程页在四种屏幕尺寸下没有可滚动区域。
- Android：双签名 APK 通过证书、签名形态、权限、正式资源与版本门禁；在无头 Android 14 模拟器上完成对 0.6.7 的覆盖安装（`versionCode 6008`、`versionName 0.6.8`），以及正式签名包的安装、调试端口关闭、前后台切换进程保持检查。**未执行**调试包的深度交互实测，因此不声称该项通过。
- **小程序里的滑动没有实测**：微信／抖音使用宿主的轮播组件实现卡片堆叠，本轮只验证了构建与产物门禁，没有在开发者工具或真机里滑动过。
- **本轮验证仅限无头环境**：没有真机或可见浏览器的人工验收。触摸滑动的手感、滑到首尾后交还页面滚动的表现、各宿主里的实际渲染仍需真机确认。
- “对话流终态”检查本轮未运行（本机所需端口被其他进程占用）。
- 在聊天里，行程卡滑到第一张或最后一张后继续滑才会滚动聊天。

### 发布资源

- 源码标签：`v0.6.8`；源码提交以 `release-manifest.json` 的 `sourceCommit` 为准。
- 公开发行仓库标签：`v0.6.8`。
- 发行清单 `release-manifest.json` 与 `SHA256SUMS` 作为本 Release 附件提供。
- 正式 Release：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/tag/v0.6.8>

---

## English

### What changed

- **One stop per card**: the itinerary card in chat, the Trip tab and the navigation drawer are no longer long lists. Each place is a card; swipe up or down for the previous or next stop, swipe sideways for the stop's other choices (parallel options and backups in one row). Landing on a place selects it.
- **Actions live on the card**: reviews, on-site reports, move up, move down, remove, add a stop after and change transit sit behind each card's “more” button; the lock button is in the card header. The Trip tab no longer has an edit-mode switch.
- **A shorter itinerary card**: the route map moved to the last card of the deck and the secondary buttons share one row.
- **Adding a stop is direct**: the last card of the Trip deck is “Add a stop”, by search or by asking 狗狗GO.
- **A cleaner welcome**: the “Just plan something for me” button is gone, leaving the four inspiration cards.
- **The empty Trip tab fits one screen** without scrolling.
- **Top bar**: the mascot at the top left is removed and the location pill sits at the left; the button for joining a friend's group vote is now “two people with a plus”, and the new-chat button is “a chat bubble with a plus”.

### Platforms

- **Web H5**: <https://gogogo.plutokeating.beer/>
- **Android**: signed Universal and `arm64-v8a` APKs, `versionCode 6008`, 10,008,624 bytes, installs over 0.6.7. Both files are currently byte-identical because this release has no native `.so` payload.
  - Universal: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.8/GoGoGo-0.6.8-android-universal.apk>, SHA-256 `d3d959a1d566b3f28b0a36b853a35352bd669ba5789a5282e916f89d505e798f`
  - arm64-v8a: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.8/GoGoGo-0.6.8-android-arm64-v8a.apk>, SHA-256 `d3d959a1d566b3f28b0a36b853a35352bd669ba5789a5282e916f89d505e798f`
- **WeChat Mini Program**: `0.6.8` development build uploaded (artifact SHA-256 `4e5090ce…ba432`), delivered through the enabled internal-test auto update; not submitted for review, so not a public launch.
- **Douyin Mini Program**: `0.6.8` preview build uploaded (artifact SHA-256 `3ec5ff6c…24fed`, preview link <https://t.zijieimg.com/i4JTBVA1/>, no expiry returned by the platform); not submitted for review, so not a public launch.
- **iOS**: no IPA because Apple distribution signing is not configured.

### Compatibility and migration

- No database migration; request and response formats are unchanged, and the backend code did not change.
- Account data, on-device private profiles, local conversations and drafts keep their format; upgrading needs no cache clearing or re-login.

### Verification and known limits

- Frontend type check and the headless regressions for H5 Canonical, the conversation experience, local-first storage, the interaction state machines, group outings, the navigation cockpit, declarative cards, account sign-in, the location picker, request errors and the WeChat header and profile layouts pass.
- New headless browser checks cover: finger swipes sideways to change the place and upwards to change the stop; a scroll caused by code or layout never changes the plan; browsing the deck changes nothing; the “more” panel opening and closing, move up and remove; the empty Trip tab having nothing scrollable at four screen sizes.
- Android: both signed APKs pass the certificate, signature-scheme, permission, production-resource and version gates; on a headless Android 14 emulator the build installed over 0.6.7 (`versionCode 6008`, `versionName 0.6.8`) and the signed release passed the install, debug-port-closed and background/foreground process checks. The deep interaction run of the debug build was **not** executed and is not claimed.
- **Swiping inside the mini programs was not exercised**: WeChat and Douyin build the deck from the host's swiper component; this round only verified the builds and artifact gates, not the gesture in devtools or on a device.
- **Verification is headless only**: no real-device or visible-browser manual acceptance. How the swipe feels, how the gesture hands back to page scrolling at either end, and the rendering in each host still need real devices.
- The conversation-stream terminal check was not run this round (the local port it needs was taken by another process).
- In chat, the itinerary card scrolls the conversation only after its first or last card is reached.

### Release assets

- Source tag: `v0.6.8`; the exact source commit is recorded as `sourceCommit` in `release-manifest.json`.
- Public release repository tag: `v0.6.8`.
- `release-manifest.json` and `SHA256SUMS` are attached to this Release.
- Release: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/tag/v0.6.8>
