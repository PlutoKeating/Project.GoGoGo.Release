# 走不走 v0.7.0 / GoGoGo v0.7.0

## 中文

### 本次更新

- **行程一站一站地出现**：狗狗GO 先替你拍板一条路线，每选定一个地方，这一站马上出现在行程卡上，不用等整条路线排完。还在安排的部分直接用样子表示，不再写提示文字：时间在闪动，说明交通还在核对；站点之间有一段在走动的虚线，交通算好后变成实线并显示用时；翻页点旁边多一个空心点，说明备选还在路上；最后一张带小狗的虚线卡，说明还在找下一站。
- **生成途中就能看、能改**：站点一出现就能翻到背面，看照片、评分、人均、营业时间、地址和特色，也可以直接去小红书、大众点评、抖音看评价。换一家、锁定、删掉都会立即生效，狗狗GO 接着排的时候会按你的改动来，不会改回去。
- **每站一个备选**：每一站准备一个顺路的替补，左右滑或点「换一家」就能换。需要二选一的地方（比如天气说不准时室内和户外各一个），狗狗GO 会在主线定下后再加上可以秒切的平行路线。
- **断网、锁屏、切后台都不会丢**：回复在服务器上继续生成，回到应用会自动接上；重新打开一段还在生成的对话，也会从头放一遍再接着往下走。停止键会真正停下这次回复。
- **更懂你此刻的处境**：天气（未来 24 小时）、你所在的街道和商圈、今天是不是节假日或调休、周边 3 公里的餐饮、商业街、咖啡、公园和影院，都会在后台提前准备好，发消息时直接用上，回复更快。手机位置变了（超过约 300 米）会自动跟着更新；你手动选的出发地点不会被覆盖。
- **对话里少了一行行的说明**：进度条不再写字，只看小狗的动作——在闻就是在找地方，在跑就是在排路线，停着就是在想；一个小圆点代表走完的一步。行程卡出现后进度条就让位，回复结束后不留痕迹。

### 平台

- **Web H5**：<https://gogogo.plutokeating.beer/>
- **Android**：签名 Universal APK 与 `arm64-v8a` APK，`versionCode 7000`，10,086,555 bytes，可覆盖安装 0.6.14。两个 APK 当前字节完全相同，因为本版本没有 native `.so` 负载。已安装 0.6.13 及以上版本的用户可在「我的 → 应用版本与更新」里应用内升级。
  - Universal：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.7.0/GoGoGo-0.7.0-android-universal.apk>，SHA-256 `eafd8bac1acae734e733413da1128f95d2eae2509c4fd71654e7f2c1a2af7f22`
  - arm64-v8a：<https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.7.0/GoGoGo-0.7.0-android-arm64-v8a.apk>，SHA-256 `eafd8bac1acae734e733413da1128f95d2eae2509c4fd71654e7f2c1a2af7f22`
- **微信小程序**：`0.7.0` 开发版本已上传（产物 SHA-256 `8b9d26b8…`），依赖已开启的体验内测自动更新；尚未提交审核，不是面向公众的正式上线。
- **抖音小程序**：`0.7.0` 预览版已上传（产物 SHA-256 `1e7b4396…`，预览短链 <https://t.zijieimg.com/i4e8EaRQ/>，平台未返回到期时间）；尚未提交审核，不是面向公众的正式上线。
- **iOS**：仍缺少 Apple 分发签名配置，本版本没有 IPA。

### 兼容性与迁移

- 新增接口：`GET /api/conversations/:id/messages/resume`（断线后接回）、`POST /api/conversations/:id/cancel`（停止回复）、`POST /api/conversations/:id/canvas`（生成途中同步卡片改动）；WebSocket 首条消息可以是 `{"resume": <seq>}`。新流事件 `itinerary-patch`，事件带 `seq`。客户端在发送时声明 `features` 才会用到新行为；没有声明的旧版客户端照常收到整张行程卡，不受影响。
- 新的画布工具 `pin_stop`；`read_context` 变为可选。`Stop.pending`、`Plan.open`、`returnAnchor.requestedTime/requestedMode` 为新增可选字段。
- 没有数据库迁移。每段对话的服务端存储新增回复事件日志（只保留最近两轮），每个用户新增一份位置／天气／日历快照，删除数据时一并清除。
- 本机私人档案、会话与行程的存储格式不变；升级不需要清理缓存或重新登录。

