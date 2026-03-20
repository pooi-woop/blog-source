---
title: yt-dlp使用教程
tags: [视频下载, yt-dlp]
cover: img/photo/85940e964bf0dff3705bf4a3225b36aa35174354.jpg
banner: img/photo/85940e964bf0dff3705bf4a3225b36aa35174354.jpg
---
 # yt-dlp 使用教程

yt-dlp 是一个功能强大的命令行视频/音频下载工具，支持 YouTube、Bilibili、抖音、小红书等 **1800+ 个网站**。它是 youtube-dl 的活跃分支，更新更频繁，功能更强大。

---

## 一、安装与准备

### 1. 下载 yt-dlp

**Windows 用户：**
- 访问 GitHub 发布页：https://github.com/yt-dlp/yt-dlp/releases
- 下载 `yt-dlp.exe`（或 `yt-dlp_x86.exe` 用于 32 位系统）

**macOS/Linux 用户：**
```bash
# 使用 pip 安装（推荐）
pip install yt-dlp

# 或使用 Homebrew (macOS)
brew install yt-dlp
```

### 2. 安装 FFmpeg（必需）

yt-dlp 需要 FFmpeg 来合并音视频、转换格式：
- 官网下载：https://ffmpeg.org/download.html
- **Windows 安装技巧**：将 `yt-dlp.exe` 放入 FFmpeg 的 `bin` 文件夹中（与 `ffmpeg.exe` 同目录）

### 3. 配置环境变量（可选但推荐）

将 yt-dlp 所在文件夹添加到系统 PATH，即可在任何位置使用命令。

---

## 二、基础使用

### 最简单的下载

```bash
# 下载单个视频（自动选择最佳画质）
yt-dlp "视频URL"

# 示例
yt-dlp "https://www.youtube.com/watch?v=xxxxx"
yt-dlp "https://www.bilibili.com/video/BV1xxxxx"
```

### 查看可用格式

```bash
yt-dlp -F "视频URL"
# 或
yt-dlp --list-formats "视频URL"
```

这会显示所有可用的视频/音频格式及其 ID、分辨率、文件大小等信息。

---

## 三、常用下载命令

### 1. 指定画质下载

```bash
# 下载最佳画质（视频+音频自动合并）
yt-dlp -f "bestvideo+bestaudio" "URL"

# 下载最佳 MP4 格式
yt-dlp -f "best[ext=mp4]" "URL"

# 下载 1080p MP4 视频 + M4A 音频并合并
yt-dlp -f 'bv[height=1080][ext=mp4]+ba[ext=m4a]' --merge-output-format mp4 "URL"

# 下载 4K 视频
yt-dlp -f 'bv[height=2160][ext=mp4]+ba[ext=m4a]' --merge-output-format mp4 "URL"

# 使用格式 ID 下载（通过 -F 查看 ID）
yt-dlp -f 137+140 "URL"
```

### 2. 仅下载音频

```bash
# 提取音频并转为 MP3
yt-dlp -x --audio-format mp3 "URL"

# 下载最佳音频质量
yt-dlp -f bestaudio "URL"

# 指定音频格式 ID（如 -f 140 通常是 YouTube 的 128k m4a）
yt-dlp -f 140 -x --audio-format mp3 "URL"
```

### 3. 下载播放列表

```bash
# 下载整个播放列表
yt-dlp "播放列表URL"

# 下载播放列表中的特定视频
yt-dlp --playlist-items 5,8,20 "播放列表URL"

# 下载第 1-5 个视频
yt-dlp --playlist-items 1-5 "播放列表URL"

# 按日期筛选（下载 2024年12月1日 之后的视频）
yt-dlp --dateafter 20241201 "播放列表URL"

# 下载最近 1 个月内的视频
yt-dlp --dateafter now-1months "播放列表URL"
```

---

## 四、高级功能

### 1. 使用 Cookie 下载（用于需要登录的视频）

**方法一：从浏览器直接读取（最简单）**
```bash
# 从 Chrome 浏览器读取 Cookie
yt-dlp --cookies-from-browser chrome "URL"

# 从 Edge 浏览器读取
yt-dlp --cookies-from-browser edge "URL"

# 指定 Chrome 配置文件（如果有多个用户）
yt-dlp --cookies-from-browser chrome::Profile 1 "URL"
```

