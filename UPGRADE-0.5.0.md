# 随聊表情 0.5.0 更新步骤

图库增加四张独立生成的 Q 版表情：生气了！（angry-puff）、难过了（sad-cry）、无语了…（speechless-deadpan）、加油呀！（encourage-cheer）。现在共 34 张，原有 30 张标准 PNG 和原稿字节保持不变。

本次交付的是待上传、待部署的更新文件。新的 GitHub 文件和服务部署尚未替你执行；本地验证不能代替部署后的客户端验证。

## 一、更新 GitHub 图库

1. 解压 chat-memes-github-update-0.5.0.zip。
2. 打开 https://github.com/herobrinein/gpt-chat-stickers ，选择 Add file → Upload files。
3. 上传解压后直接看到的 stickers 文件夹、catalog.json、SHA256SUMS、README.md、UPGRADE-0.5.0.md；不要把包含这些内容的外层文件夹整体作为仓库顶层新增目录。
4. 提交到 main。旧 stickers/0.3.7/ 目录保留，新图在 stickers/0.5.0/。
5. 用浏览器打开以下地址确认 GitHub 已能读取新图：

https://raw.githubusercontent.com/herobrinein/gpt-chat-stickers/main/stickers/0.5.0/angry-puff.png

## 二、更新普通聊天图片服务

仅上传图片还不够：服务还要知道四张新图的 id、用途、地址和哈希。

1. 解压 chat-memes-images-service-0.4.0.zip，进入同时包含 package.json 与 wrangler.jsonc 的目录。
2. 在 Windows PowerShell 执行：

```powershell
npm.cmd ci
npm.cmd run deploy
```

macOS Terminal 对应执行：

```sh
npm ci
npm run deploy
```

需要 Node.js 22 或更新版本。使用此前部署 chat-memes-images 的同一个 Cloudflare 账号；wrangler.jsonc 保留原 Worker 名称。ZIP 不含 node_modules，npm ci 会重建依赖，不需要旧文件夹。

3. 原服务地址保持不变：https://chat-memes-images.herobrinechnishere.workers.dev/mcp 。无需重填地址或修改无认证设置。
4. 在 ChatGPT 插件列表打开「随聊表情图片服务」，刷新其工具元数据，然后新建普通聊天。
5. 对原账号及测试账号各刷新一次；已有用户需要刷新才能发现新 id，新安装用户直接读取当前目录。个性化指令不用重新修改。
6. 用下面请求检查新图：

```text
请调用当前随聊表情图片服务的 show_gpt_sticker，id 为 angry-puff，显示已有图片，不生成图片，并简短报告 rendererVersion。
```

预期 rendererVersion 为 0.4.0，出现「生气了！」图片卡片。其他新增 id 为 sad-cry、speechless-deadpan、encourage-cheer。

## 三、更新 Codex 本地版

普通聊天和本地 Codex 可以独立更新。本地包直接内置全部 34 张标准 PNG，不需要等待 GitHub 上传或服务部署。

1. Windows 可解压 chat-memes-codex-local-0.5.1.zip；macOS 也可解压相同 ZIP，或使用提供的 tar.gz。
2. 进入包含 plugin.json、scripts、skills、assets 的 chat-memes 目录。
3. Windows PowerShell 执行：

```powershell
py -3 scripts/install_codex.py
```

macOS Terminal 执行：

```sh
python3 scripts/install_codex.py
```

4. 安装器同步本机 ~/.agents/skills/expressive-chat，并合并表情偏好到原全局指令，保留非表情内容。已安装旧版本时运行同一命令完成更新，无需先卸载。
5. 新开 Codex 会话，发送“显示新增的‘生气了！’表情”检查新图；日常继续按语境自动选图，不需要每轮运行脚本。

0.5.1 同时调整配图叙述：选图、读图库和准备 PNG 默认不再单独播报，开头直接回应用户或说明实际任务进度。必须重新运行安装器并新开会话，才能同步技能和全局偏好；仅解压文件不生效。宿主明确要求首次技能提示时仍需遵从，不能承诺所有客户端完全不出现提示。本次是指令层调整，尚未在你的本机实测播报行为。

此包只更新本机技能，不会替换账号里的云端主插件，也不改变普通聊天服务连接。

## 版本关系

- 图库图片：0.5.0，34 张；主插件与 Codex 本地包：0.5.1，包含减少配图播报的调整。
- 图片服务：0.4.0，34 个表情 id，新增 angry、sad 分类。
- 原有三十张公共路径保持 stickers/0.3.7/；四张新图使用 stickers/0.5.0/。
- 四张高清原稿另附打包文件；标准图为 384×384 透明 PNG。
