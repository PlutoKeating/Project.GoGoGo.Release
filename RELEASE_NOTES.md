# 走不走 v0.6.7 / GoGoGo v0.6.7

## 中文

本版本包含 0.6.6（界面减负）与 0.6.7（一张图邀请）两轮改动；0.6.6 只上传过小程序预览版，没有单独发行。

### 本次更新

- **邀请朋友只要一张图**：发起群拍板后直接得到一张邀请图，图上只有 logo、一句“扫码加入，一起出发”和二维码。点“发给朋友”或“保存图片”即可，不再有口令、邀请码或需要复制的链接。
- **扫码就能加入**：用相机或浏览器扫邀请图即可打开入局页面；安卓手机已安装 APP 时会直接进入 APP。
- **在 APP 里选图加入**：点右上角的加号，直接从相册选朋友发来的邀请图，即可进入入局页面。小程序里加号会打开扫一扫，可以拍也可以从相册选。
- **入局只需点一下**：入局页面显示谁邀请你、去哪几站、已有几人加入，称呼已经填好，点“赞成并加入”即可。忌口、预算和想法收在一行里，需要时再展开。
- **开场一屏显示**：首页开场卡删去了说明文字、出发地与忌口标签和卡片说明行，不需要滑动。
- **入口归位**：加入朋友的群拍板改为右上角的加号；语言切换从右上角移到「我的」页。
- **行程页与「我的」页更干净**：删去页面副标题、说明文案与输入框占位文字；搜索框与搜索按钮并到一行；「我的」页忌口下方的说明卡删除。
- **修复**：行程空状态里“直接和狗狗GO 聊聊”按钮的文字在浅色底上看不见。

### 平台

- **Web H5**：<https://gogogo.plutokeating.beer/>
- **Android**：签名 Universal APK 与 `arm64-v8a` APK，`versionCode 6007`，10,000,328 bytes，可覆盖安装 0.6.5。两个 APK 当前字节完全相同，因为本版本没有 native `.so` 负载。
  - Universal：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.7/GoGoGo-0.6.7-android-universal.apk>，SHA-256 `f23a5f147b1578a6e66a8c4038119287e19a8c88bca200783b86a9086920cee5`
  - arm64-v8a：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.7/GoGoGo-0.6.7-android-arm64-v8a.apk>，SHA-256 `f23a5f147b1578a6e66a8c4038119287e19a8c88bca200783b86a9086920cee5`
- **微信小程序**：`0.6.7` 开发版本已上传（产物 SHA-256 `0d916995…84e4e`），依赖已开启的体验内测自动更新；尚未提交审核，不是面向公众的正式上线。
- **抖音小程序**：`0.6.7` 预览版已上传（产物 SHA-256 `54591211…4f768`，预览短链 <https://t.zijieimg.com/i4J37w8o/>，平台未返回到期时间）；尚未提交审核，不是面向公众的正式上线。
- **iOS**：仍缺少 Apple 分发签名配置，本版本没有 IPA。

### 兼容性与迁移

- 无数据库迁移，接口请求与响应格式不变，后端代码没有变化。
- 旧版本生成的邀请链接仍然有效；本版本不再提供输入口令的入口，持有旧口令的朋友需要让组局的人重新发一张邀请图。
- 账户、本机私人档案、本地会话与草稿的存储格式保持不变；升级不需要清理缓存或重新登录。

### 验证范围与已知限制

- 前端类型检查，以及群拍板、对话体验、H5 Canonical、交互状态机、导航驾驶舱、本地优先、声明式卡片、账户登录、选点器、请求错误等无头回归通过。
- 新增的无头浏览器检查覆盖：邀请图为 720×960 且面板内没有输入框和复制类文案；把生成的邀请图通过加号选图读回并完成入局；选到没有二维码的图片只提示、不打开面板；开场页在四种屏幕尺寸下不需要滚动。
- Android：双签名 APK 通过证书、签名形态、权限、正式资源与版本门禁；在无头 Android 14 模拟器上完成正式签名包的安装、调试端口关闭、前后台切换进程保持检查；系统对域名的 App Links 校验状态为已验证，以系统浏览意图打开邀请网址直接进入 APP。**未执行**调试包的深度交互实测，因此不声称该项通过。
- **微信／抖音扫码直接进入小程序尚未生效**：需要先在各自平台后台为小程序配置“扫普通链接二维码打开小程序”。在此之前，微信内扫码会打开网页版，同样可以入局。
- **本轮验证仅限无头环境**：没有真机、微信／抖音开发者工具或可见浏览器的人工验收。小程序里的邀请图绘制、图片转发与扫一扫，APP 里的系统选图器与系统分享，以及各品牌手机相机扫码后的落点，仍需真机确认。
- 浏览器不支持分享文件时只提供“保存图片”；抖音小程序没有图片转发接口，同样只提供“保存图片”。

### 发布资源

