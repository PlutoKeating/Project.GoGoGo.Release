## 中文

### 更新
- 定位等待统一为 3 秒；卡片操作和首条消息立即在本机显示反馈。
- 消息、会话历史与私人档案优先从本地读取，再与云端同步；私人档案退出登录后仍保留，按账户隔离。
- 欢迎卡片不建立空会话；首次点击或发送后才开启会话，切换子页、标签和前后台保留当前会话状态。
- 宣传站更新当前服务状态，新增下载与版本动态页面，实时从官方 GitHub Release 获取版本、双语说明和附件。

### 平台与资源
- Web 和 API 通过 Cloudflare 提供服务。微信体验版及抖音预览版已上传，运行版本均为 0.1.19；不代表已提交平台正式审核。
- 本次为正式的数据发布，提供发行清单和 SHA256 校验文件。**本次没有可安装的 Android/iOS APP 安装包**；原生工程、签名及安装分发尚未完成。请先使用 Web 或小程序内测入口。
- 不需要用户手动迁移数据。请勿通过清除应用数据来更新版本，否则本地副本会被设备删除。

### 验证与限制
- 后端 130 项测试通过；本地优先、会话状态、账户隔离、各端构建与小程序产物检查通过。
- 下载页已验证动态版本刷新、空附件、限流、无正式发布、恶意 HTML/链接与移动端布局。
- 尚未取得本次微信／抖音真机验收结果；GitHub 请求受网络和匿名限流影响。未知结果的消息发送不自动重放，避免重复发送。

## English

### Changes
- Location waits now share a three-second deadline. Card actions and first messages show immediate local feedback.
- Messages, conversation history and private profiles load locally first, then synchronize with the cloud. Private profiles remain on the device after sign-out and are isolated by account.
- Welcome cards do not create empty conversations. A first user action starts a conversation; navigation and background/foreground transitions retain the active session.
- The marketing website now reflects the current service status and includes a download center that fetches current versions, bilingual notes and assets from the official GitHub Release API.

### Platforms and assets
- Web and API are served through Cloudflare. WeChat experience and Douyin preview builds have been uploaded, both at runtime version 0.1.19. This does not mean public mini-program review or store release.
- This full GitHub Release distributes release metadata and SHA256 checksums. **No installable Android/iOS app is included.** Native projects, signing and installation distribution are not complete. Use Web or the mini-program testing channels for now.
- No manual data migration is required. Clearing application data also removes device-local copies; do not use it as an update procedure.

### Validation and limitations
- All 130 backend tests passed, alongside local-first behavior, session retention, account isolation, cross-platform builds and mini-program artifact checks.
- The download center was tested for dynamic updates, missing assets, rate limits, missing releases, unsafe HTML/URLs and mobile layout.
- Physical-device acceptance for these mini-program builds remains pending. GitHub requests depend on network access and anonymous rate limits. Sends with unknown outcomes are not automatically replayed, to avoid duplicates.
