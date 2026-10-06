# Zyvun（质匀播放器）

本地 / 局域网 / NAS 直连播放器。手机与平板同一套界面浏览本机视频、Emby / Jellyfin、SMB，不转码、不强制云刮削。

- **不全盘扫描**：只扫用户自己指定的目录，不申请「所有文件访问」、不偷偷翻整台设备
- **不上传用户数据**：片库、进度、配置都留在本机；应用完全本地运行，不经过作者的云
- **永久无广告、永久免费**
- **不开源**：写这版花了不少 AI 费用 🙂 源码先自己留着

- 包名 `localhost.zyvun`，最低 Android 7.0，目标 SDK 35
- 原生 Java 17，不使用跨平台框架

---

## 为什么自己写

家里片库是本地 NFO + 局域网 SMB，偶尔还要连 Emby / Jellyfin，看片习惯要弹幕。市面上转了一圈，始终对不上：

- 能读本地 `.nfo`、海报墙像样的，往往没有弹幕
- 能播本地、能进 SMB 的，通常既没有弹幕，也不接 Emby / Jellyfin
- 能接媒体服务器或能弹幕的，又不太把 Kodi 那套本地资料当一等公民

没有一个播放器同时覆盖：**本地 NFO、SMB、Emby / Jellyfin、弹幕**。与其继续凑合，不如按自己的家庭影视习惯做一款。

正好现在写代码可以大量借助 AI。空闲时间里由模型完成大约 **90%** 的实现，作者负责需求、取舍，以及模型单独做不好的联调和修正。

---

## 能做什么

- **媒体库 / 资源库 / 设置**：海报墙浏览，多来源管理
- **来源**：多个本地目录、Emby、Jellyfin、仅 Wi‑Fi 下列出的 SMB
- **直连播放**：Media3 + 硬解优先，失败再 FFmpeg；本地 / HTTP 直链 / `smb://`
- **NFO 当刮削**：Kodi 风格元数据与封面，无网也能当片库
- **弹幕**：自建 danmu_api，非内置弹幕站账号
- **拼音搜索**、续播、片头片尾、画中画 / 悬浮窗

浏览习惯统一：海报 → 电影详情 / 剧集分集 → 播放。资源库里的 SMB 是目录浏览器，媒体库里的 SMB 才按片库扫描。

---

## 技术栈（精简）

| 层 | 选型 |
| --- | --- |
| 界面 | AppCompat、RecyclerView、SAF、WindowInsets、Leanback 可选 |
| 播放 | Media3 ExoPlayer 1.8、NextLib/FFmpeg、自研 PlaybackEngine |
| 网络 | OkHttp、Emby/Jellyfin REST、SMBJ |
| 其它 | Glide、DanmakuFlameMaster、org.json、本地 JSON 缓存 |

ABI 仅 `armeabi-v7a` / `arm64-v8a`。允许明文 HTTP，方便局域网服务。

---

## 开源依赖（鸣谢）

Media3、NextLib、FFmpeg、OkHttp、SMBJ、Glide、AndroidX、DanmakuFlameMaster、danmu_api。协议兼容 Emby / Jellyfin API 与 Kodi NFO。

Zyvun 与上述产品无官方从属关系。请仅连接你有权访问的媒体，二次分发请遵守各组件许可（含 FFmpeg 的 LGPL/GPL）。

---

## 交流与支持

需要反馈、求片库折腾经验，进 **QQ 群：187573029**（极速交流）。

