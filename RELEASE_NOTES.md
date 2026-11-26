# 走不走 v0.6.12 / GoGoGo v0.6.12

## 中文

### 本次更新

- **结束行程随时都能点，点了就结束**：不管行程处在哪一步（包括群拍板还在等人入局、还没有路线），也不管另一个操作是否还在进行、网络是否断开，「···」里的「结束行程」和全部打卡后的「结束并评价」都能直接点。确认一次后行程立刻结束：导航、迷你导航胶囊、还没同步完的改动一起收起，「行程」页变成评价卡。之后不会再被改回去，联网后自动同步到云端。
- **群拍板：局主结束对所有人生效，局友只能退出**：局主结束群拍板后，所有局友的页面会在大约 15 秒内跟着收尾。局友不能结束整个局，只能「退出这个局」：退出后这个局会从你的行程里移除，局主那边人数和票数随之更新；要回来需要局主重新邀请。
- **删除对话随时都能删**：带着行程的对话、狗狗GO 正在回复的对话都可以删除。删除正在回复的对话会立刻停止回复并换成新的空白对话；删除带着行程的对话会一起结束那段行程（是群拍板时对所有局友结束），确认框会提前说明。删掉的对话不会再出现在历史里。
- **换行程会结束旧行程**：确认新的行程时，旧的个人行程会自动结束；如果你正在一个群拍板里，会先问你是否结束（局主）或退出（局友）。狗狗GO 在回复里自动打开的行程不会把你带离群拍板，也不会把你已结束的行程带回来。
- **没人结束的行程会自动结束**：最后一站离店 6 小时后（无路线的群拍板在创建 24 小时后），行程会自动标为已结束。
- **吉祥物与图标更新**：吉祥物改为完整形象（不再带徽章框），Android 启动图与桌面图标同步更新。

### 平台

- **Web H5**：<https://gogogo.plutokeating.beer/>
- **Android**：签名 Universal APK 与 `arm64-v8a` APK，`versionCode 6012`，10,074,267 bytes，可覆盖安装 0.6.11。两个 APK 当前字节完全相同，因为本版本没有 native `.so` 负载。
  - Universal：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.12/GoGoGo-0.6.12-android-universal.apk>，SHA-256 `0836358895caa8fa099b67f37850891ef9495483bdf6bb28da9ff218511ffc76`
  - arm64-v8a：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.12/GoGoGo-0.6.12-android-arm64-v8a.apk>，SHA-256 `0836358895caa8fa099b67f37850891ef9495483bdf6bb28da9ff218511ffc76`
- **微信小程序**：`0.6.12` 开发版本已上传（产物 SHA-256 `565f343d…`），依赖已开启的体验内测自动更新；尚未提交审核，不是面向公众的正式上线。
- **抖音小程序**：`0.6.12` 预览版已上传（产物 SHA-256 `68709541…`，预览短链 <https://t.zijieimg.com/i4JETCbA/>，平台未返回到期时间）；尚未提交审核，不是面向公众的正式上线。
- **iOS**：仍缺少 Apple 分发签名配置，本版本没有 IPA。

### 兼容性与迁移

- 数据库迁移 `018`（退出群拍板、自动结束），已在生产库应用；新增接口 `POST /api/sessions/:id/finish`、`POST /api/sessions/:id/leave`。删除对话接口不再返回“进行中的行程对话不能删除”。
- 旧版客户端继续可用：它们结束行程仍走原来的结束动作（现在不会再因版本或阶段被拒绝）。
- 账户、本机私人档案、本地会话、行程与草稿的存储格式不变；新增本机记录 `local:ended-trips` 用于记住已结束的行程与已删除的对话。升级不需要清理缓存或重新登录。

### 验证范围与已知限制

- 后端 59 个测试文件 / 362 项用例通过，新增覆盖：版本号过期也能结束、无路线也能结束、重复结束、非局主不能结束、退出后不可见与重复退出、退出后重新计票定案、局主不能退出、自动结束规则、删除对话连带结束群拍板。
- 前端新增浏览器检查：局主在另一个操作进行中且断网时结束群拍板（评价卡立刻出现、迟到回执与轮询不会复活、联网后自动送达）、局友退出、局主在别处结束后局友端收尾、被拒绝的删除不回滚、回复生成中删除当前对话。另有 13 项 H5 无头浏览器回归、本地优先、小程序输入框与品牌资源门禁通过。
- Android：双签名 APK 通过证书、签名形态、权限、正式资源与版本门禁；在无头 Android 14 模拟器上完成对公开 0.6.11 的覆盖安装（`versionCode 6012`、`versionName 0.6.12`），以及正式签名包的安装、调试端口关闭、前后台切换进程保持检查。**未执行**调试包的深度交互实测。
- 小程序上的结束、退出与删除流程只经过源码、构建与产物门禁，没有在开发者工具或真机里实测。
- 局友端感知局主结束依赖轮询，最长约 15 秒。
- **本轮验证仅限无头环境**：没有真机或可见浏览器的人工验收。

### 发布资源

