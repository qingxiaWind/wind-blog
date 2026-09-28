---
title: 建站过程
date: 2026-09-28 22:24:10
categories:
  - 技术
tags:
  - Blog
---

*注：本文由我和GPT的聊天整理而成*

# 1. 最终成果和整体流程

这次采用的方案是：

```text
Hexo + GitHub + Cloudflare Pages
```

整体流程是：

```text
你在电脑上写 Markdown 文章
        ↓
Hexo 把 Markdown 转换成网页
        ↓
Git 记录和保存修改
        ↓
GitHub 保存博客源码
        ↓
Cloudflare Pages 自动读取 GitHub 仓库
        ↓
Cloudflare 自动执行 npm run build
        ↓
Cloudflare 发布 public 文件夹
        ↓
博客可以通过 pages.dev 地址访问
```

---

# 2. 工具与概念

## 2.1 Hexo 

Hexo 是一个静态博客生成器。

你写的是：

```text
文章.md
```

Hexo 会生成：

```text
文章.html
```

例如你创建：

```text
source/_posts/博客的创建.md
```

Hexo 会生成类似：

```text
public/2026/07/02/博客的创建/index.html
```

Hexo 的特点：

- 不需要数据库
- 不需要自己维护服务器程序
- 页面速度快
- 很适合个人博客
- 可以免费部署到 GitHub Pages 或 Cloudflare Pages
- 文章主要使用 Markdown 编写

---

## 2.2 Node.js

Node.js 是一个 JavaScript 运行环境。Hexo 本身就是基于 Node.js 生态运行的，所以即使平时写博客不需要会 JavaScript，也需要先安装 Node.js。

安装 Node.js 后会同时获得 `npm`。`npm` 可以理解为 Node.js 的“软件包管理器”，用来安装 Hexo、主题和各种依赖。

在这个博客项目里，常见的 Node.js / npm 命令有：

```bash
npm install -g hexo-cli
npm install
npm run build
```

分别可以理解为：

- `npm install -g hexo-cli`：在电脑上安装 Hexo 命令行工具
- `npm install`：根据 `package.json` 安装当前博客需要的依赖
- `npm run build`：按照项目配置生成静态网页；Cloudflare Pages 部署时也会执行这一步

Node.js 在这里主要负责“运行 Hexo 和构建网站”，并不代表博客上线后需要自己长期运行一个 Node.js 服务器。Cloudflare Pages 会在部署时自动完成构建。

---

## 2.3 VS Code

VS Code 是本地编辑器，主要用来编辑：

- Markdown 文章
- `_config.yml`
- `_config.fluid.yml`
- 其他主题或项目配置文件

VS Code 不是 Hexo 的必需组件，换成其他文本编辑器也可以；只是它对 Markdown、YAML、Git 和终端的支持比较方便。

---

## 2.4 Git 

Git 是一个版本管理工具。

它可以记录：

- 哪些文件被修改
- 哪些文件被新增
- 哪些文件被删除
- 每次修改的说明
- 每次修改的时间
- 历史版本

Git 主要运行在你的本地电脑上。

---

## 2.5 GitHub 

GitHub 可以理解为云端代码仓库。

你的博客源码上传到 GitHub 后：

- 不会只保存在电脑里
- 可以查看历史版本
- 可以从其他电脑下载
- Cloudflare 可以自动读取
- 每次 `git push` 后都会触发 Cloudflare 部署

---

## 2.6 Cloudflare Pages 

Cloudflare Pages 是静态网站托管平台。

它会自动完成：

```text
读取 GitHub
→ 安装依赖
→ 运行 npm run build
→ 生成 public
→ 发布网站
```

你不需要购买服务器。

---

## 2.7 域名

当前免费的地址是：

```text
https://wind-blog-f2h.pages.dev
```

以后可以购买自定义域名，例如：

```text
https://windblog.com
```

域名只是更好记的网站地址，不是博客运行的必要条件。

---

## 2.8 静态博客与 WordPress 的区别

| 对比项       | Hexo             | WordPress          |
| ------------ | ---------------- | ------------------ |
| 网站类型     | 静态             | 动态               |
| 数据库       | 不需要           | 通常需要           |
| 服务器       | 可用免费静态托管 | 自建时通常需要     |
| 写文章       | Markdown         | 网页后台           |
| 维护难度     | 较低             | 较高               |
| 插件         | 较少             | 很多               |
| 安全维护     | 较少             | 需要更新程序、插件 |
| 适合个人博客 | 非常适合         | 也适合，但更复杂   |
| 成本         | 可为 0 元        | 通常需要主机费用   |

