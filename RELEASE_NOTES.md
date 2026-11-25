# 走不走 v0.6.5 / GoGoGo v0.6.5

## 中文

### 本次更新

- **点了就有回应**：需要云端处理的操作（登录与绑定、发起群拍板、入局、投票、融入想法、定案、出发、结束行程、云端行程打卡、顺延、现场救急重排、导出与删除数据、地点搜索）点下去后，该按钮立刻显示转圈和进行中文案，其余同类按钮同时锁定。
- **连点不再重复提交**：连续点按不会再发出第二个请求。此前连点可能重复发送验证码、重复开房、重复入局或重复重排。
- **删除会话不会再“复活”**：删除立即生效；网络不通时在后台自动重试，期间历史列表刷新也不会把它带回来，重启应用后仍保持删除。只有服务端明确拒绝时才恢复该会话并说明原因。行程仍在进行的会话在点击时就提示不能删除。
- **移出避雷名单、保存评价、现场反馈同样即时生效**：点击即完成，后台投递并自动重试；现场反馈每个地点只记一次。
- **行程编辑不再被改回去**：云端行程上的改动（锁站、换店、排序、加站删站、改标题）在网络不通时保留在本机并提示一次“改动已保存在本机，网络恢复后自动同步”，恢复后自动送达。只是别人投票或入局时不打扰你；局友确实改过行程时采用最新版本并提示。
- **“确认放入行程”更稳**：新行程立即出现在「行程」页，不再等云端回执；同一张卡重复确认不会生成多个云端行程；保存失败自动重试。
- **偏好保存更诚实**：网络不通时提示“已保存在本机，联网后自动同步”并自动重试；只有其他设备已改过偏好时才请你核对。
- **退出登录即时完成**，不再等待服务器。
- **修复**：网页与 Android 上，历史对话面板第二次打开后删除确认框的两个按钮都点不动；卡片上的快捷动作连点会多发一条重复消息；微信分享海报打开期间反复申请动态消息。

### 平台

- **Web H5**：<https://gogogo.plutokeating.beer/>（Pages 生产部署 `ee4f6de1`）
- **Android**：签名 Universal APK 与 `arm64-v8a` APK，`versionCode 6005`，9,955,186 bytes，可覆盖安装 0.6.4。两个 APK 当前字节完全相同，因为本版本没有 native `.so` 负载。
  - Universal：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.5/GoGoGo-0.6.5-android-universal.apk>，SHA-256 `e433ac4992d041ad04045d4a40393fcde6584cb4eab6e45da5bde9b77daf3103`
  - arm64-v8a：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.5/GoGoGo-0.6.5-android-arm64-v8a.apk>，SHA-256 `e433ac4992d041ad04045d4a40393fcde6584cb4eab6e45da5bde9b77daf3103`
- **微信小程序**：`0.6.5` 开发版本已上传（`2026-11-25T18:59:16Z`，产物 SHA-256 `ab727327…2f86e`），依赖已开启的体验内测自动更新；尚未提交审核，不是面向公众的正式上线。
- **抖音小程序**：`0.6.5` 预览版已上传（`2026-11-25T19:00:22Z`，产物 SHA-256 `999eeac9…7e08d`，预览短链 <https://t.zijieimg.com/i4J3uuca/>，平台未返回到期时间）；尚未提交审核，不是面向公众的正式上线。
- **iOS**：仍缺少 Apple 分发签名配置，本版本没有 IPA。

### 兼容性与迁移

- 无数据库迁移，接口请求与响应格式不变。
- 本版本客户端不依赖新的后端：防连点、去重与失败后先核对再重试都在客户端完成。源码中另有两处服务端重放保护（同一方案短时间内重复创建行程返回同一个行程；同一人对同一地点的同类现场反馈 30 分钟内只计一次），后端已随本次发布上线（Worker 版本 `85149248`），线上实测同一方案连续提交两次返回同一个行程。
- 账户、本机私人档案、本地会话与草稿的存储格式保持不变；升级不需要清理缓存或重新登录。本机新增三个待送达记录键，不参与缓存淘汰。

