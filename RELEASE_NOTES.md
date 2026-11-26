# 走不走 v0.7.2 / GoGoGo v0.7.2

## 中文

### 本次更新

- **所有操作都快了很多，组局尤其明显**：好友组局的发起、加入、提想法、投票、定案、出发、打卡、改行程、结束，以及评价、会话列表、打开行程，都重写成“每个请求只等必要的步骤”。正式环境服务端耗时（同一组请求，改前 → 改后）：打开一个局约 7 秒 → 约 0.45 秒；行程列表约 8.5 秒 → 约 0.5 秒；加入组局约 17 秒 → 约 0.8 秒；局主在定案后出发并打卡约 35 秒 → 约 1.3 秒；结束行程此前会超时失败 → 约 0.5 秒。
- **组局状态实时更新**：打开的群拍板与服务器保持一条实时连接，有人投票、提想法、改行程、出发、打卡或结束时立即推送，只在确实有变化时才读取一次；不再每隔几秒反复向服务器查询。连接断开时自动退回每 15 秒一次的轻量检查（没有变化时服务器不读数据库），并自动重连。
- **少发很多请求**：定案后的第一次打卡直接出发（原来要先“出发”再“打卡”两次请求）；发起和加入组局不再先等身份查询；结束、退出、评价、删除黑名单后直接用服务器的回执更新本机，不再整页重新拉取；删除带行程的对话不再重复结束同一个局；现场救急重排一次请求写回群局；保存私人档案不再先读一遍；多张图片同时上传；回到前台不再重新拉取本人档案、评价和黑名单。

### 平台

- **Web H5**：<https://gogogo.plutokeating.beer/>
- **Android**：签名 Universal APK 与 `arm64-v8a` APK，`versionCode 7002`，10,090,651 bytes，可覆盖安装 0.7.1；已安装 0.6.13 及以上版本的用户可在「我的 → 应用版本与更新」里应用内升级。两个 APK 当前字节完全相同，因为本版本没有 native `.so` 负载。
  - Universal：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.7.2/GoGoGo-0.7.2-android-universal.apk>，SHA-256 `e7d491218de15627a4fc175c81c4274fca822a095c4ec746ada3145ebeb199df`
  - arm64-v8a：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.7.2/GoGoGo-0.7.2-android-arm64-v8a.apk>，SHA-256 `e7d491218de15627a4fc175c81c4274fca822a095c4ec746ada3145ebeb199df`
- **微信小程序**：`0.7.2` 开发版本已上传（产物 SHA-256 `5bb34f2a…`），依赖已开启的体验内测自动更新；尚未提交审核，不是面向公众的正式上线。实时推送需要在小程序后台把 API 域名加入 socket 合法域名；配置前自动使用 15 秒一次的轻量检查。
- **抖音小程序**：`0.7.2` 预览版已上传（产物 SHA-256 `ec6d7c22…`，预览短链 <https://t.zijieimg.com/i4ejKrrx/>，平台未返回到期时间）；尚未提交审核，不是面向公众的正式上线。socket 合法域名同上。
- **iOS**：仍缺少 Apple 分发签名配置，本版本没有 IPA。

### 兼容性与迁移

- 新增 `GET /api/sessions/:id/live`（WebSocket，会话令牌作为子协议 `gogogo, <token>` 传入），推送 `{type:"revision",revision}`；新增 `GET /api/sessions/:id?known=<revision>`，未变化时返回 `{unchanged:true}`。
- 局主在 `confirmed` 阶段的第一次 `checkin` 同时出发；`POST /api/feedback` 返回写入的评价与屏蔽项；`POST /api/plan/reroute` 写回群局时返回 `sessionRevision`；`finish` 不再顺带清理过期访客（由每小时定时任务负责）。旧客户端的请求方式仍然有效。
- 所有 API 应答带 `Server-Timing: app;dur=…`。
- 没有数据库迁移；本机私人档案、会话与行程的存储格式不变，升级不需要清理缓存或重新登录。

### 验证范围与已知限制

- 后端 64 个测试文件 / 398 项用例通过；新增覆盖：组局各操作的批量语句、定案后打卡即出发、单语句评价与列表、带引号／反斜杠／注入式文本／emoji 的字符串原样往返、出错整批拒绝。
- 在真实 PostgreSQL 17 上逐项核对权限拒绝、行级隔离、版本冲突、重放保护、重复结束与出错回滚，并与旧代码在同一模拟链路（每次往返 100ms）对照：读一局 12 → 1 次往返，入局 24 → 1，局主改动 24 → 2，定案后打卡 57 → 2，结束 17 → 1。
- 正式环境（游客、海外测试机）复测见上；实时通道已在正式环境验证：非成员被拒绝，成员连上即收到当前版本，写入完成后约 0.2 秒收到推送，`ping`／`pong` 正常。**大陆免代理网络下的整体耗时尚未实测**；带新约束的入局与重排想法仍包含模型与地图调用的时间。
- 浏览器检查：`check:local-first`、`check:interaction-state`、`check:trip-end`（新增条件读取降级与模拟推送）及组局、行程页、导航、对话等既有检查通过；`conversation-ui-check` 仍有一条 v0.7.0 起过时的文字断言，`check:h5-canonical` 仍在登录一步失败（均为既有问题）。
- Android：双签名 APK 通过证书、签名形态、权限、正式资源与版本门禁；在无头 Android 14 模拟器上覆盖安装公开 0.7.1，正式签名包通过安装、调试端口关闭、前后台切换进程保持检查。**未执行**调试包深度交互实测。
- 小程序实时推送依赖平台后台的 socket 合法域名配置（未配置时自动退回轻量检查）；小程序与 Android 的真机验收尚未进行。

### 发布资源