---

# 3. 费用

## 3.1 当前方案可以 0 元运行

| 项目             |                 费用 |
| ---------------- | -------------------: |
| Hexo             |                 免费 |
| Git              |                 免费 |
| GitHub           |                 免费 |
| Cloudflare Pages | 免费额度足够个人博客 |
| Node.js          |                 免费 |
| VS Code          |                 免费 |
| pages.dev 地址   |                 免费 |
| HTTPS            |                 免费 |

目前不需要：

- 买服务器
- 买数据库
- 买证书
- 买域名
- 买主题

---

## 3.2 以后可能花钱的地方

### 域名

普通 `.com` 域名通常每年几十到一百多元人民币。购买时不要只看第一年价格，要看：

- 续费价格
- 是否有隐私保护
- 是否方便转出
- 是否支持双重验证

### 主题

很多 Hexo 主题是免费的，刚开始不建议购买收费主题。

### 图片存储

图片很多以后，可以考虑：

- Cloudflare R2
- 对象存储
- 图床

目前博客图片统一放在：

```text
source/img
```

---

# 4. 需要安装的软件

需要安装：

1. Git
2. Node.js
3. VS Code
4. Hexo CLI

其中：

- Git、Node.js、VS Code 从官网下载
- Hexo 通过终端安装

---

# 5. 认识 Hexo 项目结构

项目结构：

```text
wind-blog
├── _config.yml
├── _config.fluid.yml
├── package.json
├── package-lock.json
├── scaffolds
├── source
│   ├── _posts
│   ├── _drafts
│   └── img
├── themes
├── node_modules
└── public
```

说明：

| 文件或目录          | 用途                                      |
| ------------------- | ----------------------------------------- |
| `_config.yml`       | Hexo 博客总配置                           |
| `_config.fluid.yml` | 当前 Fluid 主题的独立配置                 |
| `source/_posts`     | 正式文章                                  |
| `source/_drafts`    | 草稿                                      |
| `source/img`        | 博客图片、Banner、头像等静态资源          |
| `themes`            | 主题目录                                  |
| `package.json`      | 依赖和 npm 脚本                           |
| `package-lock.json` | 锁定依赖版本，建议提交到 Git              |
| `node_modules`      | 本地安装的依赖，不上传                    |
| `public`            | Hexo 生成的网站文件，一般不提交到源码仓库 |

---

# 6. 创建和编写文章

目前 `_config.yml` 建议使用：

```yaml
new_post_name: :year-:month-:day-:title.md
```

因此以后新文章的文件名统一使用：

```text
年-月-日-英文标题.md
```

例如执行：

```bash
hexo new "building-my-blog"
```

会生成类似：

```text
source/_posts/2026-09-28-building-my-blog.md
```

文件名主要用于项目管理和 URL；真正展示给读者的标题由文章 Front Matter 中的 `title` 决定，所以可以继续使用中文：

```yaml
title: 博客的创建
```

完整示例：

```markdown
---
title: 博客
date: 2026-07-02 18:43:35
categories:
  - 建站记录
tags:
  - Hexo
  - Git
  - Cloudflare
---

# 博客的创建

今天我第一次建立自己的个人博客

## 使用的工具

- Hexo
- Git
- GitHub
- Cloudflare Pages
- Visual Studio Code

## 我的目标

以后我会在这里记录学习、生活和思考。
```



## 6.1 在 Markdown 中插入图片

目前图片统一放在：

```text
source/img
```

为了方便维护，可以继续按文章建立子文件夹，例如：

```text
source/img/building-my-blog/github.png
source/img/building-my-blog/cloudflare.png
```

Markdown 中使用：

```markdown
![图片说明](/img/building-my-blog/github.png)
```

注意：

- Markdown 里的路径使用 `/`，不要使用 Windows 的 `\`
- 图片文件名尽量使用小写英文和短横线
- `source/img/...` 在生成网站后会对应 `/img/...`
- 首页 Banner、关于页头像等也可以统一放在 `source/img` 下管理

---

# 7. YAML 与 Front Matter 格式

文章最上方的配置区域叫 Front Matter。

结构必须是：

```markdown
---
配置
---
正文
```

例如：

```yaml
---
title: 博客的创建
date: 2026-07-02 18:43:35
categories:
  - 技术
tags:
  - Hexo
  - Git
  - Cloudflare
