---
name: misskey
description: |
  Misskey API integration for posting notes and uploading media to Misskey/Fediverse instances.
  Use when users want to post to Misskey, upload images, or interact with Fediverse.
  Triggers: "发帖到misskey", "misskey发图", "post to misskey", "fediverse发帖".
metadata:
  version: "1.0.0"
---

# Misskey API

发帖和上传图片到 Misskey/Fediverse 实例。

## 配置

需要设置环境变量或配置文件：

```bash
# Misskey 实例地址
export MISSKEY_HOST="https://maid.lat"
# API Token (从设置 > API 获取)
export MISSKEY_TOKEN="your-token-here"
```

**获取 Token：**
1. 登录 Misskey 实例
2. 设置 > API > 访问令牌
3. 创建新令牌，勾选需要的权限

## 发帖

### 发送文本

```bash
MISSKEY_HOST="https://maid.lat" MISSKEY_TOKEN="xxx" \
  bash ~/.openclaw/workspace/skills/misskey/scripts/post.sh "你好世界！"
```

### 发送带图片的帖子

```bash
MISSKEY_HOST="https://maid.lat" MISSKEY_TOKEN="xxx" \
  bash ~/.openclaw/workspace/skills/misskey/scripts/post.sh "图片说明" "/path/to/image.png"
```

### 发送多图帖子

```bash
MISSKEY_HOST="https://maid.lat" MISSKEY_TOKEN="xxx" \
  bash ~/.openclaw/workspace/skills/misskey/scripts/post.sh "多图帖子" "/path/to/img1.png" "/path/to/img2.png"
```

## 上传图片

单独上传图片到网盘：

```bash
MISSKEY_HOST="https://maid.lat" MISSKEY_TOKEN="xxx" \
  bash ~/.openclaw/workspace/skills/misskey/scripts/upload.sh "/path/to/image.png"
```

## 可见性选项

在帖子文本后添加可见性参数：

```bash
# 公开（默认）
bash post.sh "内容" --visibility public

# 首页
bash post.sh "内容" --visibility home

# 关注者
bash post.sh "内容" --visibility followers

# 指定用户
bash post.sh "内容" --visibility specified --visible-user-ids "user-id"
```

## 添加 CW (内容警告)

```bash
bash post.sh "正文内容" --cw "内容警告标题"
```

## 删除帖子

```bash
MISSKEY_HOST="https://maid.lat" MISSKEY_TOKEN="xxx" \
  bash ~/.openclaw/workspace/skills/misskey/scripts/delete.sh "帖子ID"
```

帖子ID 可以从帖子链接获取：`https://maid.lat/notes/ak4lrcfalen102bc` → ID 为 `ak4lrcfalen102bc`

## API 端点

| 端点 | 方法 | 用途 |
|------|------|------|
| /api/notes/create | POST | 发帖 |
| /api/drive/files/create | POST | 上传文件 |
| /api/i | POST | 获取当前用户信息 |

## 错误处理

- 401: Token 无效或过期
- 400: 参数错误
- 429: 请求过于频繁

## 示例：maid.lat 实例

```bash
# 配置
export MISSKEY_HOST="https://maid.lat"
export MISSKEY_TOKEN="your-token"

# 发帖
bash ~/.openclaw/workspace/skills/misskey/scripts/post.sh "来自 OpenClaw 的测试帖子！"
```
