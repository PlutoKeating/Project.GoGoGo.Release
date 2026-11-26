# 走不走 v0.7.3 / GoGoGo v0.7.3

## 中文

### 本次更新

- **带约束入局、提想法立刻完成**：带饮食、健康、预算等要求加入组局，或在局里提一个想法，现在约 0.5 秒（服务端）就完成；此前带要求入局要等约 15 秒，带想法入局和提想法会在约 20 秒后失败。
- **路线在后台为大家调整**：需要为新要求或新想法调整路线时，路线会在后台重新安排，多数约 6–7 秒后自动推送到每位成员的手机上，并沿用“别人改了行程”的站点高亮与说明。调整期间，群局路线上会出现一层轻微的扫光和一只奔跑的小狗（没有文字），这时照常可以投票、换店、编辑；如果期间有人改了行程，路线会在最新版本上重新安排，不会覆盖别人的修改。
- **同一组想法不再重复等待**：大家写的想法读一次就记住，之后只补充饮食、预算的入局不再等这一步；附近地点的查询结果也在边缘缓存，重复查询几乎不花时间。
- **路线写入更快**：行程保存到服务器时压缩路线坐标（体积约减少四分之三），群局里改行程、打卡、调整路线的写入都更快；读到的行程和以前完全一样。
- **对话里排路线也更快**：各站之间的路线改为同时查询，不再一段一段等。

### 平台

- **Web H5**：<https://gogogo.plutokeating.beer/>
- **Android**：签名 Universal APK 与 `arm64-v8a` APK，`versionCode 7003`，10,090,651 bytes，可覆盖安装 0.7.2；已安装 0.6.13 及以上版本的用户可在「我的 → 应用版本与更新」里应用内升级。两个 APK 当前字节完全相同，因为本版本没有 native `.so` 负载。
  - Universal：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.7.3/GoGoGo-0.7.3-android-universal.apk>，SHA-256 `9b34fd3194baa8ecdbea7927d11adf6b09feb2c5ec3fa374652df06365dd352f`
  - arm64-v8a：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.7.3/GoGoGo-0.7.3-android-arm64-v8a.apk>，SHA-256 `9b34fd3194baa8ecdbea7927d11adf6b09feb2c5ec3fa374652df06365dd352f`
- **微信小程序**：`0.7.3` 开发版本已上传（产物 SHA-256 `e01515d3…`），依赖已开启的体验内测自动更新；尚未提交审核，不是面向公众的正式上线。实时推送仍需在小程序后台把 API 域名加入 socket 合法域名，配置前自动使用 15 秒一次的轻量检查。
- **抖音小程序**：`0.7.3` 预览版已上传（产物 SHA-256 `1a677f33…`，预览短链 <https://t.zijieimg.com/i4eMrmFa/>，平台未返回到期时间）；尚未提交审核，不是面向公众的正式上线。socket 合法域名同上。
- **iOS**：仍缺少 Apple 分发签名配置，本版本没有 IPA。

### 兼容性与迁移

- `POST /api/sessions/join` 与 `POST /api/sessions/:id/idea` 在需要调整路线时立即返回 `replanning: true`（返回的路线尚未调整），调整后的路线作为新 revision 经实时通道推送；实时通道新增 `{type:"replanning",active}` 消息。旧客户端会忽略新字段，在下次读取时拿到新路线。
- 后台调整只写回到它读取时的版本；期间有其他修改则在新版本上重算，因此推送的 revision 可能比回执大不止 1。
- 服务器保存行程时压缩路线坐标（精度约 0.1 米），接口返回的格式不变；之前保存的行程照常读出。
- 没有数据库迁移；本机私人档案、会话与行程的存储格式不变，升级不需要清理缓存或重新登录。

### 验证范围与已知限制

