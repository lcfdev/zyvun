# Zyvun（质匀播放器）

支持本地 / 局域网 / NAS 直连播放器，支持Emby / Jellyfin服务，支持Kodi NFO，兼容danmu_api弹幕协议，支持自定义搜索弹幕，不转码、不强制云刮削。

- **不全盘扫描**：只扫用户自己指定的目录，不申请「所有文件访问」、不偷偷翻整台设备，不对文件增删改
- **不上传用户数据**：片库、进度、配置都留在本机；应用完全本地运行，不经过作者的云
- **永久无广告、永久免费**
- **不开源**：写这版花了不少 AI 费用 🙂 源码先自己留着

- 包名 `localhost.zyvun`，TV版包名`localhost.zyvun.tv`，最低 Android 9.0
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

- **来源**：本地目录、Emby、Jellyfin、WebDAV、仅局域网 SMB
- **浏览**：海报墙 → 电影详情 / 剧集分集 → 播放
- **直连**：Media3 硬解优先，失败再 FFmpeg；本地 / HTTP 直链 / `smb://`
- **NFO**：Kodi 风格元数据与封面，无网也能当片库
- **弹幕**：自建 danmu_api（不是内置弹幕站账号）
- **其它**：拼音搜索、续播、片头片尾、倍速、字幕/音轨、画中画 / 悬浮窗

资源库里的 SMB / WebDAV 是文件管理器；媒体库里才按 NFO / 文件名扫成片库。

---

## 两端差异

- **手机端**：触控手势、底部导航、竖屏为主；适合随身看。
- **电视端**：焦点 / D-pad、侧栏导航、横屏布局；包名独立，可与手机端同机共存。

业务与播放栈基本同源，界面与交互按端裁剪。

---

## 怎么用（最短路径）

1. 设置里添加来源（本地选目录，或填 Emby / Jellyfin / SMB / WebDAV）。
2. 媒体库切到来源，等扫描出海报。
3. 点进影片播放。局域网 SMB 建议走 Wi‑Fi / 有线，避免蜂窝误下大文件。

---
## 开源鸣谢

###### 播放与多媒体

| 组件 | 版本 / 说明 | 许可 | 地址 |
|------|-------------|------|------|
| AndroidX Media3（ExoPlayer / UI） | 1.8.0 | Apache-2.0 | https://github.com/androidx/media |
| decoder_ffmpeg（Media3 官方 JNI 桥） | 自研模块，源自 androidx/media | Apache-2.0 | https://github.com/androidx/media |
| FFmpeg | 自编译软解内核（含 AV1），无 GPL 组件 | LGPL-2.1+ | https://ffmpeg.org |

硬解优先，失败再走 FFmpeg。FFmpeg 以静态链接编入 `libffmpegJNI.so`；App 主体通过动态加载该 so，可保持闭源。二次分发请保留 FFmpeg 的 LGPL 声明，并提供用户替换 / 重新链接该动态库的途径。

---

###### 网络、共享与图片

| 组件 | 版本 | 许可 | 地址 |
|------|------|------|------|
| OkHttp | 4.12.0 | Apache-2.0 | https://square.github.io/okhttp/ |
| Okio | OkHttp 依赖 | Apache-2.0 | https://square.github.io/okio/ |
| SMBJ | 0.15.0 | Apache-2.0 | https://github.com/hierynomus/smbj |
| SLF4J | SMBJ 日志依赖 | MIT | https://www.slf4j.org |
| Glide | 4.16.0 | BSD-2-Clause | https://github.com/bumptech/glide |
| org.json | 20240303 | JSON License | https://github.com/stleary/JSON-java |

---

###### 界面与系统库

| 组件 | 版本 | 许可 | 地址 |
|------|------|------|------|
| AndroidX AppCompat | 1.7.0 | Apache-2.0 | https://developer.android.com/jetpack/androidx |
| AndroidX Activity | 1.9.2 | Apache-2.0 | https://developer.android.com/jetpack/androidx |
| AndroidX RecyclerView | 1.3.2 | Apache-2.0 | https://developer.android.com/jetpack/androidx |
| AndroidX DocumentFile | 1.0.1 | Apache-2.0 | https://developer.android.com/jetpack/androidx |
| Kotlin Standard Library | 2.1.21 | Apache-2.0 | https://kotlinlang.org |

---

###### 弹幕

| 组件 | 版本 / 说明 | 许可 | 地址 |
|------|-------------|------|------|
| DanmakuFlameMaster | 0.9.25，原 ctiao，现由 Bilibili 维护 | Apache-2.0 | https://github.com/bilibili/DanmakuFlameMaster |

---


## 交流与支持

需要反馈、求片库折腾经验，进 **QQ 群：217032088**（极速交流）。

---

## 法律与免责
Zyvun 是独立播放与浏览客户端，与 Emby、Jellyfin、Kodi、Bilibili 无官方从属关系。商标归各权利人。

本应用仅提供本地与局域网媒体播放能力，不提供任何影视内容。

请仅连接你本人有权访问的媒体服务器与文件。

弹幕内容来自你自行配置的服务，与本应用作者无关。

应用按「现状」提供，不对播放兼容性、数据丢失作额外担保。