**方法二：使用 Cookie 文件**
1. 安装浏览器扩展 **Cookie-Editor**（Chrome/Edge 应用商店）
2. 在目标网站登录后，点击扩展图标 → **Export** → **Export as Netscape**
3. 保存为 `cookies.txt` 文件
4. 使用命令：
```bash
yt-dlp --cookies cookies.txt "URL"
```

> **注意**：如果提示 Cookie 被锁定错误，需要先关闭浏览器，或用以下命令启动 Chrome：
> `"C:\Program Files\Google\Chrome\Application\chrome.exe" --disable-features=LockProfileCookieDatabase`

### 2. 自定义输出文件名

```bash
# 基础命名
yt-dlp -o "%(title)s.%(ext)s" "URL"

# 包含上传者、日期等信息
yt-dlp -o '%(title)s by %(uploader)s on %(upload_date)s.%(ext)s' "URL"

# 保存到指定目录
yt-dlp -o "D:/Videos/%(title)s.%(ext)s" "URL"

# 按播放列表分文件夹保存
yt-dlp -o "%(playlist)s/%(playlist_index)s - %(title)s.%(ext)s" "播放列表URL"
```

### 3. 下载字幕和元数据

```bash
# 下载视频 + 所有可用字幕
yt-dlp --write-subs --sub-langs all "URL"

# 下载自动生成的字幕（YouTube）
yt-dlp --write-auto-subs --sub-langs zh-CN "URL"

# 下载视频描述、缩略图、元数据
yt-dlp --write-description --write-thumbnail --write-info-json "URL"

# 嵌入缩略图到视频文件
yt-dlp --embed-thumbnail "URL"

# 嵌入元数据（标题、作者等）
yt-dlp --embed-metadata "URL"
```

### 4. 网络代理设置

```bash
# 使用 HTTP 代理
yt-dlp --proxy http://127.0.0.1:7890 "URL"

# 使用 SOCKS5 代理
yt-dlp --proxy socks5://127.0.0.1:1080 "URL"
```

### 5. 其他实用选项

```bash
# 限制下载速度（50KB/s）
yt-dlp -r 50K "URL"

# 设置年龄限制（跳过成人内容）
yt-dlp --age-limit 18 "URL"

# 多线程下载（5个并发片段）
yt-dlp --concurrent-fragments 5 "URL"

# 显示下载进度条
yt-dlp --progress "URL"

# 继续未完成的下载
yt-dlp -c "URL"

# 下载 YouTube Shorts（解决 403 错误）
yt-dlp --extractor-args "youtube:player_client=android" "URL"
```

---

## 五、实用组合命令示例

### 高清视频下载（推荐）

```bash
# 下载 1080p 以内最佳画质，优先 MP4，5线程，带进度，嵌入元数据
yt-dlp -f "bv*[height<=1080]+ba" -S "ext" --concurrent-fragments 5 --progress --embed-metadata --merge-output-format mp4 "URL"
```

### 完整下载（视频+音频+字幕+缩略图+元数据）

```bash
yt-dlp -f 'bv[ext=mp4]+ba[ext=m4a]' --embed-metadata --embed-thumbnail --write-subs --sub-langs zh-CN,en --merge-output-format mp4 "URL"
```

---

## 六、常见问题

| 问题 | 解决方案 |
|------|----------|
| **提示缺少 FFmpeg** | 下载 FFmpeg 并将 yt-dlp 放在其 bin 目录中，或添加到环境变量 |
| **YouTube 403 错误** | 添加 `--extractor-args "youtube:player_client=android"` 或使用 `--cookies-from-browser` |
| **Cookie 被锁定** | 关闭浏览器后重试，或添加启动参数 `--disable-features=LockProfileCookieDatabase` |
| **下载速度慢** | 使用 `--concurrent-fragments 5` 开启多线程，或检查代理设置 |
| **Bilibili 需要登录** | 使用 `--cookies-from-browser` 或导出 Cookie 文件 |

---

## 七、官方资源

- **GitHub 仓库**：https://github.com/yt-dlp/yt-dlp
- **详细文档**：https://github.com/yt-dlp/yt-dlp/blob/master/README.md
- **支持网站列表**：https://github.com/yt-dlp/yt-dlp/blob/master/supportedsites.md

