# 走不走 v0.7.4 / GoGoGo v0.7.4

## 中文

### 本次更新

- **对话页不再被行程大卡片反复吸回**：狗狗GO 排出一张行程大卡片之后再发新消息，此前画面会在“新消息”和“上一张大卡片”之间每秒来回跳——停下时大卡片把画面吸回去，新消息又把画面拉到底部。现在只要你停在最新的消息处、而大卡片下面已经有新内容（你的新问题、等待中的工作区、简短回复），画面就停在最新消息，不再被吸回。手指滑到大卡片中间松手时，大卡片照常完整对齐；大卡片本身就是最新内容时也照常对齐。
- 包含 v0.7.3 的全部内容：带约束入局与提想法立即完成，路线在后台为全员调整并实时推送。

### 平台

- **Web H5**：<https://gogogo.plutokeating.beer/>
- **Android**：签名 Universal APK 与 `arm64-v8a` APK，`versionCode 7004`，10,090,651 bytes，可覆盖安装 0.7.3；已安装 0.6.13 及以上版本的用户可在「我的 → 应用版本与更新」里应用内升级。两个 APK 当前字节完全相同，因为本版本没有 native `.so` 负载。
  - Universal：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.7.4/GoGoGo-0.7.4-android-universal.apk>，SHA-256 `63e017622e1bfca5a0179154a2ba8803cbee9b9fd6a850e3b4e5e408d2507831`
  - arm64-v8a：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.7.4/GoGoGo-0.7.4-android-arm64-v8a.apk>，SHA-256 `63e017622e1bfca5a0179154a2ba8803cbee9b9fd6a850e3b4e5e408d2507831`
- **微信小程序**：`0.7.4` 开发版本已上传（产物 SHA-256 `da61ad9d…`），依赖已开启的体验内测自动更新；尚未提交审核，不是面向公众的正式上线。
- **抖音小程序**：`0.7.4` 预览版已上传（产物 SHA-256 `a3cfe8a4…`，预览短链 <https://t.zijieimg.com/i4erB469/>，平台未返回到期时间）；尚未提交审核，不是面向公众的正式上线。
- **iOS**：仍缺少 Apple 分发签名配置，本版本没有 IPA。

### 兼容性与迁移

- 仅前端滚动行为变化，接口与数据不变；没有数据库迁移，升级不需要清理缓存或重新登录。

### 验证范围与已知限制

- `check:itinerary-page` 新增场景：行程大卡片之后发送新消息，回复 5 秒后才到且只是一句短文本，9 秒内每 250 毫秒记录画面位置。修复前同一场景约每秒在最新消息与大卡片顶部之间往复；修复后两种手机尺寸下始终停在最新消息、从未被吸回。原有“滑到大卡片大部分可见时完整对齐、大部分不可见时移出”的检查仍通过；`check:progressive-itinerary`、`check:local-first-ui`、`check:interaction-ui`、`check:trip-end`、`check:group-outing` 通过。
- 小程序采用同样的规则（以触底事件判断是否在最新位置），已通过正式构建与产物检查，未在真机上验证滚动手感。
- Android：双签名 APK 通过证书、签名形态、权限、正式资源与版本门禁；在无头 Android 14 模拟器上覆盖安装公开 0.7.3，正式签名包通过安装、调试端口关闭、前后台切换进程保持检查。**未执行**调试包深度交互实测；小程序与 Android 真机验收尚未进行。

### 发布资源

- 源码标签：`v0.7.4`；源码提交以 `release-manifest.json` 的 `sourceCommit` 为准。
- 公开发行仓库标签：`v0.7.4`。
- 国内下载镜像：<https://gogogo.williamhvollita.dpdns.org/releases/download/v0.7.4/GoGoGo-0.7.4-android-universal.apk>

## English

### What's new

- **The conversation no longer snaps back to the itinerary card**: after 狗狗GO laid out a full-screen itinerary card, sending a new message used to make the view jump back and forth about once a second — the card pulled the view up when scrolling stopped, and the new message pulled it back down. Now, while you are at the newest messages and there is new content below the card (your new question, the waiting view, a short reply), the view stays with the newest messages. Letting go mid-card still aligns the card fully, and so does a card that is itself the newest content.
- Includes everything in v0.7.3: joining with needs and adding ideas finish at once, and the route is adjusted for everyone in the background and pushed live.

### Platforms

- **Web H5**: <https://gogogo.plutokeating.beer/>
- **Android**: signed universal and `arm64-v8a` APKs, `versionCode 7004`, 10,090,651 bytes, installs over 0.7.3; users on 0.6.13 or later can update in the app from "Me → App version & updates". The two APKs are byte-identical for now because this release has no native `.so` payload.
  - Universal: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.7.4/GoGoGo-0.7.4-android-universal.apk>, SHA-256 `63e017622e1bfca5a0179154a2ba8803cbee9b9fd6a850e3b4e5e408d2507831`
  - arm64-v8a: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.7.4/GoGoGo-0.7.4-android-arm64-v8a.apk>, SHA-256 `63e017622e1bfca5a0179154a2ba8803cbee9b9fd6a850e3b4e5e408d2507831`
- **WeChat Mini Program**: `0.7.4` development version uploaded (artifact SHA-256 `da61ad9d…`), relying on the enabled automatic experience-version update; not submitted for review and not a public launch.
- **Douyin Mini Program**: `0.7.4` preview uploaded (artifact SHA-256 `a3cfe8a4…`, preview link <https://t.zijieimg.com/i4erB469/>, no expiry returned by the platform); not submitted for review and not a public launch.
- **iOS**: Apple distribution signing is still missing; no IPA in this release.

### Compatibility and migration

- Only the frontend's scrolling changed; APIs and data are unchanged. No database migration, and no cache clearing or new sign-in is needed.

### Verification and known limitations

- `check:itinerary-page` gained a scenario: after an itinerary card, a new message is sent whose reply arrives 5 seconds later as a single short text, and the view position is sampled every 250 ms for 9 seconds. Before the fix the same scenario bounced between the newest messages and the top of the card about once a second; after it, the view stays with the newest messages at both phone sizes and is never pulled back. The existing checks that a mostly visible card aligns fully and a mostly hidden one leaves the view still pass, as do `check:progressive-itinerary`, `check:local-first-ui`, `check:interaction-ui`, `check:trip-end` and `check:group-outing`.
- Mini programs use the same rule (at the newest messages per the lower-edge event); they pass the production build and artifact checks, but the scrolling has not been tried on a physical device.
- Android: both signed APKs pass the certificate, signature scheme, permission, production-asset and version gates; on a headless Android 14 emulator the build installed over the public 0.7.3 and the signed release passed install, WebView-debug-port-closed and background/foreground checks. The debug-build deep interaction run was **not** executed; mini-program and Android physical-device acceptance has not been done yet.

### Release assets

- Source tag: `v0.7.4`; the source commit is `sourceCommit` in `release-manifest.json`.
- Public release repository tag: `v0.7.4`.
- Mirror download (faster in mainland China): <https://gogogo.williamhvollita.dpdns.org/releases/download/v0.7.4/GoGoGo-0.7.4-android-universal.apk>