- 源码标签：`v0.6.7`；源码提交以 `release-manifest.json` 的 `sourceCommit` 为准。
- 公开发行仓库标签：`v0.6.7`。
- 发行清单 `release-manifest.json` 与 `SHA256SUMS` 作为本 Release 附件提供。
- 正式 Release：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/tag/v0.6.7>

---

## English

This release carries two rounds of work: 0.6.6 (a leaner interface) and 0.6.7 (the one-picture invite). 0.6.6 was only uploaded as mini-program previews and was not released on its own.

### What changed

- **Inviting friends takes one picture**: opening a group vote hands you an invite picture with only the logo, one line (“Scan to join the outing”) and a QR code. Tap “Send to friends” or “Save picture”. There are no codes or links to copy any more.
- **Scan to join**: scanning the picture with a camera or a browser opens the join page; on an Android phone with the app installed it opens the app directly.
- **Join from a picture inside the app**: tap the plus button at the top right and pick the invite picture a friend sent. In the mini programs the plus button opens the scanner, which can also read a picture from the album.
- **Joining is one tap**: the join page shows who invited you, the stops and how many have joined; a name is already filled in, and “Approve & join” does the rest. Diet, budget and ideas sit in one row you can open when needed.
- **A one-screen welcome**: the home card lost its helper text, the location and diet tags and the card captions, and no longer needs scrolling.
- **Entries moved to where they belong**: joining a friend's group vote is the plus button at the top right; the language switch moved from the top bar to the Me tab.
- **Cleaner Trip and Me tabs**: page subtitles, helper text and input placeholders are gone; the search field and its button share one row; the note card under dietary needs on the Me tab is removed.
- **Fix**: the “Chat with 狗狗GO” button in the empty Trip tab had text that was invisible on its light background.

### Platforms

- **Web H5**: <https://gogogo.plutokeating.beer/>
- **Android**: signed Universal and `arm64-v8a` APKs, `versionCode 6007`, 10,000,328 bytes, installs over 0.6.5. Both files are currently byte-identical because this release has no native `.so` payload.
  - Universal: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.7/GoGoGo-0.6.7-android-universal.apk>, SHA-256 `f23a5f147b1578a6e66a8c4038119287e19a8c88bca200783b86a9086920cee5`
  - arm64-v8a: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.7/GoGoGo-0.6.7-android-arm64-v8a.apk>, SHA-256 `f23a5f147b1578a6e66a8c4038119287e19a8c88bca200783b86a9086920cee5`
- **WeChat Mini Program**: `0.6.7` development build uploaded (artifact SHA-256 `0d916995…84e4e`), delivered through the enabled internal-test auto update; not submitted for review, so not a public launch.
- **Douyin Mini Program**: `0.6.7` preview build uploaded (artifact SHA-256 `54591211…4f768`, preview link <https://t.zijieimg.com/i4J37w8o/>, no expiry returned by the platform); not submitted for review, so not a public launch.
- **iOS**: no IPA because Apple distribution signing is not configured.

### Compatibility and migration

- No database migration; request and response formats are unchanged, and the backend code did not change.
- Invite links made by earlier versions still work. This version no longer has a place to type an invite code, so a friend holding an old code needs a fresh invite picture from the organiser.
- Account data, on-device private profiles, local conversations and drafts keep their format; upgrading needs no cache clearing or re-login.

### Verification and known limits

- Frontend type check and the headless regressions for group outings, the conversation experience, H5 Canonical, the interaction state machines, the navigation cockpit, local-first storage, declarative cards, account sign-in, the location picker and request errors pass.
- New headless browser checks cover: the invite picture is 720×960 and its sheet has no input field or copy action; the generated picture is read back through the plus button and the join completes; a picture without a QR code shows a notice and opens nothing; the welcome page needs no scrolling at four screen sizes.
- Android: both signed APKs pass the certificate, signature-scheme, permission, production-resource and version gates; on a headless Android 14 emulator the signed release passed the install, debug-port-closed and background/foreground process checks; the system reports the domain's App Links as verified, and opening an invite address with a system browse intent lands in the app. The deep interaction run of the debug build was **not** executed and is not claimed.
- **Scanning straight into the WeChat or Douyin mini program is not active yet**: each platform console first needs the “open the mini program from an ordinary link QR code” rule for the mini program. Until then, scanning inside WeChat opens the web version, where joining works the same way.
- **Verification is headless only**: no real-device, WeChat/Douyin devtools or visible-browser manual acceptance. Drawing the picture, forwarding it and scanning inside the mini programs, the system picture picker and share sheet inside the app, and where each phone brand's camera lands after a scan still need real devices.
- A browser that cannot share files offers “Save picture” only; the Douyin mini program has no picture-forwarding interface and likewise offers “Save picture” only.

### Release assets

- Source tag: `v0.6.7`; the exact source commit is recorded as `sourceCommit` in `release-manifest.json`.
- Public release repository tag: `v0.6.7`.
- `release-manifest.json` and `SHA256SUMS` are attached to this Release.
- Release: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/tag/v0.6.7>
