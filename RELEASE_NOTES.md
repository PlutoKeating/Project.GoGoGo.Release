## 中文

- **安卓实机逐屏视觉与交互对齐精修（100% 复刻 H5 品质）**：基于广州番禺万达广场真实商圈坐标全链路逐屏对照修复：
  - **消除状态栏双倍留白与手势条贴边**：`MainActivity` 显式统一沉浸式边到边窗口模式并校准底部导航栏安全区高度，消除 `targetSdk 34` 下的状态栏多余留白及底部标签贴触系统手势条问题。
  - **修复首启隐私合规弹窗与中英文排版**：补齐门禁层按钮样式与正文弹性滚动区，右上角语言切换胶囊紧凑对齐，中文与英文模式下「同意并进入走不走」均完整固定在视口内。
  - **修复应用内实时导航与行程卡片胶囊排版**：修复「实时跟随视角已锁定」与「语音/驾车辅助」并排比例，修复「行程」地图抽屉模式切换（「公交地铁 / 打车预估」单行显示）、站点锚点胶囊同行排列，以及站点卡内「小红书看实拍 / 抖音看探店 / 大众点评 / 电话商家」与「现场核验」四项紧凑同行胶囊排版。
  - **修复地图标记层级穿透、首屏渲染与 5:4 分享海报长标题自适应**：隔离地图抽屉层叠上下文防止站点序号浮在顶栏或弹层之上，首次进入「行程」即刻绘制站点标记与轨迹并配备暖米色坐标网格底纹；修复长地名在 5:4 动态路线海报中的自适应字号与边界留白；顶部绿色状态提示条支持手动关闭与 4.5 秒自动收起。
- **国产系统安装兼容（含 vivo OriginOS）与核心原生能力**：保留规范签发的纯 `v1（CERT JAR）+ v2` 签名（显式关闭 `v3/v4`）与 `targetSdkVersion 34`，杜绝 vivo OriginOS 等系统预检误报「缺乏开发者证书」；内置无 GMS 3 秒多源定位、传感器融合（`TYPE_ROTATION_VECTOR`）应用内实时跟随导航、`Directory.Data` 原生私有目录档案持久化、原生鉴权 WebSocket、Custom Tabs + App Links 登录、5:4 海报存相册与系统面板分享及应用内版本更新卡片。
- **升级与多端可用性**：提供签名的 `GoGoGo-0.3.2-android-universal.apk`（全架构通用）与 `GoGoGo-0.3.2-android-arm64-v8a.apk`（约 `9.4 MB`，Android 7.0+），沿用同一官方发布证书（SHA-256 `FA:49:93:27:...`），已安装 `0.1.20`、`0.2.0` 或 `0.3.1` 的用户可直接覆盖升级。Web 版已同步上线；微信体验版与抖音预览版已同步更新至 `0.3.2`（内测阶段）；iOS 暂无可下载的 IPA。
- **验证范围与限制**：已完成广州番禺万达全链路逐屏 Eyeball 截图对照、二进制签名门禁、Android 14 无窗口模拟器 WebView CDP 深度 E2E（含中英文首启弹窗与导航双按钮几何断言）与正式包安全/前后台门禁、Web 与官网部署校验及双小程序上传；多品牌实体手机真机路测持续进行中。

## English

- **Screen-by-Screen Android Visual & Interactive Polish (100% H5 Parity)**: Refined via full end-to-end side-by-side comparison around Panyu Wanda Plaza, Guangzhou:
  - **System-Bar & Gesture-Bar Precision**: Enforced explicit edge-to-edge window geometry in `MainActivity` and calibrated bottom-nav safe-area height, eliminating double top status-bar padding under `targetSdk 34` and bottom gesture-pill overlap.
  - **First-Launch Privacy Consent Gate**: Fixed Taro button styling and added an elastic scrollable body inside `.privacy-gate-shell`, keeping the language toggle compact and ensuring "Agree and enter" fits cleanly within the viewport in both Chinese and English.
  - **In-App Live Navigation & Outing Chip Layout**: Restored proportional side-by-side layout for "Live follow locked" + "Voice / car" in live navigation, kept Walk / Bike / Transit / Taxi pills single-line, aligned stop-anchor chips horizontally, and rendered social discovery (Xiaohongshu / Douyin / Dianping) and on-site verification buttons as compact inline pills.
  - **Map Stacking Isolation, Instant Pin Render & 5:4 Share Poster Fit**: Isolated Leaflet stacking contexts so stop pins never float above the top bar or modal backdrops, enabled immediate pin/polyline rendering on initial Trip mount over a warm architectural grid fallback, added adaptive font-fitting for long location titles on the 5:4 share poster, and made status notice banners dismissible with 4.5s auto-clear.
- **Domestic OEM Installer Compatibility (vivo OriginOS) & Native Core**: Retains canonical `apksigner` `v1 (CERT JAR) + v2` signing (`v3/v4` disabled) with `targetSdkVersion 34`, non-GMS 3-second positioning, hardware sensor-fused (`TYPE_ROTATION_VECTOR`) in-app live navigation, `Directory.Data` private storage, native authenticated WebSocket streaming, Custom Tabs + App Links sign-in, gallery save & native image share, and in-app update checking.
- **Compatibility & Platform Availability**: Ships signed `GoGoGo-0.3.2-android-universal.apk` and `GoGoGo-0.3.2-android-arm64-v8a.apk` (`~9.4 MB`, Android 7.0+), signed with the same official release certificate (`FA:49:93:27:...`) for seamless in-place upgrades over `0.1.20`, `0.2.0`, and `0.3.1`. The Web app is live; WeChat `0.3.2` experience and Douyin `0.3.2` preview builds are uploaded for internal testing; no downloadable iOS IPA is included in this release.
- **Verification & Limitations**: Verified via full Panyu Wanda screen-by-screen eyeball comparison, binary signature gates, headless Android 14 emulator WebView CDP end-to-end + layout geometry assertions, signed release security/lifecycle gates, Cloudflare Pages deployment, and WeChat/Douyin uploads. Physical multi-OEM street testing remains ongoing.