### 验证范围与已知限制

- 后端 347 项测试通过。前端类型检查，以及本地优先、交互状态机、对话体验、H5 Canonical、群拍板、导航驾驶舱、声明式卡片、账户登录、选点器、请求错误等无头回归通过。
- 新增的无头浏览器检查覆盖：断网删除会话不复活并自动送达、重启后仍隐藏、被拒绝时回滚并说明；行程编辑在断网时熬过轮询与重试后送达、仅版本号变动时静默重发、真实冲突采用云端版本；云端操作与卡片动作连点只发一次并显示进行中。
- 微信／抖音：使用正式接口地址构建并通过产物门禁，取得上传回执。
- Android：双签名 APK 通过证书、签名形态、权限、正式资源与版本门禁；在无头 Android 14 模拟器上完成对 0.6.4 的覆盖安装（`versionCode 6005`、`versionName 0.6.5`），以及正式签名包的安装、调试端口关闭、前后台切换进程保持检查。**未执行**调试包的深度交互实测（含真实模型生成行程卡），因此不声称该项通过。
- **本轮验证仅限无头环境**：没有真机、微信／抖音开发者工具或可见浏览器的人工验收。弱网与断网下的重试时机、小程序宿主在后台时的网络恢复事件、加载指示在各宿主的实际渲染仍需真机确认。
- 云端行程打卡仍需等待云端结果（多人共享状态），只是增加了进行中反馈；消息发送断线后仍不自动重发（服务端没有幂等键），沿用“先核对发送状态再重试”。

### 发布资源

- 源码标签：`v0.6.5`；源码提交以 `release-manifest.json` 的 `sourceCommit` 为准。
- 公开发行仓库标签：`v0.6.5`。
- 发行清单 `release-manifest.json` 与 `SHA256SUMS` 作为本 Release 附件提供。
- 正式 Release：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/tag/v0.6.5>

---

## English

### What changed

- **Every tap answers**: for actions the cloud has to process (sign-in and linking, opening a group vote, joining, voting, adding an idea, locking the plan, starting, ending an outing, check-in on a cloud outing, delaying, on-site re-planning, exporting and deleting data, place search) the tapped button immediately shows a spinner and a working label, and the other buttons of that kind are locked meanwhile.
- **A double tap no longer submits twice**: repeated taps do not send a second request. Before, they could send a second verification code, open a second room, join twice or re-plan twice.
- **A deleted conversation no longer comes back**: deletion takes effect at once; while the network is away it retries in the background, a history refresh in the meantime does not bring the row back, and it stays deleted after restarting the app. The conversation is restored only if the server actually refuses, with the reason. A conversation whose outing is still in progress says so when tapped.
- **Removing a place from the avoid list, saving a review and on-site reports work the same way**: done on tap, delivered and retried in the background; an on-site report is recorded once per place.
- **Itinerary edits are no longer undone**: changes to a cloud outing (locking, swapping, reordering, adding or removing stops, renaming) stay on the device while the network is away, with one notice “Saved on this device. It will sync when the connection is back”, and are delivered automatically afterwards. You are not interrupted when a friend merely voted or joined; when a friend really changed the itinerary, the latest version is shown with a notice.
- **“Add to Trip” is sturdier**: the new plan appears on the Trip tab at once without waiting for the cloud; confirming the same card again no longer creates several cloud outings; a failed save retries by itself.
- **More honest preference saving**: while offline it says “Saved on this device. It will sync when you’re back online” and retries; you are asked to review only when another device changed your preferences.
- **Signing out is immediate** and no longer waits for the server.
- **Fixes**: on the web and Android, both buttons of the delete confirmation were dead the second time the History sheet was opened; a double tap on a card action sent a duplicate message; the WeChat share poster kept requesting an updatable-message activity while open.

