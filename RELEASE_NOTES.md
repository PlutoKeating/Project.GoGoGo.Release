# 走不走 v0.6.10 / GoGoGo v0.6.10

## 中文

### 本次更新

- **各页独立滚动**：「行程」和「我的」不再共用同一个滚动位置，切页时各自停在自己上次的位置，第一次进入从顶部开始。三个标签页的顶栏和底部标签栏都固定不动，滚到最上或最下时的回弹只作用在中间内容上，不再把顶栏和底栏一起拉动。
- **邀请朋友按钮固定在右上角**：对话里的行程页，“邀朋友群拍板”改为标题区右上角的圆形按钮，位置固定，不再放在底部那一排小按钮里。
- **底部按钮整行横滑**：屏幕较矮、“确认行程 · 去出发”和微调按钮在同一行时，整行一起左右滑动，在确认按钮上滑也能看到后面的按钮。

### 平台

- **Web H5**：<https://gogogo.plutokeating.beer/>
- **Android**：签名 Universal APK 与 `arm64-v8a` APK，`versionCode 6010`，10,004,528 bytes，可覆盖安装 0.6.9。两个 APK 当前字节完全相同，因为本版本没有 native `.so` 负载。
  - Universal：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.10/GoGoGo-0.6.10-android-universal.apk>，SHA-256 `52cf68bb362cbf42e67b480cf1858cea6a9feb2dc80a758106b74f4eb9893375`
  - arm64-v8a：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.10/GoGoGo-0.6.10-android-arm64-v8a.apk>，SHA-256 `52cf68bb362cbf42e67b480cf1858cea6a9feb2dc80a758106b74f4eb9893375`
- **微信小程序**：`0.6.10` 开发版本已上传（产物 SHA-256 `086e3591…`），依赖已开启的体验内测自动更新；尚未提交审核，不是面向公众的正式上线。
- **抖音小程序**：`0.6.10` 预览版已上传（产物 SHA-256 `6b702bf7…`，预览短链 <https://t.zijieimg.com/llcM_ALycmk/>，平台未返回到期时间）；尚未提交审核，不是面向公众的正式上线。
- **iOS**：仍缺少 Apple 分发签名配置，本版本没有 IPA。

### 兼容性与迁移

- 无数据库迁移，接口与后端代码相对 0.6.9 没有变化。
- 账户、本机私人档案、本地会话与草稿的存储格式保持不变；升级不需要清理缓存或重新登录。

### 验证范围与已知限制

- 前端类型检查与 13 项 H5 无头浏览器回归、本地优先、交互状态机、小程序输入框、请求错误检查通过。行程页检查新增：邀请按钮位于右上角且不挡标题；矮屏下在确认按钮上横滑可滚动整行；「我的」只在内容区滚动、窗口不可滚动、滚动后顶栏与底栏不动；切到「行程」从顶部开始、切回「我的」回到原位置。
- Android：双签名 APK 通过证书、签名形态、权限、正式资源与版本门禁；在无头 Android 14 模拟器上完成对 0.6.9 的覆盖安装（`versionCode 6010`、`versionName 0.6.10`），以及正式签名包的安装、调试端口关闭、前后台切换进程保持检查。**未执行**调试包的深度交互实测，因此不声称该项通过。
- **回弹手感无法在无头环境验证**；小程序里各页滚动位置的恢复没有在开发者工具或真机里实测。
- **本轮验证仅限无头环境**：没有真机或可见浏览器的人工验收。

### 发布资源

- 源码标签：`v0.6.10`；源码提交以 `release-manifest.json` 的 `sourceCommit` 为准。
- 公开发行仓库标签：`v0.6.10`。
- 发行清单 `release-manifest.json` 与 `SHA256SUMS` 作为本 Release 附件提供。
- 正式 Release：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/tag/v0.6.10>

---

## English

### What changed

- **Each tab scrolls on its own**: Trip and Me no longer share one scroll position; each keeps its own place when you switch, starting from the top the first time. On all three tabs the top bar and the tab bar stay still, and the stretch at the top or bottom of a page moves only the content, no longer dragging the bars with it.
- **The invite button is fixed at the top right**: on the chat itinerary page, “Invite friends to a group vote” is now a round button at the top right of the title area instead of one of the small buttons at the bottom.
- **The bottom row swipes as a whole**: on shorter screens, where “Save trip · Ready to go” and the follow-up buttons share a row, the whole row swipes sideways, so swiping over the confirm button reveals the buttons after it.

### Platforms

- **Web H5**: <https://gogogo.plutokeating.beer/>
- **Android**: signed Universal and `arm64-v8a` APKs, `versionCode 6010`, 10,004,528 bytes, installs over 0.6.9. Both files are currently byte-identical because this release has no native `.so` payload.
  - Universal: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.10/GoGoGo-0.6.10-android-universal.apk>, SHA-256 `52cf68bb362cbf42e67b480cf1858cea6a9feb2dc80a758106b74f4eb9893375`
  - arm64-v8a: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.10/GoGoGo-0.6.10-android-arm64-v8a.apk>, SHA-256 `52cf68bb362cbf42e67b480cf1858cea6a9feb2dc80a758106b74f4eb9893375`
- **WeChat Mini Program**: `0.6.10` development build uploaded (artifact SHA-256 `086e3591…`), delivered through the enabled internal-test auto update; not submitted for review, so not a public launch.
- **Douyin Mini Program**: `0.6.10` preview build uploaded (artifact SHA-256 `6b702bf7…`, preview link <https://t.zijieimg.com/llcM_ALycmk/>, no expiry returned by the platform); not submitted for review, so not a public launch.
- **iOS**: no IPA because Apple distribution signing is not configured.

### Compatibility and migration

- No database migration; the API and backend code are unchanged from 0.6.9.
- Account data, on-device private profiles, local conversations and drafts keep their format; upgrading needs no cache clearing or re-login.

### Verification and known limits

- Frontend type check, 13 headless H5 browser regressions and the local-first, interaction state machine, mini-program composer and request-error checks pass. The itinerary-page check now also covers: the invite button at the top right without covering the title; on a short screen, a sideways swipe over the confirm button scrolling the whole row; Me scrolling only inside its content area, the window not scrollable, and the bars staying still while scrolling; Trip starting at the top and Me returning to its position.
- Android: both signed APKs pass the certificate, signature-scheme, permission, production-resource and version gates; on a headless Android 14 emulator the build installed over 0.6.9 (`versionCode 6010`, `versionName 0.6.10`) and the signed release passed the install, debug-port-closed and background/foreground process checks. The deep interaction run of the debug build was **not** executed and is not claimed.
- **The feel of the overscroll stretch cannot be verified headlessly**; restoring each tab's position inside the mini programs was not exercised in devtools or on a device.
- **Verification is headless only**: no real-device or visible-browser manual acceptance.

### Release assets

- Source tag: `v0.6.10`; the exact source commit is recorded as `sourceCommit` in `release-manifest.json`.
- Public release repository tag: `v0.6.10`.
- `release-manifest.json` and `SHA256SUMS` are attached to this Release.
- Release: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/tag/v0.6.10>
