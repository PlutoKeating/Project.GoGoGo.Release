# 走不走 v0.6.3 / GoGoGo v0.6.3

## 中文

### 本次修复

- **换店后不再残留旧店叙述**：「换一家」与备选抽屉统一重算站点阶段、标签、理由、提示、标题、时刻、交通和预算；后续流式合并及本地编辑重放也走同一逻辑，不会把旧店描述恢复。
- **预算变化明确可见**：换店导致原有人均预算带被抬高时，卡片会直接提示调整前后的区间，不再静默涨价。
- **生成中避免两页不一致**：流式生成未完成时暂时禁止换店，完成后「拍板」与「行程」展示同一方案；正常连续 A→B→C→A 轮换不受路由核验等待影响。
- **正常地点标题不误清洗**：仅清除与被替换门店明确绑定的专属叙述，保留「周五五山出发」这类普通地点标题。

### 平台与兼容性

- Web H5、Android、微信小程序、抖音小程序共用同一套业务代码与 `Plan` v2 协议；本次无新增数据库迁移，生产 Worker 沿用 `v0.6.2` 后端。
- Web H5：<https://gogogo.plutokeating.beer/>
- Android：签名 Universal APK 与 arm64-v8a APK，`versionCode 6003`，支持覆盖安装。
- 微信 / 抖音：`0.6.3` 体验版 / 预览版已上传，抖音预览短链 <https://t.zijieimg.com/i4JmrraV/>。
- iOS：仍缺少 Apple 分发签名配置，本版本无 IPA。
- `v0.6.2` 因独立新人验收发现上述换店一致性问题而被本版本取代，请使用 `v0.6.3`。

### 验证范围与已知限制

- 后端 56 个测试文件 / 339 项用例通过；前后端 TypeScript 0 错误；H5 Canonical 与群组等真实浏览器门禁通过。
- Android 正式签名双 APK 通过静态证书、权限、正式资源及版本门禁，并在 Android 14 模拟器完成覆盖安装、首启隐私、首页、返回/前后台保持与崩溃日志检查，验毕关闭模拟器。
- 独立新人视角对生产 H5 的换店叙述、预算提示、流式门禁及 320px 溢出进行最终复查，证据保存在源码仓库 QA 报告中。
- 微信/抖音上传回执不等于真机验收；实体手机户外路测与小程序真机验收仍需继续补充。地图、营业时间与路线依赖真实上游，不构成实时交通、空位或营业承诺。

---

## English

### Fixes

- **No stale venue narrative after swapping**: both one-tap Swap and the alternatives drawer now reset the stop phase, tags, reason, tips, title, clocks, legs, and budget together. Streaming merges and replayed local edits use the same path, so descriptions of the replaced venue cannot return.
- **Visible budget changes**: when a replacement raises the original per-person budget band, the card explicitly shows the old and new ranges instead of silently increasing the estimate.
- **Consistent Decide and Trip surfaces during generation**: swapping is gated while the itinerary is streaming; once complete, both surfaces show the same plan. Ordinary consecutive A→B→C→A cycling is not blocked by route verification.
- **Normal place titles preserved**: cleanup targets venue-specific narrative tied to the replaced stop and leaves ordinary titles such as “Friday, starting from Wushan” intact.

### Platforms & compatibility

- Web H5, Android, WeChat Mini Program, and Douyin Mini Program share the same business code and `Plan` v2 protocol. No new database migration is required; production continues to use the `v0.6.2` Worker backend.
- Web H5: <https://gogogo.plutokeating.beer/>
- Android: signed Universal and arm64-v8a APKs, `versionCode 6003`, upgrade-safe.
- WeChat / Douyin: `0.6.3` experience/preview builds uploaded. Douyin preview: <https://t.zijieimg.com/i4JmrraV/>.
- iOS: no IPA because Apple distribution signing is not configured.
- `v0.6.2` is superseded by this release following independent first-time QA findings around swap consistency. Please use `v0.6.3`.

### Verification & known limits

- 56 backend test files / 339 tests passed; zero TypeScript errors in backend and frontend; H5 Canonical and group real-browser gates passed.
- Signed Android APKs passed certificate, permission, production-resource, and version gates. Override installation, first-run privacy, home screen, back/foreground-background retention, and fatal-log checks were exercised on an Android 14 emulator, which was shut down afterward.
- Independent first-time QA rechecked production H5 swap narratives, budget warnings, streaming gating, and 320px overflow; evidence is retained in the source repository QA report.
- Upload receipts are not real-device acceptance. Physical outdoor testing and WeChat/Douyin device acceptance remain follow-up work. Maps, opening hours, and routes depend on live providers and are not guarantees of traffic, availability, or opening status.