- 后端 66 个测试文件 / 406 项用例通过，新增覆盖：带约束入局立即返回且路线未动、只在需要时排队调整、想法立即保存、后台调整只写回读到的版本并在并发修改后重算、路线压缩的精确往返与旧数据兼容。
- 生产实测（游客、海外测试机，同一脚本连续多轮）：带约束入局、带想法入局、提想法的服务端耗时约 0.47–0.84 秒；新路线经推送到达多数约 6–7 秒（5.9–11.7 秒）。改前这三种操作分别约 15 秒、约 20 秒后 503、约 20 秒后 503。后台日志 `group_replan` 记录各阶段耗时（不含想法、约束与地点）。
- 用探针 Worker 经真实 Hyperdrive 实测：向数据库上传 30KB 约 1.1 秒、120KB 约 6–8 秒，读回同样大小只要约 0.3–0.6 秒；这是压缩路线坐标的依据。
- 浏览器检查：`check:trip-end`（新增后台调整场景：入局者回执立即显示无文字标记、结束后换上新路线；另一成员仅凭实时消息看到标记）、`check:group-outing`、`check:local-first`、`check:interaction-state`、`check:local-first-ui`、`check:interaction-ui`、`check:trip-phase`、`check:ui-block`、`check:navigation-cockpit`、`check:progressive-itinerary`、`check:itinerary-page` 通过；`conversation-ui-check` 一条 v0.7.0 起过时的文字断言与 `check:h5-canonical` 登录一步失败为既有问题。
- Android：双签名 APK 通过证书、签名形态、权限、正式资源与版本门禁；在无头 Android 14 模拟器上覆盖安装公开 0.7.2，正式签名包通过安装、调试端口关闭、前后台切换进程保持检查。**未执行**调试包深度交互实测。
- **大陆免代理网络下的耗时尚未实测**；新路线的到达时间主要取决于地图服务响应，预算很低时会多一次严格预算重排。小程序实时推送依赖 socket 合法域名配置；小程序与 Android 真机验收尚未进行。

### 发布资源

- 源码标签：`v0.7.3`；源码提交以 `release-manifest.json` 的 `sourceCommit` 为准。
- 公开发行仓库标签：`v0.7.3`。
- 国内下载镜像：<https://gogogo.williamhvollita.dpdns.org/releases/download/v0.7.3/GoGoGo-0.7.3-android-universal.apk>

## English

### What's new

- **Joining with needs and adding ideas finish at once**: joining a group outing with diet, health or budget needs, or adding an idea in the group, now completes in about 0.5 s on the server; before, joining with needs took about 15 s, and joining with an idea or adding one failed after about 20 s.
- **The route is adjusted for everyone in the background**: when new needs or ideas call for a different route, it is reworked in the background and usually reaches every member's phone about 6–7 s later, with the usual "someone changed the plan" highlights and explanation. While it is being adjusted, the group route shows a light sweep and a running puppy (no text); you can keep voting, swapping places and editing, and if someone edits meanwhile the route is reworked on the newest version instead of overwriting their change.
- **The same ideas are not waited for twice**: what the group's ideas ask for is read once and remembered, so later joins that only add diet or budget needs skip that step; nearby place lookups are cached at the edge as well.
- **Faster route saving**: route coordinates are compacted when an itinerary is saved on the server (about three quarters smaller), which speeds up editing, check-ins and route adjustments in groups; itineraries read back exactly as before.
- **Faster routes in conversations too**: the legs between stops are now looked up together instead of one after another.

### Platforms

- **Web H5**: <https://gogogo.plutokeating.beer/>
- **Android**: signed universal and `arm64-v8a` APKs, `versionCode 7003`, 10,090,651 bytes, installs over 0.7.2; users on 0.6.13 or later can update in the app from "Me → App version & updates". The two APKs are byte-identical for now because this release has no native `.so` payload.
  - Universal: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.7.3/GoGoGo-0.7.3-android-universal.apk>, SHA-256 `9b34fd3194baa8ecdbea7927d11adf6b09feb2c5ec3fa374652df06365dd352f`
  - arm64-v8a: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.7.3/GoGoGo-0.7.3-android-arm64-v8a.apk>, SHA-256 `9b34fd3194baa8ecdbea7927d11adf6b09feb2c5ec3fa374652df06365dd352f`