### 验证范围与已知限制

- 后端 62 个测试文件 / 383 项用例通过，新增覆盖：逐站补丁的计算与应用、待补标记、每站一个备选、事件日志回放、发消息拼上下文时不发任何网络请求、上下文快照只刷新过期部分、`pin_stop` 端到端逐站下发并定稿。
- 线上实测（正式模型）：一轮“先吃饭再去公园”的请求中，两个站点依次出现（交通先标为待补，随后补齐），首张卡片约 14 秒；断线续传、取消与生成途中同步接口在线上可用。
- 浏览器检查：新增 `check:progressive-itinerary`（无文字进度条、首站的待补样子与末尾找站卡、生成中看卡背、断线后续传并定稿、跟随新站、停止键取消），以及对话、行程页、本地优先、组局、导航驾驶舱等 14 项既有检查。`h5-canonical` 在登录步骤失败，此前版本同样失败，与本版本无关。
- Android：双签名 APK 通过证书、签名形态、权限、正式资源与版本门禁；在无头 Android 14 模拟器上覆盖安装公开 0.6.14，正式签名包通过安装、调试端口关闭、前后台切换进程保持检查。**未执行**调试包的深度交互实测。
- 周边地点（来自高德）按服务条款只在服务器内存保留 5 分钟；打开应用超过 5 分钟才发消息时，这一轮由狗狗GO 现场搜索地点。
- 小程序只在回到前台时更新位置（持续定位需要额外的平台隐私声明）；网页在位置变化时自动更新。
- 站点上屏的快慢取决于所用模型是否逐段返回工具参数；不支持时，站点在每一站排好后出现，流程不变。
- 小程序与 Android 的真机验收尚未进行。

### 发布资源

- 源码标签：`v0.7.0`；源码提交以 `release-manifest.json` 的 `sourceCommit` 为准。
- 公开发行仓库标签：`v0.7.0`。
- 国内下载镜像：<https://gogogo.williamhvollita.dpdns.org/releases/download/v0.7.0/GoGoGo-0.7.0-android-universal.apk>

## English

### What's new

- **Your outing appears stop by stop**: 狗狗GO settles one route for you and puts each place on the itinerary card the moment it picks it, instead of making you wait for the whole route. What is still being worked out shows as a shape, not as words: a shimmering time means the trip there is still being checked; a moving dashed line between stops turns solid with the travel time once it is known; a hollow dot next to the page dots means the backup is on its way; a dashed card with the puppy at the end means the next stop is still being found.
- **Look and change while it works**: flip any stop to its back as soon as it appears for photos, rating, price, opening hours, address and highlights, or jump to Xiaohongshu, Dianping or Douyin for reviews. Swapping, locking and removing take effect at once, and 狗狗GO builds on your change instead of undoing it.
- **One backup per stop**: every stop comes with one nearby alternative — swipe or tap "Swap". Where two options are equally good (say, indoor or outdoor when the weather is unsure), 狗狗GO adds a parallel option you can switch instantly, after the main route is set.
- **Losing the connection loses nothing**: the reply keeps being written on the server while your network drops, the screen locks or the app is in the background, and picks up again when you return; reopening a conversation that is still being answered replays it and carries on. The stop button now really stops the reply.
- **Knows your moment better**: the next 24 hours of weather, your street and neighbourhood, whether today is a public holiday or a make-up workday, and nearby restaurants, shopping streets, cafés, parks and cinemas within 3 km are prepared in the background and used the moment you send — replies come faster. When your phone moves more than about 300 m this updates by itself; a starting point you chose yourself is never replaced.
- **Fewer status lines in the chat**: the progress bar no longer has text — the puppy sniffs while looking for places, runs while laying out the route and waits while thinking, with one dot per step taken. It gives way once the itinerary card appears and leaves nothing behind when the reply ends.

### Platforms

