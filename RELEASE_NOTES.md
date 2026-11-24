# 走不走 v0.6.2 / GoGoGo v0.6.2

## 中文

### 这次更新解决了什么

- **忌口真正记得住**：固定 8 项预设、自定义忌口与对话中口头补充的忌口统一进入会话级 `OutingCanvasDoc` 记忆，跨轮追问、零工具回合与运行中插话均不丢失；也可以在「我的 → 饮食与偏好」中随时管理，游客同样本机持久保存，登录后跨设备同步。清真保持严格白名单，其他忌口硬性剔除冲突专营店，普通综合餐厅提示向厨房确认。
- **指定地点周边搜得更准**：新增 `resolve_place` 空间锚点工具，支持「我要去的这个地方周围 1.5 公里」「深圳湾公园周围 800 米」等指定地标/行程站点/当前目的地检索，范围 `100m–50km`，严格执行球面距离裁剪并标明实际圆心与半径；地标解析失败会明确说明，绝不悄悄拿当前 GPS 冒充目标地点。
- **问怎么用，不再乱排路线**：产品功能与界面咨询由狗狗GO 直接给出与真实界面一致的操作指引；「放到行程页面」在多个候选且未指明店名时会先让你确认，不再盲选第一家。
- **每站都能一键换一家**：行程卡与行程页自动配齐同细分类别、同饮食约束、营业时段兼容且顺路的备选；点按「↻ 换一家」即可 `0ms` 循环切换，站点时刻、衔接交通与预算同步更新，历史卡片与流式更新均不会回滚。
- **群拍板真正融合每个人的想法**：入局与局内想法更新改为增量画布融合，保留已打卡与兼容已锁定站点，支持具体店名、同餐段分歧平行分支与饭后新阶段（如唱K）；`confirmed` 盖章后出发前仍可微调路线且不退回投票，跨商圈/弹性预算不再误报 `422`。想法中的忌口只进入匿名约束，不公开展示个人归属，未经同意绝不写入健康字段。
- **行程页更清爽**：默认阅读态去除内部工程术语与重复价格评分，排序/锁定/删除及段间交通切换收进「调整行程」；单点目的地可「+ 顺路加下一站」直接串成多站，空行程页可搜首站或使用多站模板直接开排。

### 兼容性与迁移

- Web H5、Android APP、微信小程序、抖音小程序共用同一套业务代码与 `Plan` v2 行程画布协议。
- 生产 PostgreSQL 已备份并应用迁移 `017_group_idea_constraints.sql`：升级 `update_member_idea`（支持私密忌口合并，保留 `healthConsent`）与 `reconcile_voting_session`（`confirmed` 状态原子更新方案且保留盖章/投票）。
- 旧版 `OutingCanvasDoc` 快照自动补齐会话忌口数组，保持严格 JSON 兼容。

### 平台与资源

- Web H5：<https://gogogo.plutokeating.beer/>
- Android：签名 Universal APK 与 arm64-v8a APK（`versionCode 6002`，沿用官方发布证书，支持覆盖安装）。
- 微信 / 抖音：`0.6.2` 体验版 / 预览版已上传；小程序仍需按平台规则体验，真机验收以平台回执与实机为准。
- iOS：仍缺少 Apple 分发签名配置，本版本无 IPA。

### 验证范围与已知限制

- 后端 56 个测试文件 / 336 项用例通过；前后端 TypeScript 0 错误。
- Web H5 Canonical Playwright 门禁通过：候选循环与前后台持久化、历史卡片定向追问、行程工作台 ↔ 3D 驾驶舱、群拍板海报/深链/封盘/平权共创、320/390 声明式卡片零溢出、定位选择、账号登录、本地优先与恢复。
- Android 正式签名包通过静态证书/权限/正式 H5 资源门禁，并在本地 Android 14 模拟器完成安装启动与 WebView 深度交互验收；实体真机户外路测与微信/抖音真机验收仍需继续补充。
- 地图、营业时间与路线依赖真实上游，不能视为实时交通、空位或营业承诺；本版本不接入付费菜单级配料库。

---

## English

### What’s new

- **Dietary restrictions that actually persist**: all 8 presets, custom restrictions, and spoken/steered updates now live in session-level `OutingCanvasDoc` memory across follow-ups, zero-tool turns, and mid-run steering. Guests can manage local-first preferences in **Me → Diet & preferences**; signed-in users sync across devices. Halal remains a strict whitelist; other restrictions hard-block conflicting specialty venues and remind you to confirm ingredients with kitchen staff at general restaurants.
- **Accurate search around a chosen place**: the new `resolve_place` spatial anchor tool supports searches such as “within 1.5 km of where I’m going” or “within 800 m of Shenzhen Bay Park”, from **100 m to 50 km**, with strict Haversine filtering and an explicit resolved center/radius. Unresolved landmarks return an honest empty result instead of silently falling back to your GPS.
- **Usage questions no longer invent routes**: 狗狗GO answers product/UI questions with instructions that match the real interface, and `open_in_trip_page` asks which venue you mean instead of blindly picking the first candidate.
- **One-tap “Swap” on every stop**: itinerary cards and the trip workspace now carry role-matched, diet-compatible, open-hours-aware nearby backups. Tap **↻ Swap** to cycle instantly with updated legs, clocks, and budget—stable across streaming updates and historical cards.
- **Group outings that fuse everyone’s ideas**: joins and in-room idea updates incrementally enrich `Plan` v2, preserving checked-in and compatible locked stops, named venues, same-slot parallel options, and new stages such as karaoke. Pre-departure edits in `confirmed` keep the seal and votes intact, and cross-district/elastic-budget plans no longer trigger false `422` errors. Dietary terms become anonymous constraints only; health data is never stored without consent.
- **A calmer trip workspace**: a clean reading mode removes jargon and repeated price/rating blocks; reorder/lock/delete and transit-mode controls live behind **Edit trip**. A single destination can grow into a multi-stop plan, and an empty trip tab can start from a searched first stop or a ready-made template.

### Compatibility & migration

- Web H5, Android, WeChat Mini Program, and Douyin Mini Program share the same business code and `Plan` v2 canvas protocol.
- Production PostgreSQL was backed up and migrated with `017_group_idea_constraints.sql` (private diet merging with `healthConsent` preserved, and `confirmed`-preserving plan reconciliation).
- Legacy `OutingCanvasDoc` snapshots are normalized with default session-constraint arrays while keeping strict JSON compatibility.

### Platforms & resources

- Web H5: <https://gogogo.plutokeating.beer/>
- Android: signed Universal and arm64-v8a APKs (`versionCode 6002`, official release certificate, upgrade-safe).
- WeChat / Douyin: `0.6.2` experience/preview builds uploaded; on-device acceptance remains subject to platform receipts and real-device checks.
- iOS: no IPA in this release because Apple distribution signing is not configured.

### Verification & known limits

- 56 backend test files / 336 tests passed; zero TypeScript errors in backend and frontend.
- Web H5 Canonical Playwright gates passed for candidate cycling and foreground/background persistence, historical-card targeting, workspace ↔ 3D cockpit, group poster/deep-link/seal/equal co-editing, 320/390px UI blocks without overflow, location picking, account login, and local-first restore.
- Signed Android APKs passed certificate/permission/production-H5 artifact gates and installation/startup plus deep WebView interaction checks on a local Android 14 emulator. Physical outdoor device testing and WeChat/Douyin real-device acceptance remain follow-up work.
- Maps, opening hours, and routes depend on live upstream providers and are not guarantees of real-time traffic, availability, or opening status. No paid menu-level ingredient database is included.
