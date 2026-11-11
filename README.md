# RuiC-PoseAtlas 自建部署手册

> 这份是我们自己的操作手册，不是作者的 README。作者那份讲项目本身，这份讲**你怎么跑起来、怎么更新、怎么换地方部署**。

## 现状

- 站点：https://poseatlas-18h.pages.dev
- Cloudflare 项目名：`poseatlas`
- Cloudflare 账号：2416858007@qq.com
- 本地仓库根：`E:\AI`
- 站点目录：`E:\AI\poseatlas`
- GitHub 仓库：https://github.com/Dravi-art/RuiC-PoseAtlas（代码 + 缩略图，不含原图）

## 目录说明

| 路径 | 内容 | 能不能删 |
|---|---|---|
| `E:\AI\poseatlas` | 完整站点：代码 + 姿势/衣装/人像全部原图 | 建议保留 |
| `E:\AI\README.md` | 本文件 | 保留 |
| `E:\AI\.gitignore` | 忽略原图，只提交代码和缩略图 | 保留 |

## 日常更新（作者更新了仓库）

作者仓库：https://github.com/HRuiCcc/RuiC-PoseAtlas

```powershell
cd E:\AI\poseatlas
git remote add upstream https://github.com/HRuiCcc/RuiC-PoseAtlas.git   # 只需第一次
git fetch upstream
git merge upstream/main
```

重新部署：

```powershell
set CLOUDFLARE_API_TOKEN=<你的 Cloudflare API Token>
C:\Users\Administrator\AppData\Roaming\npm\wrangler.cmd pages deploy E:\AI\poseatlas --project-name poseatlas --branch main
```

**注意**：部署目录里不能有 `.git`（会导致上传几千个 git 对象文件，站点 522）。如果 `poseatlas` 里有 `.git`，先复制一份不含 `.git` 的目录再部署：

```powershell
robocopy E:\AI\poseatlas E:\AI\deploy /E /XD .git /NFL /NDL /NJH /NJS /NP
C:\Users\Administrator\AppData\Roaming\npm\wrangler.cmd pages deploy E:\AI\deploy --project-name poseatlas --branch main
```

## 从零开始（换机器 / 重装）

### 1. 拉取作者仓库

```powershell
git clone https://github.com/HRuiCcc/RuiC-PoseAtlas.git E:\AI\poseatlas
```

### 2. 下载素材包

夸克网盘：https://pan.quark.cn/s/d775c1471804?pwd=Ahcd
提取码：`Ahcd`

三个包：
- `AI 作图姿势库.zip`（约 630MB）
- `AI 服装库.zip`（约 1.3GB）
- `AI 作图脸库.zip`（约 4.6GB）

### 3. 解压

```powershell
7z x "AI 作图姿势库.zip" -oE:\AI\src\pose
7z x "AI 服装库.zip" -oE:\AI\src\costume
7z x "AI 作图脸库.zip" -oE:\AI\src\face
```

### 4. 合并图片进站点

| 素材 | 来源 | 目标 |
|---|---|---|
| 姿势 | `E:\AI\src\pose\originals\*.png` | `E:\AI\poseatlas\img\` |
| 衣装 | `E:\AI\src\costume\originals\*.png` | `E:\AI\poseatlas\costume\img\`（仓库自带 webp，png 可选） |
| 人像 | `E:\AI\src\face\originals\*.png` | `E:\AI\poseatlas\portrait\img\` |

**人像这一步必须做**：作者仓库默认不包含人像原图（`.gitignore` 忽略了 `portrait/img/`），不拷进去人像页点开大图是空的。

### 5. 安装 wrangler

```powershell
npm install -g wrangler
```

### 6. 部署

```powershell
set CLOUDFLARE_API_TOKEN=<你的 Cloudflare API Token>
C:\Users\Administrator\AppData\Roaming\npm\wrangler.cmd pages deploy E:\AI\poseatlas --project-name poseatlas --branch main
```

部署完会输出一个 `https://xxxx.poseatlas-18h.pages.dev` 的地址。

## Cloudflare 凭据

- API Token：去 https://dash.cloudflare.com → 右上角头像 → My Profile → API Tokens → Create Token → 选 Cloudflare Pages Edit
- 账号：2416858007@qq.com
- 项目名：`poseatlas`
- 生产域名：https://poseatlas-18h.pages.dev

## 常见问题

### push 到 GitHub 失败（`did not receive expected object`）

GitHub 单次 push 上限约 2GB，完整仓库 5.4GB 推不上去。网络不稳时 800MB 也会断。
**图片不需要进 GitHub**——它们在 Cloudflare 上。GitHub 只放代码 + 缩略图就够了。

### 部署后 522 错误

Cloudflare 到源站超时。检查部署目录里是不是混进了 `.git`（会导致上传几千个 git 对象文件）。
**必须用不含 `.git` 的目录部署**。

### 更新后图片丢失 / 人像页空白

作者仓库的 `.gitignore` 默认忽略 `portrait/img/`。`git pull` 之后检查一下这个目录还在不在，不在就从 `E:\AI\src\face\originals\` 重新拷。

### 想换域名

Cloudflare Pages 免费给 `*.pages.dev` 子域名，不用买域名。想用自己的域名：Cloudflare Pages → 项目 → Custom domains → 添加。

## 站点结构

- 姿势图鉴：`/`
- 衣装图鉴：`/costume.html`
- 人像图鉴：`/face.html`

## 一句话总结

**部署 = 站点目录 + wrangler + Cloudflare token。** 图片在 Cloudflare 上，代码 + 缩略图放 GitHub 备份。更新就是 `git pull` → `robocopy`（去 .git）→ `wrangler deploy` 三步。