- **Web H5**: <https://gogogo.plutokeating.beer/>
- **Android**: signed universal and `arm64-v8a` APKs, `versionCode 7000`, 10,086,555 bytes, installs over 0.6.14. The two APKs are byte-identical for now because this release has no native `.so` payload. Users on 0.6.13 or later can update inside the app from "Me → App version & updates".
  - Universal: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.7.0/GoGoGo-0.7.0-android-universal.apk>, SHA-256 `eafd8bac1acae734e733413da1128f95d2eae2509c4fd71654e7f2c1a2af7f22`
  - arm64-v8a: <https://github.com/PlutoKeating/Project.GoGoGo.Release/releases/download/v0.7.0/GoGoGo-0.7.0-android-arm64-v8a.apk>, SHA-256 `eafd8bac1acae734e733413da1128f95d2eae2509c4fd71654e7f2c1a2af7f22`
- **WeChat Mini Program**: `0.7.0` development version uploaded (artifact SHA-256 `8b9d26b8…`), relying on the enabled automatic experience-version update; not submitted for review and not a public launch.
- **Douyin Mini Program**: `0.7.0` preview uploaded (artifact SHA-256 `1e7b4396…`, preview link <https://t.zijieimg.com/i4e8EaRQ/>, no expiry returned by the platform); not submitted for review and not a public launch.
- **iOS**: Apple distribution signing is still missing; no IPA in this release.

### Compatibility and migration

- New endpoints: `GET /api/conversations/:id/messages/resume` (re-attach after a drop), `POST /api/conversations/:id/cancel` (stop a reply), `POST /api/conversations/:id/canvas` (sync card edits made while a reply runs); a WebSocket's first message may be `{"resume": <seq>}`. New stream event `itinerary-patch`; events carry `seq`. Clients opt in through `features` when sending; older clients that do not keep receiving whole itinerary cards.
- New canvas tool `pin_stop`; `read_context` is now optional. `Stop.pending`, `Plan.open` and `returnAnchor.requestedTime/requestedMode` are new optional fields.
- No database migration. Each conversation's server storage gains a reply event log (last two replies only), and each user a place/weather/calendar snapshot; both are removed with the user's data.
- Local private profiles, conversations and trips keep their storage format; no cache clearing or new sign-in is needed.

### Verification and known limitations

- Backend: 62 test files / 383 cases pass, newly covering node patch computation and application, pending marks, one backup per stop, event-log replay, sending a message without any network request for the context, refreshing only the stale parts of the context snapshot, and `pin_stop` end to end.
- Live test with the production model: for "lunch, then a walk in a park", the two stops appeared one after the other (legs pending, then settled), first card after about 14 seconds; the resume, cancel and mid-reply sync endpoints respond in production.
- Browser checks: new `check:progressive-itinerary` (wordless live bar, pending shapes and the trailing search card, card back mid-reply, resume after a drop and settled card, following new stops, stop cancels) plus 14 existing checks (conversation, itinerary page, local-first, group outing, navigation cockpit and more). `h5-canonical` fails at its sign-in step, as it did before this release.
- Android: both signed APKs pass the certificate, signature scheme, permission, production-asset and version gates; on a headless Android 14 emulator the build installed over the public 0.6.14 and the signed release passed install, WebView-debug-port-closed and background/foreground checks. The debug-build deep interaction run was **not** executed.
- Nearby places (from AMap) are kept in server memory for only five minutes under its terms; when a message is sent more than five minutes after opening the app, 狗狗GO searches for places on the spot that turn.
- Mini programs update the location only when returning to the foreground (continuous location needs extra platform privacy declarations); the web updates when the location changes.
- How early stops appear depends on whether the model streams tool arguments; if it does not, each stop appears once it is laid out, and nothing else changes.
- Mini-program and Android physical-device acceptance has not been done yet.

### Release assets

- Source tag: `v0.7.0`; the source commit is `sourceCommit` in `release-manifest.json`.
- Public release repository tag: `v0.7.0`.
- Mirror download (faster in mainland China): <https://gogogo.williamhvollita.dpdns.org/releases/download/v0.7.0/GoGoGo-0.7.0-android-universal.apk>
