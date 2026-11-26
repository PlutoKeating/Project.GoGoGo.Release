# 走不走 v0.6.13 / GoGoGo v0.6.13

## 中文

### 本次更新

- **登录、注册不用离开应用**：网页和 Android APP 的登录弹窗里直接输入邮箱，点「获取邮箱验证码」，输入验证码后点「登录 / 注册」即可。还没有账号的邮箱会当场自动注册，弹窗会提示「这是新邮箱」。也可以切到「密码登录」；忘记密码直接用验证码登录。以游客身份聊过的对话会自动并入账号。通行密钥和 GitHub 登录保留在弹窗底部，这两种仍会打开账号服务页面。
- **Android 应用内更新**：「我的 → 应用版本与更新」发现新版本后，点「下载并安装」会在应用内下载并显示进度（可取消）。下载完成后，应用会核对安装包是否为本应用、版本是否更高、签名是否一致、文件是否完整，全部通过才打开系统安装界面。第一次使用时，安卓会要求在设置里允许本应用「安装未知应用」，允许后回到应用会自动继续。只有下载失败时才提供「改用浏览器下载」。
- **小程序**：微信、抖音仍是平台一键登录，行为不变。

### 平台

- **Web H5**：<https://gogogo.plutokeating.beer/>
- **Android**：签名 Universal APK 与 `arm64-v8a` APK，`versionCode 6013`，10,082,459 bytes，可覆盖安装 0.6.12。两个 APK 当前字节完全相同，因为本版本没有 native `.so` 负载。
  - Universal：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.13/GoGoGo-0.6.13-android-universal.apk>，SHA-256 `0b873abe93f53b4e050bfa0e95d97c3adf503cc549f70bf203d287358f7dfe4c`
  - arm64-v8a：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.13/GoGoGo-0.6.13-android-arm64-v8a.apk>，SHA-256 `0b873abe93f53b4e050bfa0e95d97c3adf503cc549f70bf203d287358f7dfe4c`
- **微信小程序**：`0.6.13` 开发版本已上传（产物 SHA-256 `f5e48c8d…`），依赖已开启的体验内测自动更新；尚未提交审核，不是面向公众的正式上线。
- **抖音小程序**：`0.6.13` 预览版已上传（产物 SHA-256 `215fb193…`，预览短链 <https://t.zijieimg.com/i4e1S3Un/>，平台未返回到期时间）；尚未提交审核，不是面向公众的正式上线。
- **iOS**：仍缺少 Apple 分发签名配置，本版本没有 IPA。

### 兼容性与迁移

- 新增接口 `POST /api/auth/direct/code/start`、`/api/auth/direct/code/verify`、`/api/auth/direct/password`；原有的跳转登录（`/api/auth/oidc/*`）与小程序登录不变。没有数据库迁移。
- APP 新增 `REQUEST_INSTALL_PACKAGES` 权限，只用于把校验过的本应用更新包交给系统安装器。
- **应用内更新从 0.6.13 起生效**：仍在 0.6.12 或更早版本的用户，需要再从下载页或浏览器手动安装一次 0.6.13，之后的版本就能在应用内更新。
- 账户、本机私人档案、会话与行程的存储格式不变；升级不需要清理缓存或重新登录。

### 验证范围与已知限制

- 后端 59 个测试文件 / 366 项用例通过，新增覆盖：新邮箱验证码注册并带入游客数据、注册后注销账号服务的临时会话、密码错误提示、邮箱绑定凭据不能用于登录、未同意协议不发送验证码。
- 浏览器检查（本地构建与线上正式站点各跑一次）：密码错误就地提示、新邮箱验证码注册、游客会话随登录带入、全程不离开当前页面，以及通行密钥／GitHub 备选的跳转回传。线上用不存在的账号验证了「后端 → 账号服务」链路会正确拒绝错误密码。
- Android：双签名 APK 通过证书、签名形态、权限（含新增安装权限）、正式资源与版本门禁；在无头 Android 14 模拟器上覆盖安装公开 0.6.12，正式签名包通过安装、调试端口关闭、前后台切换进程保持检查。**未执行**调试包的深度交互实测。
- 从 GitHub 下载安装包在中国大陆网络下可能较慢；下载失败时可改用浏览器。
- 真实邮箱收验证码、真机上的应用内更新与小程序真机验收尚未进行。
- 手机号短信登录、APP 与网页内的微信登录需要短信服务商与微信开放平台资质，本版本未提供。

### 发布资源

