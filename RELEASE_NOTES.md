# 走不走 v0.6.14 / GoGoGo v0.6.14

## 中文

### 本次更新

- **下载与更新改走自有镜像，GitHub 作为备用**：官网下载页和 APP「我的 → 应用版本与更新」先从走不走自己的服务器（Cloudflare R2 存储）读取最新版本并下载安装包，只有它连不上时才去 GitHub。在中国大陆网络下，下载更快、更不容易中断；多人共用一个网络出口时（比如校园网），也不再碰到 GitHub 的访问次数限制。
- **官网下载页**：主按钮从自有镜像下载，按钮下方多了一个「备用：从 GitHub 下载」链接，以防镜像出问题。
- **APP 应用内更新**：从镜像下载失败时会自动改从 GitHub 下载，不用手动重试。下载完成后除了原有的包名、版本、签名和文件大小检查，还会核对镜像提供的 SHA-256 校验值。
- **小程序**：本版本只重新上传了体验版和预览版，功能和使用方式没有变化。

### 平台

- **Web H5**：<https://gogogo.plutokeating.beer/>
- **Android**：签名 Universal APK 与 `arm64-v8a` APK，`versionCode 6014`，10,082,459 bytes，可覆盖安装 0.6.13。两个 APK 当前字节完全相同，因为本版本没有 native `.so` 负载。
  - Universal（镜像）：<https://gogogo.williamhvollita.dpdns.org/releases/download/v0.6.14/GoGoGo-0.6.14-android-universal.apk>
  - Universal（GitHub）：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.14/GoGoGo-0.6.14-android-universal.apk>，SHA-256 `c8d7b76962c90ab53416980949107d38e6fddf43d12b7838eb868fcf612fd816`
  - arm64-v8a（GitHub）：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.14/GoGoGo-0.6.14-android-arm64-v8a.apk>，SHA-256 `c8d7b76962c90ab53416980949107d38e6fddf43d12b7838eb868fcf612fd816`
- **微信小程序**：`0.6.14` 开发版本已上传（产物 SHA-256 `d4f9c3f2…`），依赖已开启的体验内测自动更新；尚未提交审核，不是面向公众的正式上线。
- **抖音小程序**：`0.6.14` 预览版已上传（产物 SHA-256 `a01a4072…`，预览短链 <https://t.zijieimg.com/i4edBAk6/>，平台未返回到期时间）；尚未提交审核，不是面向公众的正式上线。
- **iOS**：仍缺少 Apple 分发签名配置，本版本没有 IPA。

### 兼容性与迁移

- 新增两个无需登录的公开接口：`GET /api/releases/latest`（最新正式版本信息，格式与 GitHub 的 `releases/latest` 相同）和 `GET /releases/download/<tag>/<file>`（安装包下载，支持断点续传）。镜像只保留最新版本，旧版本链接返回 404，旧版本请到 GitHub 下载。没有数据库迁移。
- **从镜像更新从 0.6.14 起生效**：0.6.13 只认 GitHub 地址，所以从 0.6.13 升到 0.6.14 这一次仍从 GitHub 下载；之后的版本会优先走镜像。
- 账户、本机私人档案、会话与行程的存储格式不变；升级不需要清理缓存或重新登录。

### 验证范围与已知限制

- 后端 61 个测试文件 / 373 项用例通过，新增覆盖：镜像接口返回内容、断点续传、拒绝非安装包文件名和已删除的旧版本，以及 APP 的「镜像优先、镜像故障改用 GitHub、拒绝指向外部地址的镜像链接」。
- 官网下载页浏览器检查新增「镜像正常」与「镜像故障」两种情况：镜像正常时主按钮指向镜像，并显示 GitHub 备用链接；镜像故障时只显示 GitHub 下载。
- 线上镜像（当时为 0.6.13）实测：版本信息正确，完整下载的 SHA-256 与 GitHub 一致，断点续传返回 206，旧版本返回 404，官网跨域访问正常。
- Android：双签名 APK 通过证书、签名形态、权限、正式资源与版本门禁；在无头 Android 14 模拟器上覆盖安装从镜像下载的公开 0.6.13，正式签名包通过安装、调试端口关闭、前后台切换进程保持检查。**未执行**调试包的深度交互实测。
- Cloudflare 免费版在中国大陆没有机房，晚高峰仍可能绕道香港或更远的节点，镜像只能减少对 GitHub 的依赖，不能保证一定更快。
- 真机上的应用内更新与小程序真机验收尚未进行。

### 发布资源