---
```

其中：

- `categories`：适合表示文章所属的主要“大类”，个人博客通常每篇文章保留 1 个主要分类即可
- `tags`：适合表示更细的关键词，一篇文章可以有多个标签
- `date`：Hexo 默认会使用这里的时间参与文章排序，而不是依靠 Markdown 文件名排序

---

# 8. Git 的基本工作原理

最常用的流程：

```bash
git add .
git commit -m "说明"
git push
```

可以理解为：

```text
git add .
把修改放入待提交区
```

```text
git commit
在本地保存一个版本
```

```text
git push
上传到 GitHub
```

---

## 8.1 Git 与 Hexo 是两套不同的东西

Hexo：

```bash
hexo server
hexo clean
hexo generate
```

负责：

- 本地预览
- 生成网页
- 检查文章格式

Git：

```bash
git add .
git commit
git push
```

负责：

- 记录修改
- 保存版本
- 上传 GitHub

不要把 `git commit` 理解成提交 `hexo server`。

---

# 9. 部署到 Cloudflare Pages

进入 Cloudflare 后：

```text
Workers 和 Pages
→ 开始构建
```

新版页面可能显示：

```text
Ship something new
```

以及：

- Connect GitHub
- Connect GitLab
- 从 Hello World 开始
- 选择模板
- Upload your static files

如果底部显示：

```text
想要部署 Pages？开始使用
```

点击：

```text
开始使用
```

然后选择：

```text
连接到 Git
```

---

## 9.1 选择仓库

连接 GitHub 后选择：

```text
qingxiaWind / wind-blog
```

---

## 9.2 构建配置

填写：

```text
项目名称：wind-blog
生产分支：main
框架预设：无
构建命令：npm run build
构建输出目录：public
根目录：留空
环境变量：留空
```

### 为什么框架预设可以选“无”

因为已经手动填写：

```text
npm run build
public
```

框架预设只是帮你自动填写这些内容。

---

## 9.3 保存并部署

点击：

```text
保存并部署
```

Cloudflare 会：

```text
读取 GitHub
→ 安装依赖
→ 运行 npm run build
→ 生成 public
→ 发布网站
```

---

## 9.4 设置正式网站地址

Cloudflare 分配地址：

```text
https://wind-blog-f2h.pages.dev
```

修改 `_config.yml`：

```yaml
url: https://wind-blog-f2h.pages.dev
root: /
```

然后：

```bash
hexo clean
hexo generate
git add .
git commit -m "Set site URL"
git push
```

成功标志：

```text
main -> main
```

Cloudflare 会自动部署新版本。

---

# 10. 日常发布文章的标准流程
## 10.1 创建文章

```bash
hexo new "文章标题"
```

---

## 10.2 编辑文章

路径：

```text
source/_posts/年-月-日-英文标题.md
```

---

## 10.3 本地测试

```bash
hexo clean
hexo server
```

打开：

```text
http://localhost:4000
```

---

## 10.4 停止服务器

```text
Ctrl + C
```

---

## 10.5 生成检查

```bash
hexo clean
hexo generate
```

如果没有红色 ERROR，继续。

---

## 10.6 检查 Git

```bash
git status
```

---

## 10.7 提交和上传

```bash
git add .
git commit -m "准确描述这次修改"
git push
```

完整流程：

```text
写文章
→ 本地预览
→ 修复错误
→ hexo generate 检查
→ git status
→ git add .
→ git commit
→ git push
→ Cloudflare 自动部署
```

---

# 11. Git commit 信息怎么写

`git commit -m "..."` 中的文字不是固定代码。

它只是：

> 说明这次做了什么。

可以写中文，也可以写英文。

---

## 11.1 常见例子

| 操作         | 推荐 commit                                 |
| ------------ | ------------------------------------------- |
| 新增文章     | `git commit -m "添加博客创建文章"`          |
| 修改文章     | `git commit -m "更新博客创建文章"`          |
| 删除默认文章 | `git commit -m "删除 Hello World 默认文章"` |
| 修改博客标题 | `git commit -m "修改博客标题"`              |
| 修复标签格式 | `git commit -m "修复文章标签格式"`          |
| 修改网站地址 | `git commit -m "更新网站地址"`              |
| 添加图片     | `git commit -m "添加文章图片"`              |
| 更换主题     | `git commit -m "更换博客主题"`              |
| 修改主题配置 | `git commit -m "调整主题配置"`              |

英文也可以：

```bash
git commit -m "Add new post"
git commit -m "Update blog title"
git commit -m "Fix post tags"
git commit -m "Remove Hello World post"
```

---

## 11.2 好的 commit 信息

推荐：

```text
添加暑假计划文章
修复文章标签格式
修改博客标题
更新网站地址
```

不推荐：

```text
改一下
更新
aaa
test
```

因为以后看不懂改了什么。

---