- 源码标签：`v0.6.13`；源码提交以 `release-manifest.json` 的 `sourceCommit` 为准。
- 公开发行仓库标签：`v0.6.13`。
- 发行清单 `release-manifest.json` 与 `SHA256SUMS` 作为本 Release 附件提供。
- 正式 Release：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/tag/v0.6.13>

---

## English

### What changed

- **Sign in and sign up without leaving the app**: on the web and in the Android app, enter your email in the sign-in sheet, tap "Send code", enter the code and tap "Sign in / Sign up". An email with no account gets one on the spot, and the sheet tells you it is new. You can also switch to "Password"; if you forgot it, just use the code. Chats you had as a guest come along into the account. Passkey and GitHub sign-in stay at the bottom of the sheet and still open the account service page.
- **In-app Android updates**: when "Me → App version & updates" finds a new release, "Download & install" downloads it inside the app with a progress bar you can cancel. The app then checks that the package is this app, is newer, carries the same signature and is complete, and only then opens the system installer. The first time, Android asks you to allow this app to "install unknown apps"; once allowed, installation continues when you come back. The browser is offered only if the download fails.
- **Mini programs**: WeChat and Douyin keep one-tap platform sign-in, unchanged.

### Platforms

- **Web H5**: <https://gogogo.plutokeating.beer/>
- **Android**: signed Universal and `arm64-v8a` APKs, `versionCode 6013`, 10,082,459 bytes, installs over 0.6.12. Both APKs are currently byte-identical because this release has no native `.so` payload.
  - Universal: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.13/GoGoGo-0.6.13-android-universal.apk>, SHA-256 `0b873abe93f53b4e050bfa0e95d97c3adf503cc549f70bf203d287358f7dfe4c`
  - arm64-v8a: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.13/GoGoGo-0.6.13-android-arm64-v8a.apk>, SHA-256 `0b873abe93f53b4e050bfa0e95d97c3adf503cc549f70bf203d287358f7dfe4c`
- **WeChat mini program**: development version `0.6.13` uploaded (artifact SHA-256 `f5e48c8d…`) and delivered through the enabled experience auto-update; not submitted for review and not a public release.
- **Douyin mini program**: preview `0.6.13` uploaded (artifact SHA-256 `215fb193…`, preview link <https://t.zijieimg.com/i4e1S3Un/>, no expiry returned by the platform); not submitted for review and not a public release.
- **iOS**: Apple distribution signing is still not configured; no IPA in this release.

### Compatibility and migration

- New endpoints `POST /api/auth/direct/code/start`, `/api/auth/direct/code/verify` and `/api/auth/direct/password`; the redirect sign-in (`/api/auth/oidc/*`) and mini-program sign-in are unchanged. No database migration.
- The app now declares `REQUEST_INSTALL_PACKAGES`, used only to hand a verified update of this app to the system installer.
- **In-app updates start with 0.6.13**: users on 0.6.12 or earlier need to install 0.6.13 once from the download page or a browser; later versions can then be updated inside the app.
- Storage formats for accounts, the on-device private profile, conversations and trips are unchanged; no cache clearing or re-sign-in is needed.

### Verification and known limits

- Backend: 59 test files / 366 cases pass. New coverage: signing up a new email with a code and bringing guest data along, signing out the account service's temporary session afterwards, a wrong password, refusing an email-binding ticket for sign-in, and sending nothing without consent.
- Browser checks, run once on a local build and once on the live site: a wrong password reported in place, signing up a new email with a code, the guest session carried into sign-in, never leaving the page, and the passkey/GitHub fallback round trip. On the live service, a non-existent account confirmed that the backend-to-account-service chain rejects a wrong password correctly.
- Android: both signed APKs pass the certificate, signature-scheme, permission (including the new install permission), production-resource and version gates. On a headless Android 14 emulator the build installed over the public 0.6.12, and the signed release passed install, WebView-debug-port-closed and background/foreground process checks. The debug-build deep interaction run was **not** executed.
- Downloading from GitHub can be slow on networks in mainland China; if the download fails, use the browser instead.
- Code delivery to a real mailbox, in-app updating on a physical phone and mini-program device acceptance have not been performed.
- SMS phone-number sign-in and WeChat sign-in inside the app or web page need an SMS provider and WeChat Open Platform qualifications and are not offered in this release.

### Release assets

- Source tag: `v0.6.13`; the source commit is the `sourceCommit` in `release-manifest.json`.
- Public release repository tag: `v0.6.13`.
- `release-manifest.json` and `SHA256SUMS` are attached to this release.
- Release: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/tag/v0.6.13>