- 源码标签：`v0.6.14`；源码提交以 `release-manifest.json` 的 `sourceCommit` 为准。
- 公开发行仓库标签：`v0.6.14`。
- 发行清单 `release-manifest.json` 与 `SHA256SUMS` 作为本 Release 附件提供。
- 正式 Release：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/tag/v0.6.14>

---

## English

### What changed

- **Downloads and updates come from our own mirror, with GitHub as backup**: the download page and "Me → App version & updates" in the app now read the latest release and download installers from GoGoGo's own server (Cloudflare R2 storage) first, and only go to GitHub when it cannot be reached. On networks in mainland China, downloads are faster and less likely to break, and many people sharing one network exit (such as a campus network) no longer run into GitHub's request limit.
- **Download page**: the main button downloads from the mirror, and a "Backup: download from GitHub" link sits below it in case the mirror has a problem.
- **In-app updates**: if the download from the mirror fails, the app automatically switches to GitHub without you having to retry. After downloading, the app also checks the SHA-256 published by the mirror, on top of the existing package, version, signature and file size checks.
- **Mini programs**: only new beta and preview builds were uploaded; features and usage are unchanged.

### Platforms

- **Web H5**: <https://gogogo.plutokeating.beer/>
- **Android**: signed Universal and `arm64-v8a` APKs, `versionCode 6014`, 10,082,459 bytes, installs over 0.6.13. Both APKs are currently byte-identical because this release has no native `.so` payload.
  - Universal (mirror): <https://gogogo.williamhvollita.dpdns.org/releases/download/v0.6.14/GoGoGo-0.6.14-android-universal.apk>
  - Universal (GitHub): <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.14/GoGoGo-0.6.14-android-universal.apk>, SHA-256 `c8d7b76962c90ab53416980949107d38e6fddf43d12b7838eb868fcf612fd816`
  - arm64-v8a (GitHub): <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.14/GoGoGo-0.6.14-android-arm64-v8a.apk>, SHA-256 `c8d7b76962c90ab53416980949107d38e6fddf43d12b7838eb868fcf612fd816`
- **WeChat mini program**: development version `0.6.14` uploaded (artifact SHA-256 `d4f9c3f2…`) and delivered through the enabled experience auto-update; not submitted for review and not a public release.
- **Douyin mini program**: preview `0.6.14` uploaded (artifact SHA-256 `a01a4072…`, preview link <https://t.zijieimg.com/i4edBAk6/>, no expiry returned by the platform); not submitted for review and not a public release.
- **iOS**: Apple distribution signing is still not configured; no IPA in this release.

### Compatibility and migration

- Two new public endpoints that need no sign-in: `GET /api/releases/latest` (the latest official release, in the same shape as GitHub's `releases/latest`) and `GET /releases/download/<tag>/<file>` (installer downloads with resume support). The mirror keeps only the newest version; links to older versions return 404, so get older versions from GitHub. No database migration.
- **Mirror updates start with 0.6.14**: 0.6.13 only accepts GitHub addresses, so updating from 0.6.13 to 0.6.14 still downloads from GitHub; later versions prefer the mirror.
- Storage formats for accounts, the on-device private profile, conversations and trips are unchanged; no cache clearing or re-sign-in is needed.

### Verification and known limits

- Backend: 61 test files / 373 cases pass. New coverage: the mirror endpoint's response, resumed downloads, refusing non-installer file names and removed old versions, and the app's mirror-first order, switching to GitHub when the mirror fails, and ignoring mirror links that point elsewhere.
- The download page browser check now covers a working mirror and a mirror outage: with the mirror up, the main button points to the mirror with a GitHub backup link; with it down, only GitHub downloads are shown.
- Live mirror check (then serving 0.6.13): correct release data, a full download whose SHA-256 matches GitHub, resume answered with 206, old versions answered with 404, and cross-origin access from the website working.
- Android: both signed APKs pass the certificate, signature-scheme, permission, production-resource and version gates. On a headless Android 14 emulator the build installed over the public 0.6.13 (downloaded from the mirror), and the signed release passed install, WebView-debug-port-closed and background/foreground process checks. The debug-build deep interaction run was **not** executed.
- Cloudflare's free plan has no data centers in mainland China, so at peak hours traffic may still route through Hong Kong or farther away. The mirror reduces the dependence on GitHub but cannot guarantee faster downloads.
- In-app updating on a physical phone and mini-program device acceptance have not been performed.

### Release assets

- Source tag: `v0.6.14`; the source commit is the `sourceCommit` in `release-manifest.json`.
- Public release repository tag: `v0.6.14`.
- `release-manifest.json` and `SHA256SUMS` are attached to this release.
- Release: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/tag/v0.6.14>