- **WeChat Mini Program**: `0.7.3` development version uploaded (artifact SHA-256 `e01515d3…`), relying on the enabled automatic experience-version update; not submitted for review and not a public launch. Live updates still need the API domain in the mini program's socket domain list; until then it uses the 15-second light check.
- **Douyin Mini Program**: `0.7.3` preview uploaded (artifact SHA-256 `1a677f33…`, preview link <https://t.zijieimg.com/i4eMrmFa/>, no expiry returned by the platform); not submitted for review and not a public launch. Same socket domain note.
- **iOS**: Apple distribution signing is still missing; no IPA in this release.

### Compatibility and migration

- `POST /api/sessions/join` and `POST /api/sessions/:id/idea` answer at once with `replanning: true` when the route needs adjusting (the returned route is not adjusted yet); the adjusted route arrives as a newer revision over the live channel, which also sends `{type:"replanning",active}`. Older clients ignore the new field and get the new route on their next read.
- A background adjustment writes back only onto the revision it read; if the outing changed meanwhile it is reworked on the newer version, so the pushed revision may be more than one above the reply's.
- The server compacts route coordinates when storing itineraries (about 0.1 m precision); the API format is unchanged and itineraries stored earlier read as before.
- No database migration; local private profiles, conversations and trips keep their format, and no cache clearing or new sign-in is needed.

### Verification and known limitations

- Backend: 66 test files / 406 cases pass, newly covering: joining with needs answers at once with the route untouched, adjustments queue only when needed, ideas are saved at once, background adjustments write back only onto the revision they read and recompute after concurrent changes, and exact round trips of compacted routes with old data still readable.
- Production (guest, overseas test machine, several consecutive runs of one script): server time for joining with needs, joining with an idea and adding an idea is about 0.47–0.84 s; the new route arrives by push in about 6–7 s in most runs (5.9–11.7 s). Before: about 15 s, a 503 after about 20 s, and a 503 after about 20 s. The background log `group_replan` records phase timings (no ideas, needs or places).
- Measured through real Hyperdrive with a probe Worker: sending 30 KB to the database takes about 1.1 s and 120 KB about 6–8 s, while reading the same sizes back takes about 0.3–0.6 s — the reason route coordinates are compacted.
- Browser checks: `check:trip-end` (new background-adjustment scenario: the joiner's reply shows the wordless mark at once and the new route replaces it; another member sees the mark from live messages alone), `check:group-outing`, `check:local-first`, `check:interaction-state`, `check:local-first-ui`, `check:interaction-ui`, `check:trip-phase`, `check:ui-block`, `check:navigation-cockpit`, `check:progressive-itinerary` and `check:itinerary-page` pass; one `conversation-ui-check` text assertion outdated since v0.7.0 and `check:h5-canonical` failing at sign-in are pre-existing.
- Android: both signed APKs pass the certificate, signature scheme, permission, production-asset and version gates; on a headless Android 14 emulator the build installed over the public 0.7.2 and the signed release passed install, WebView-debug-port-closed and background/foreground checks. The debug-build deep interaction run was **not** executed.
- **Timings on a mainland network without a proxy have not been measured yet**; when the new route arrives depends mostly on the map service, and a very low budget adds one strict-budget recommendation. Live updates in mini programs depend on the socket domain configuration; mini-program and Android physical-device acceptance has not been done yet.

### Release assets

- Source tag: `v0.7.3`; the source commit is `sourceCommit` in `release-manifest.json`.
- Public release repository tag: `v0.7.3`.
- Mirror download (faster in mainland China): <https://gogogo.williamhvollita.dpdns.org/releases/download/v0.7.3/GoGoGo-0.7.3-android-universal.apk>