- 源码标签：`v0.6.12`；源码提交以 `release-manifest.json` 的 `sourceCommit` 为准。
- 公开发行仓库标签：`v0.6.12`。
- 发行清单 `release-manifest.json` 与 `SHA256SUMS` 作为本 Release 附件提供。
- 正式 Release：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/tag/v0.6.12>

---

## English

### What changed

- **End a trip any time, and it ends**: whatever step the trip is at (including a group plan still waiting for people or without a route), and whether or not another action is still running or the network is down, End trip in the ··· menu and Finish and rate after the last check-in can always be tapped. After one confirmation the trip ends at once: navigation, the mini navigation island and unsynced changes are put away, and the Trip tab shows the review card. It is never undone; the cloud is updated once you are back online.
- **Group plans: the host ends it for everyone, members can leave**: when the host ends a group plan, every member's page follows within about 15 seconds. Members cannot end the whole plan; they can Leave this group plan, which removes it from their trips and updates the host's member and vote counts. Coming back needs a new invite from the host.
- **Delete a conversation any time**: conversations that carry a trip, and conversations 狗狗GO is still replying in, can be deleted. Deleting one with a reply in progress stops the reply and opens a new blank chat; deleting one that carries a trip ends that trip too (for every member, if it is a group plan), and the confirmation says so. Deleted conversations do not come back in History.
- **A new trip ends the old one**: confirming a new itinerary ends your previous personal trip; inside a group plan you are first asked whether to end it (host) or leave it (member). A plan that 狗狗GO opens by itself in a reply never takes you out of a group plan and never brings back a trip you ended.
- **Trips nobody ended end by themselves**: six hours after the last stop (24 hours after creation for a group plan that never got a route), a trip is marked as finished.
- **Mascot and icons**: the mascot is shown in full without a badge frame, and the Android splash screen and launcher icons are updated to match.

### Platforms

- **Web H5**: <https://gogogo.plutokeating.beer/>
- **Android**: signed Universal and `arm64-v8a` APKs, `versionCode 6012`, 10,074,267 bytes, installs over 0.6.11. Both files are currently byte-identical because this release has no native `.so` payload.
  - Universal: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.12/GoGoGo-0.6.12-android-universal.apk>, SHA-256 `0836358895caa8fa099b67f37850891ef9495483bdf6bb28da9ff218511ffc76`
  - arm64-v8a: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.12/GoGoGo-0.6.12-android-arm64-v8a.apk>, SHA-256 `0836358895caa8fa099b67f37850891ef9495483bdf6bb28da9ff218511ffc76`
- **WeChat Mini Program**: `0.6.12` development build uploaded (artifact SHA-256 `565f343d…`), delivered through the enabled internal-test auto update; not submitted for review, so not a public launch.
- **Douyin Mini Program**: `0.6.12` preview build uploaded (artifact SHA-256 `68709541…`, preview link <https://t.zijieimg.com/i4JETCbA/>, no expiry returned by the platform); not submitted for review, so not a public launch.
- **iOS**: no IPA because Apple distribution signing is not configured.

### Compatibility and migration

- Database migration `018` (leaving a group plan, ending trips automatically) is applied in production; new endpoints `POST /api/sessions/:id/finish` and `POST /api/sessions/:id/leave`. Deleting a conversation no longer fails with "a conversation with an active outing can't be deleted".
- Older clients keep working: they still end trips through the existing finish action, which is no longer refused for a stale version or a phase.
- Account data, on-device private profiles, local conversations, trips and drafts keep their format; a new on-device record `local:ended-trips` remembers ended trips and deleted conversations. Upgrading needs no cache clearing or re-login.

### Verification and known limits

- Backend: 59 test files / 362 tests pass, newly covering ending with a stale version, ending without a route, ending twice, non-hosts not ending, leaving (no longer visible, leaving twice), a re-count that decides after someone leaves, the host not leaving, the auto-end rule, and deleting a conversation ending its group plan.
- New frontend browser checks: the host ends a group plan while another action is running and the network is down (review card at once, late replies and polls do not bring it back, delivered once online), a member leaves, members wind down after the host ended elsewhere, a refused delete is not rolled back, and deleting the current conversation mid-reply. Thirteen more headless H5 browser regressions, the local-first, mini-program composer and brand-asset gates pass.
- Android: both signed APKs pass the certificate, signature-scheme, permission, production-resource and version gates; on a headless Android 14 emulator the build installed over the public 0.6.11 (`versionCode 6012`, `versionName 0.6.12`) and the signed release passed the install, debug-port-closed and background/foreground process checks. The deep interaction run of the debug build was **not** executed.
- In the mini programs, ending, leaving and deleting were checked through source, build and artifact gates only, not in devtools or on a device.
- Members learn that the host ended a plan through polling, within about 15 seconds.
- **Verification is headless only**: no real-device or visible-browser manual acceptance.

### Release assets

- Source tag: `v0.6.12`; the exact source commit is recorded as `sourceCommit` in `release-manifest.json`.
- Public release repository tag: `v0.6.12`.
- `release-manifest.json` and `SHA256SUMS` are attached to this Release.
- Release: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/tag/v0.6.12>
