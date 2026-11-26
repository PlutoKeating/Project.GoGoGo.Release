# 走不走 v0.6.11 / GoGoGo v0.6.11

## 中文

### 本次更新

- **「行程」页按出行阶段重做**：页面不再把所有功能一次摆出来，而是看你处在哪一步——自己的草稿、等朋友入局、大家拍板、已经定案、出发路上——每一步只给一个主按钮：开始出发、生成路线、就这个／定案、全员出发／导航去集合点、继续导航；全部打卡后是“结束并评价”。
- **一页看完，不用上下翻**：有行程时「行程」页整页不滚动。最上面一行说明现在的情况（阶段、剩余时间、谁已赞成、还差几票），点一下看所有成员和他们的想法；下面是标题与「邀请」按钮、可展开的地图缩略条、一站一卡的站点卡片，最底部是操作栏。原来飘在屏幕中间、挡住内容的底部按钮条已修复。
- **拍板和投票合成一件事**：拍板期间局主和局友都可以直接在卡片上换一家、加站、调顺序；改动后大家需要重新表态。局友点「就这个」表示同意眼前这版，点「想换」写下想法，狗狗GO 会融合大家的想法重新排；局主可以随时「定案」，只有自己一个人时也可以。
- **按阶段出现的按钮**：拍板时每站的第一个按钮是「换一家」，出发后才变成「打卡已到」；「现场有变」只在出发后出现。加入日历、让狗狗GO微调、更换出发起点、重新排、结束行程等收进右下角的「···」。
- **别人改了行程会提示**：局友改动路线时，被改的站点卡会短暂高亮，并显示一行“谁改了什么”。
- **邀请按钮**：对话里行程页右上角的邀请按钮加上「邀请」二字，变成长圆形按钮。

### 平台

- **Web H5**：<https://gogogo.plutokeating.beer/>
- **Android**：签名 Universal APK 与 `arm64-v8a` APK，`versionCode 6011`，10,012,720 bytes，可覆盖安装 0.6.10。两个 APK 当前字节完全相同，因为本版本没有 native `.so` 负载。
  - Universal：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.11/GoGoGo-0.6.11-android-universal.apk>，SHA-256 `0183c1ccb07d4bf4df58625b732fc040d8246921c0a4471048d25acfe0f50eaa`
  - arm64-v8a：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.11/GoGoGo-0.6.11-android-arm64-v8a.apk>，SHA-256 `0183c1ccb07d4bf4df58625b732fc040d8246921c0a4471048d25acfe0f50eaa`
- **微信小程序**：`0.6.11` 开发版本已上传（产物 SHA-256 `06fb276c…`），依赖已开启的体验内测自动更新；尚未提交审核，不是面向公众的正式上线。
- **抖音小程序**：`0.6.11` 预览版已上传（产物 SHA-256 `4853fe34…`，预览短链 <https://t.zijieimg.com/i4JKHTC2/>，平台未返回到期时间）；尚未提交审核，不是面向公众的正式上线。
- **iOS**：仍缺少 Apple 分发签名配置，本版本没有 IPA。

### 兼容性与迁移

- 无数据库迁移，接口与后端代码相对 0.6.10 没有变化；局主一人定案使用已有的定案接口。
- 账户、本机私人档案、本地会话、行程与草稿的存储格式保持不变；升级不需要清理缓存或重新登录。

### 验证范围与已知限制

- 前端类型检查；新增阶段规则检查（个人草稿／出发中、拍板流程、局主一人定案、过半票数、被改动站点）；群拍板检查新增：拍板中的状态栏与局主「定案」、拍板时没有打卡按钮、页面不滚动、操作栏既不压住站点卡也不落到底部标签栏下、已定案局友的「导航去集合点」与成员面板。另有 8 项 H5 无头浏览器回归、本地优先与小程序输入框检查通过，并人工查看了 390×844 与 360×640 下各阶段的截图。
- Android：双签名 APK 通过证书、签名形态、权限、正式资源与版本门禁；在无头 Android 14 模拟器上完成对公开 0.6.10 的覆盖安装（`versionCode 6011`、`versionName 0.6.11`），以及正式签名包的安装、调试端口关闭、前后台切换进程保持检查。**未执行**调试包的深度交互实测，因此不声称该项通过。
- 小程序里整页高度、站点卡在剩余高度内的滑动、底部面板与安全区没有在开发者工具或真机里实测。
- 导航页抽屉里的群拍板卡片本次没有改动。
- **本轮验证仅限无头环境**：没有真机或可见浏览器的人工验收。

### 发布资源