### Platforms

- **Web H5**: <https://gogogo.plutokeating.beer/> (Pages production deployment `ee4f6de1`)
- **Android**: signed Universal and `arm64-v8a` APKs, `versionCode 6005`, 9,955,186 bytes, installs over 0.6.4. Both files are currently byte-identical because this release has no native `.so` payload.
  - Universal: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.5/GoGoGo-0.6.5-android-universal.apk>, SHA-256 `e433ac4992d041ad04045d4a40393fcde6584cb4eab6e45da5bde9b77daf3103`
  - arm64-v8a: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.6.5/GoGoGo-0.6.5-android-arm64-v8a.apk>, SHA-256 `e433ac4992d041ad04045d4a40393fcde6584cb4eab6e45da5bde9b77daf3103`
- **WeChat Mini Program**: `0.6.5` development build uploaded (`2026-11-25T18:59:16Z`, artifact SHA-256 `ab727327…2f86e`), delivered through the enabled internal-test auto update; not submitted for review, so not a public launch.
- **Douyin Mini Program**: `0.6.5` preview build uploaded (`2026-11-25T19:00:22Z`, artifact SHA-256 `999eeac9…7e08d`, preview link <https://t.zijieimg.com/i4J3uuca/>, no expiry returned by the platform); not submitted for review, so not a public launch.
- **iOS**: no IPA because Apple distribution signing is not configured.

### Compatibility and migration

- No database migration; request and response formats are unchanged.
- This client does not depend on a new backend: tap locking, de-duplication and “check first, then retry” all happen on the client. The source also contains two server-side replay guards (creating an outing from the same plan again within a short window returns the same outing; the same person’s same on-site report about a place counts once per 30 minutes). The backend went live with this release (Worker version `85149248`); a live check confirmed that submitting the same plan twice returns the same outing.
- Account data, on-device private profiles, local conversations and drafts keep their format; upgrading needs no cache clearing or re-login. Three new on-device keys hold writes that are still to be delivered and are exempt from cache eviction.

### Verification and known limits

- 347 backend tests pass. Frontend type check and the headless regressions for local-first storage, the interaction state machines, the conversation experience, H5 Canonical, group outings, the navigation cockpit, declarative cards, account sign-in, the location picker and request errors pass.
- New headless browser checks cover: an offline conversation delete that stays deleted and is delivered, stays hidden after a restart, and rolls back with the reason when refused; an itinerary edit that survives polls and retries while offline and then lands, a silent resend when only the revision moved, the server version on a real conflict; one request and a working state for a double tap on cloud actions and card actions.
- WeChat/Douyin: built against the production API, passed the artifact gates, upload receipts obtained.
- Android: both signed APKs pass the certificate, signature-scheme, permission, production-resource and version gates; on a headless Android 14 emulator the build installed over 0.6.4 (`versionCode 6005`, `versionName 0.6.5`) and the signed release passed the install, debug-port-closed and background/foreground process checks. The deep interaction run of the debug build (including a live-model itinerary card) was **not** executed and is not claimed.
- **Verification is headless only**: no real-device, WeChat/Douyin devtools or visible-browser manual acceptance. Retry timing on weak or missing networks, the mini-program hosts’ network-restored events while backgrounded, and how the spinner renders in each host still need real devices.
- Check-in on a cloud outing still waits for the cloud (shared multi-person state) and only gained progress feedback; a message whose send was interrupted is still not resent automatically (the server has no idempotency key), keeping “check the send status, then retry”.

### Release assets

- Source tag: `v0.6.5`; the exact source commit is recorded as `sourceCommit` in `release-manifest.json`.
- Public release repository tag: `v0.6.5`.
- `release-manifest.json` and `SHA256SUMS` are attached to this Release.
- Release: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/tag/v0.6.5>
