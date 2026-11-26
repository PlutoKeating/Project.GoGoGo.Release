# 走不走 v0.7.1 / GoGoGo v0.7.1

## 中文

### 本次更新

- **第一站快了很多**：狗狗GO 不再在动笔前长时间“思考”。正式环境同类请求里，第一站从发出请求算起 3–6 秒就出现在行程卡上，整条路线约 10–11 秒排完；此前同类请求要等十几秒，而且所有站点是同时冒出来的。
- **真正一站一站出现**：每选定一个地方就上屏一站，后面的站点依次补上，不会再一下子全部出现，也不会出现某一站先出现又消失的闪动。
- **等待时看得到它在忙什么**：发出消息后，行程卡出现前会有一块大的工作区——小狗的动作和一条四段进度轨道告诉你它正在想、在找地方、在挑站点还是在排路线；下面是你的出发点、当前天气和时间；找到的地点会以小图滚动经过，下面留着第一站的位置。行程卡一到就原地换上。没有一行提示文字。
- **页面更干净**：「行程」和「我的」页去掉了顶部的大标题。
- **登录更快**：登录和注册时服务端的数据库往返大幅减少（建账户、合并游客数据合成一步，会话在边缘直接签发），重新登录不再要等很久。

### 平台

- **Web H5**：<https://gogogo.plutokeating.beer/>
- **Android**：签名 Universal APK 与 `arm64-v8a` APK，`versionCode 7001`，10,086,555 bytes，可覆盖安装 0.7.0；已安装 0.6.13 及以上版本的用户可在「我的 → 应用版本与更新」里应用内升级。两个 APK 当前字节完全相同，因为本版本没有 native `.so` 负载。
  - Universal：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.7.1/GoGoGo-0.7.1-android-universal.apk>，SHA-256 `68e8bd3f838f7f98c21b268870ad976880f4374b88d8fefa3d64e3dde54c12b1`
  - arm64-v8a：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.7.1/GoGoGo-0.7.1-android-arm64-v8a.apk>，SHA-256 `68e8bd3f838f7f98c21b268870ad976880f4374b88d8fefa3d64e3dde54c12b1`
- **微信小程序**：`0.7.1` 开发版本已上传（产物 SHA-256 `7a263cb9…`），依赖已开启的体验内测自动更新；尚未提交审核，不是面向公众的正式上线。
- **抖音小程序**：`0.7.1` 预览版已上传（产物 SHA-256 `e49ea8cd…`，预览短链 <https://t.zijieimg.com/i4eYdXer/>，平台未返回到期时间）；尚未提交审核，不是面向公众的正式上线。
- **iOS**：仍缺少 Apple 分发签名配置，本版本没有 IPA。

### 兼容性与迁移

- 新流事件 `turn-context`（出发点、当前天气、时间）与 `candidates-peek`（正在查看的地点），只用于等待视图展示；不认识它们的旧客户端会忽略。`done.timing` 增加分段耗时字段。
- 画布还没有站点时，`write_itinerary` 不再一次写出整条路线，新路线由 `pin_stop` 逐站钉；`pin_stop` 不能在 `codemode` 脚本里调用。
- 对 DeepSeek 官方接口的请求现在带 `thinking: {type: "disabled"}`；其他模型服务商的请求不变。
- 服务端开启 Workers Logs，记录每轮各阶段耗时，不含对话内容与位置，保留 7 天。
- 没有数据库迁移；本机私人档案、会话与行程的存储格式不变，升级不需要清理缓存或重新登录。

### 验证范围与已知限制

- 后端 63 个测试文件 / 384 项用例通过，新增覆盖：新路线不能一次写出整条且 `pin_stop` 只能由模型直接调用；检索结果先于第一个站点下发候选预览；DeepSeek 请求体带关闭思考参数（本地探针）。
- 线上实测（正式模型，游客，三轮不同请求）：第一站 3.0–6.4 秒上屏，整轮 10.1–11.3 秒，站点数只增不减；模型首次输出 0.8–4.5 秒。部署后的第一个冷请求读取模型配置约 5.4 秒，之后命中缓存。以上数据来自海外网络测试机，**大陆免代理网络下的首卡时间尚未实测**；Cloudflare 免费网络在大陆的入口延迟与晚高峰丢包仍然存在（本版不涉及备案、香港入口或优选 IP）。
- 浏览器检查：`check:progressive-itinerary`（无文字工作台：阶段轨道、真实数据、候选滚动、首站槽位；随后逐站上屏、续传、停止）以及对话、行程页、本地优先、组局、导航驾驶舱、账号登录等 14 项既有检查通过。
- Android：双签名 APK 通过证书、签名形态、权限、正式资源与版本门禁；在无头 Android 14 模拟器上覆盖安装公开 0.7.0，正式签名包通过安装、调试端口关闭、前后台切换进程保持检查。**未执行**调试包深度交互实测。
- 登录提速只减少了服务端往返；验证码邮件的送达时间取决于账号服务的邮件发送，本版未改动。
- 小程序与 Android 的真机验收尚未进行。

### 发布资源