- 源码标签：`v0.6.11`；源码提交以 `release-manifest.json` 的 `sourceCommit` 为准。
- 公开发行仓库标签：`v0.6.11`。
- 发行清单 `release-manifest.json` 与 `SHA256SUMS` 作为本 Release 附件提供。
- 正式 Release：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/tag/v0.6.11>

---

## English

### What changed

- **The Trip tab follows where your outing is**: instead of showing every feature at once, the page now depends on the step you are at — your own draft, waiting for friends to join, deciding together, decided, or on the way — and each step has one main button: Set off, Build the route, This one / Decide, Everyone go / Go to meetup, Resume navigation, and Finish and rate once every stop is visited.
- **One page, no scrolling**: with a trip, the Trip tab no longer scrolls. The top row says where things stand (step, time left, who approved, how many votes are still needed); tap it to see every member and their ideas. Below are the title with an Invite button, a map strip you can expand, one card per stop, and the action bar at the bottom. The bottom button bar that floated mid-screen and covered content is fixed.
- **Deciding and voting are one flow**: while deciding, the host and members can all swap a venue, add a stop or reorder directly on the cards; after a change everyone confirms again. Members tap This one to approve the version on screen, or Change it to write an idea that 狗狗GO blends into a new route; the host can Decide at any time, including alone.
- **Buttons that fit the step**: while deciding, each stop's first button is Swap; it becomes Check in only once you are on the way, and Plans changed appears only then too. Add to calendar, Ask 狗狗GO to adjust, Change starting point, Plan a new one and End trip moved into the ··· button.
- **Changes from others are pointed out**: when a member changes the route, the stops they touched glow briefly and one line says who changed what.
- **Invite button**: the invite button at the top right of the chat itinerary page now reads Invite next to its icon, as a pill.

### Platforms

- **Web H5**: <https://gogogo.plutokeating.beer/>
- **Android**: signed Universal and `arm64-v8a` APKs, `versionCode 6011`, 10,012,720 bytes, installs over 0.6.10. Both files are currently byte-identical because this release has no native `.so` payload.
  - Universal: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.11/GoGoGo-0.6.11-android-universal.apk>, SHA-256 `0183c1ccb07d4bf4df58625b732fc040d8246921c0a4471048d25acfe0f50eaa`
  - arm64-v8a: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.11/GoGoGo-0.6.11-android-arm64-v8a.apk>, SHA-256 `0183c1ccb07d4bf4df58625b732fc040d8246921c0a4471048d25acfe0f50eaa`
- **WeChat Mini Program**: `0.6.11` development build uploaded (artifact SHA-256 `06fb276c…`), delivered through the enabled internal-test auto update; not submitted for review, so not a public launch.
- **Douyin Mini Program**: `0.6.11` preview build uploaded (artifact SHA-256 `4853fe34…`, preview link <https://t.zijieimg.com/i4JKHTC2/>, no expiry returned by the platform); not submitted for review, so not a public launch.
- **iOS**: no IPA because Apple distribution signing is not configured.

### Compatibility and migration

- No database migration; the API and backend code are unchanged from 0.6.10. A host deciding alone uses the existing decide action.
- Account data, on-device private profiles, local conversations, trips and drafts keep their format; upgrading needs no cache clearing or re-login.

### Verification and known limits

- Frontend type check; a new check of the step rules (own draft / on the way, the deciding flow, a host deciding alone, the majority count, changed stops); the group check now also covers the deciding status row and the host's Decide, no check-in button while deciding, the page not scrolling, the action bar neither covering the stop cards nor sitting under the tab bar, and a member's Go to meetup and members sheet once decided. Eight more headless H5 browser regressions, the local-first and mini-program composer checks pass, and screenshots of each step at 390×844 and 360×640 were reviewed.
- Android: both signed APKs pass the certificate, signature-scheme, permission, production-resource and version gates; on a headless Android 14 emulator the build installed over the public 0.6.10 (`versionCode 6011`, `versionName 0.6.11`) and the signed release passed the install, debug-port-closed and background/foreground process checks. The deep interaction run of the debug build was **not** executed and is not claimed.
- Inside the mini programs, the full-page height, swiping the stop cards in the remaining height, and the bottom sheets with safe areas were not exercised in devtools or on a device.
- The group card inside the navigation drawer is unchanged in this release.
- **Verification is headless only**: no real-device or visible-browser manual acceptance.

### Release assets

- Source tag: `v0.6.11`; the exact source commit is recorded as `sourceCommit` in `release-manifest.json`.
- Public release repository tag: `v0.6.11`.
- `release-manifest.json` and `SHA256SUMS` are attached to this Release.
- Release: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/tag/v0.6.11>