- 源码标签：`v0.7.2`；源码提交以 `release-manifest.json` 的 `sourceCommit` 为准。
- 公开发行仓库标签：`v0.7.2`。
- 国内下载镜像：<https://gogogo.williamhvollita.dpdns.org/releases/download/v0.7.2/GoGoGo-0.7.2-android-universal.apk>

## English

### What's new

- **Everything is much faster, group outings most of all**: starting, joining, adding ideas, voting, sealing, setting off, checking in, editing and ending a group outing — plus ratings, the trip list and opening a trip — now wait only for the steps each request really needs. Server time in production for the same requests, before → after: opening an outing about 7 s → about 0.45 s; the trip list about 8.5 s → about 0.5 s; joining about 17 s → about 0.8 s; the host setting off and checking in after sealing about 35 s → about 1.3 s; ending a trip used to time out → about 0.5 s.
- **Live group updates**: an open group outing keeps a live connection to the server. Votes, ideas, edits, setting off, check-ins and ending are pushed at once, and the outing is read only when something actually changed — no more asking the server every few seconds. If the connection drops it falls back to a light check every 15 seconds (the server skips the database when nothing changed) and reconnects by itself.
- **Far fewer requests**: the first check-in after sealing sets off in the same request (before: "set off", then "check in"); starting and joining a group no longer wait for an identity lookup first; ending, leaving, rating and unblocking update this device from the server's reply instead of reloading everything; deleting a conversation that carries a trip no longer ends it twice; an on-site reroute writes back to the group in one request; saving the private profile no longer reads it first; several images upload at once; returning to the foreground no longer reloads your profile, ratings and blocked places.

### Platforms

- **Web H5**: <https://gogogo.plutokeating.beer/>
- **Android**: signed universal and `arm64-v8a` APKs, `versionCode 7002`, 10,090,651 bytes, installs over 0.7.1; users on 0.6.13 or later can update in the app from "Me → App version & updates". The two APKs are byte-identical for now because this release has no native `.so` payload.
  - Universal: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.7.2/GoGoGo-0.7.2-android-universal.apk>, SHA-256 `e7d491218de15627a4fc175c81c4274fca822a095c4ec746ada3145ebeb199df`
  - arm64-v8a: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.7.2/GoGoGo-0.7.2-android-arm64-v8a.apk>, SHA-256 `e7d491218de15627a4fc175c81c4274fca822a095c4ec746ada3145ebeb199df`
- **WeChat Mini Program**: `0.7.2` development version uploaded (artifact SHA-256 `5bb34f2a…`), relying on the enabled automatic experience-version update; not submitted for review and not a public launch. Live updates need the API domain added to the mini program's socket domain list; until then it uses the 15-second light check.
- **Douyin Mini Program**: `0.7.2` preview uploaded (artifact SHA-256 `ec6d7c22…`, preview link <https://t.zijieimg.com/i4ejKrrx/>, no expiry returned by the platform); not submitted for review and not a public launch. Same socket domain note.
- **iOS**: Apple distribution signing is still missing; no IPA in this release.

### Compatibility and migration

- New `GET /api/sessions/:id/live` (WebSocket; the session token is passed as the subprotocol `gogogo, <token>`) pushing `{type:"revision",revision}`; new `GET /api/sessions/:id?known=<revision>` answering `{unchanged:true}` when nothing changed.
- The host's first `checkin` in the `confirmed` phase also sets off; `POST /api/feedback` returns the stored rating and block; `POST /api/plan/reroute` returns `sessionRevision` when it writes back to a group; `finish` no longer cleans up expired guests (the hourly schedule does). Older clients' requests still work.
- Every API answer carries `Server-Timing: app;dur=…`.
- No database migration; local private profiles, conversations and trips keep their format, and no cache clearing or new sign-in is needed.

### Verification and known limitations

- Backend: 64 test files / 398 cases pass, newly covering the batched statements of each group operation, setting off on the first check-in after sealing, single-statement ratings and lists, strings with quotes, backslashes, injection-like text and emoji round-tripping exactly, and whole-batch rejection on errors.
- On a real PostgreSQL 17, permission refusals, row-level isolation, revision conflicts, replay protection, repeated ending and rollback on errors were checked one by one and compared with the old code over the same simulated link (100 ms per round trip): opening an outing 12 → 1 round trips, joining 24 → 1, host edits 24 → 2, checking in after sealing 57 → 2, ending 17 → 1.
- Production timings (guest, overseas test machine) are above. The live channel was verified in production: non-members are refused, members get the current revision on connecting and the push about 0.2 s after a write completes, and `ping`/`pong` works. **End-to-end timings on a mainland network without a proxy have not been measured yet**; joining with new needs and replanning ideas still include the model and map calls.
- Browser checks: `check:local-first`, `check:interaction-state`, `check:trip-end` (new: conditional-read fallback and simulated pushes) and the existing group, trip page, navigation and conversation checks pass; `conversation-ui-check` still has one text assertion outdated since v0.7.0 and `check:h5-canonical` still fails at sign-in (both pre-existing).
- Android: both signed APKs pass the certificate, signature scheme, permission, production-asset and version gates; on a headless Android 14 emulator the build installed over the public 0.7.1 and the signed release passed install, WebView-debug-port-closed and background/foreground checks. The debug-build deep interaction run was **not** executed.
- Live updates in mini programs depend on the platforms' socket domain configuration (otherwise the light check is used); mini-program and Android physical-device acceptance has not been done yet.

### Release assets

- Source tag: `v0.7.2`; the source commit is `sourceCommit` in `release-manifest.json`.
- Public release repository tag: `v0.7.2`.
- Mirror download (faster in mainland China): <https://gogogo.williamhvollita.dpdns.org/releases/download/v0.7.2/GoGoGo-0.7.2-android-universal.apk>
