# GPT 龙娘表情公开图库

包含 30 张预先生成的 384 × 384 PNG，图片原始字节保持一致。只发布表情图片、目录与校验表。

## 发布步骤

1. 登录你自己的 GitHub 账号，创建一个 Public 仓库，例如 `gpt-chat-stickers`。可勾选创建 README 以初始化仓库。
2. 解压下载包。在仓库中选择 Add file → Upload files，把解压后的 `stickers` 文件夹、`catalog.json`、`SHA256SUMS`、`README.md` 上传到仓库根目录。不要只上传 ZIP 文件。
3. 提交文件，然后把公开仓库网址发回聊天，继续验证一张实际图片。

仓库根目录应包含：

```text
README.md
catalog.json
SHA256SUMS
stickers/
  0.3.7/
    happy-yes.png
    ...其余 29 张 PNG
```

公开图片直链格式示例（占位符需替换成实际值，默认分支以仓库为准）：

```text
https://raw.githubusercontent.com/<用户名>/<仓库名>/<默认分支>/stickers/0.3.7/happy-yes.png
```

只有上传维护者需要 GitHub 账号；朋友读取公开图片不需要 GitHub 登录或账号连接。GitHub 自带测试 PNG 已在用户普通聊天中验证可见，本图库的 GitHub 地址仍需单独验证后才用于插件。

此图库包不包含 Codex 安装器或插件服务，不会改变现有 Codex 用法。