- 源码标签：`v0.7.1`；源码提交以 `release-manifest.json` 的 `sourceCommit` 为准。
- 公开发行仓库标签：`v0.7.1`。
- 国内下载镜像：<https://gogogo.williamhvollita.dpdns.org/releases/download/v0.7.1/GoGoGo-0.7.1-android-universal.apk>

## English

### What's new

- **The first stop comes much sooner**: 狗狗GO no longer "thinks" at length before it starts. In production, the first stop of a comparable request appears on the itinerary card 3–6 seconds after sending and the whole route is laid out in about 10–11 seconds; before, comparable requests took over a dozen seconds and every stop appeared at once.
- **Really one stop at a time**: each place lands as soon as it is chosen and the next ones follow — no more everything at once, and no stop that appears and then vanishes for a moment.
- **See what it is busy with while you wait**: until the itinerary card arrives, a large working view shows what 狗狗GO is doing — the puppy's pose and a four-step rail (thinking, looking for places, picking stops, laying out the route), your starting point, the weather now and the time, the places it found scrolling past as thumbnails, and a slot for the first stop. The card takes its place when it arrives. No status text.
- **Cleaner pages**: the Trip and Me tabs no longer have a big page title.
- **Faster sign-in**: signing in or up makes far fewer server-side database round trips (entering the account and merging guest data is one step, and the session is issued at the edge), so signing in again no longer drags.

### Platforms

- **Web H5**: <https://gogogo.plutokeating.beer/>
- **Android**: signed universal and `arm64-v8a` APKs, `versionCode 7001`, 10,086,555 bytes, installs over 0.7.0; users on 0.6.13 or later can update in the app from "Me → App version & updates". The two APKs are byte-identical for now because this release has no native `.so` payload.
  - Universal: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.7.1/GoGoGo-0.7.1-android-universal.apk>, SHA-256 `68e8bd3f838f7f98c21b268870ad976880f4374b88d8fefa3d64e3dde54c12b1`
  - arm64-v8a: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.7.1/GoGoGo-0.7.1-android-arm64-v8a.apk>, SHA-256 `68e8bd3f838f7f98c21b268870ad976880f4374b88d8fefa3d64e3dde54c12b1`
- **WeChat Mini Program**: `0.7.1` development version uploaded (artifact SHA-256 `7a263cb9…`), relying on the enabled automatic experience-version update; not submitted for review and not a public launch.
- **Douyin Mini Program**: `0.7.1` preview uploaded (artifact SHA-256 `e49ea8cd…`, preview link <https://t.zijieimg.com/i4eYdXer/>, no expiry returned by the platform); not submitted for review and not a public launch.
- **iOS**: Apple distribution signing is still missing; no IPA in this release.

### Compatibility and migration

- New stream events `turn-context` (starting point, weather now, time) and `candidates-peek` (places being looked at), for the waiting view only; older clients ignore them. `done.timing` gains per-phase fields.
- On an empty canvas `write_itinerary` no longer lays out a whole route; a new route is pinned stop by stop with `pin_stop`, which cannot be called from a `codemode` script.
- Requests to the DeepSeek official API now carry `thinking: {type: "disabled"}`; requests to other model providers are unchanged.
- Workers Logs is on, recording per-phase timings for each reply (no conversation text or locations), kept for 7 days.
- No database migration; local private profiles, conversations and trips keep their format, and no cache clearing or new sign-in is needed.

### Verification and known limitations

- Backend: 63 test files / 384 cases pass, newly covering that a new route cannot be written whole and `pin_stop` is model-only, that the candidate preview precedes the first stop patch, and (local probe) that DeepSeek requests carry the thinking-off parameter.
- Live tests with the production model (guest, three different requests): first stop at 3.0–6.4 s, whole reply 10.1–11.3 s, stop counts only grow; first model output 0.8–4.5 s. The first cold request after a deploy spent about 5.4 s reading the model configuration, then hit the cache. These numbers come from a test machine on an overseas network; **first-stop times on a mainland network without a proxy have not been measured yet**, and the entry latency and evening packet loss of Cloudflare's free network in mainland China remain (this release adds no ICP filing, Hong Kong entry or preferred IPs).
- Browser checks: `check:progressive-itinerary` (wordless working view with rail, real data, scrolling candidates and first-stop slot; then stop-by-stop arrival, resume and stop) plus 14 existing checks (conversation, itinerary page, local-first, group outing, navigation cockpit, account sign-in and more).
- Android: both signed APKs pass the certificate, signature scheme, permission, production-asset and version gates; on a headless Android 14 emulator the build installed over the public 0.7.0 and the signed release passed install, WebView-debug-port-closed and background/foreground checks. The debug-build deep interaction run was **not** executed.
- The sign-in speed-up removes server round trips only; how fast the code email arrives depends on the account service's mail delivery, which this release does not change.
- Mini-program and Android physical-device acceptance has not been done yet.

### Release assets

- Source tag: `v0.7.1`; the source commit is `sourceCommit` in `release-manifest.json`.
- Public release repository tag: `v0.7.1`.
- Mirror download (faster in mainland China): <https://gogogo.williamhvollita.dpdns.org/releases/download/v0.7.1/GoGoGo-0.7.1-android-universal.apk>
