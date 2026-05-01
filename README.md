# 综合网站 · 个人导航 & 博客系统（代码没有整合的原因是这样便于学习，可以拆分引用，总计23个文件）

基于腾讯云 EdgeOne Pages 构建的全栈个人网站，所有数据存储在 EdgeOne KV（绑定名 `NAV_KV`），无需数据库，零冷启动。

## 功能列表

### 首页
- 左侧固定侧边栏（书签分类、热门文章、后台入口）
- 博客/书签 Tab 切换
- 搜索文章
- 标签云
- 暗色模式

### 文章管理
- 发布/编辑/删除文章
- Quill 富文本编辑器
- 封面图、摘要、标签
- 置顶功能
- 草稿/发布状态
- 阅读量统计

### 书签管理
- 添加/编辑/删除书签
- 排序功能
- Logo 和描述

### 站点设置
- 站点标题、副标题
- Logo 设置
- 页眉背景图
- 国内线路链接

## 部署步骤

### 1. 创建 KV 命名空间

1. 登录腾讯云 EdgeOne Pages 控制台
2. 进入 KV 存储，创建命名空间（如 `myblog`）

### 2. 创建 Pages 项目

1. 关联 GitHub 仓库
2. 分支选择 master
3. 构建命令留空
4. 输出目录留空
5. 点击部署

### 3. 绑定 KV

1. 进入项目 → KV 存储 → 绑定命名空间
2. 变量名：`NAV_KV`（必须大写）
3. 选择创建的 KV 命名空间

### 4. 首次登录

- 访问 `/admin`
- 默认密码：`admin123`

## 注意事项

1. KV 绑定名必须是 `NAV_KV`
2. 图片上传限制 5MB
3. 国内线路按钮需要先在后台填写链接才会显示

# 旭儿导航 · EdgeOne Pages 完整版

基于腾讯云 EdgeOne Pages 构建的全栈个人网站，支持书签导航和博客管理。所有数据存储在 EdgeOne KV 中，无需数据库，零冷启动。

## 📁 文件结构及作用

📁 .edgeone/
   └── functions.json               # 1

📁 functions/
   ├── [[catchall]].js              # 2
   ├── _middleware.js               # 3
   ├── admin.js                     # 4
   ├── index.js                     # 5
   ├── logout.js                    # 6
   │
   ├── 📁 post/
   │   └── [[slug]].js              # 7
   │
   └── 📁 api/
       ├── blog.js                  # 8
       ├── change-password.js       # 9
       ├── config.js                # 10
       ├── header-bg.js             # 11
       ├── logo.js                  # 12
       ├── logo-link.js             # 13
       ├── search.js                # 14
       ├── site-info.js             # 15
       ├── sitemap.js               # 16
       ├── stats.js                 # 17
       ├── upload.js                # 18
       │
       ├── 📁 blog/
       │   └── [[id]].js            # 19
       │
       ├── 📁 config/
       │   └── [id].js              # 20
       │
       └── 📁 image/
           └── [filename].js        # 21

📄 _routes.json                     # 22
📄 README.md                        # 23


### 核心文件详解

| 文件路径 | 作用 | 说明 |
|----------|------|------|
| `.edgeone/functions.json` | 路由映射 | 将 URL 路径映射到对应的 Function 文件 |
| `functions/[[catchall]].js` | **主入口** | 包含首页、后台管理、所有 API 路由 |
| `functions/_middleware.js` | 中间件 | 处理退出登录，放行静态资源和 API |
| `functions/logout.js` | 退出登录 | 清理 session 并跳转首页 |
| `functions/post/[[slug]].js` | 文章详情页 | 根据 slug 显示文章完整内容 |
| `_routes.json` | 路由规则 | 定义哪些路径走 Functions |

## 🚀 部署步骤

### 第一步：创建 KV 命名空间

1. 登录 [腾讯云 EdgeOne Pages 控制台](https://console.cloud.tencent.com/edgeone/pages)
2. 左侧菜单点击 **"KV 存储"**
3. 点击 **"新建命名空间"**
4. 名称填写：`myblog`（或其他任意名称）
5. 点击 **"创建"**

### 第二步：创建 Pages 项目

1. 进入 **Pages** → **创建项目**
2. 选择 **"连接 Git"** 或 **"直接上传"**
3. 如果使用 Git，关联你的 GitHub 仓库，选择 `master` 分支
4. **构建命令**：留空
5. **输出目录**：留空
6. 点击 **"创建"** 或 **"保存并部署"**

### 第三步：绑定 KV 命名空间

1. 进入项目 → **"KV 存储"** → **"绑定命名空间"**
2. **变量名**：`NAV_KV`（必须大写）
3. **命名空间**：选择第一步创建的 `myblog`
4. 点击 **"保存"**

### 第四步：等待部署

部署约需 1-2 分钟，完成后会获得一个 `https://项目名.edgeone.app` 域名。

### 第五步：首次登录

1. 访问 `https://项目名.edgeone.app/admin`
2. 输入密码：`admin123`
3. 登录后立即修改密码（后台右上角"修改密码"按钮）

## ✨ 功能列表

### 首页（`/`）

| 区域 | 功能 |
|------|------|
| 顶部 | 站点标题、副标题、日期、国内线路按钮 |
| 左侧侧边栏 | 博客列表入口、书签分类（带数量）、热门文章（带阅读量）、后台入口 |
| 主内容区 | 博客/书签 Tab 切换 |
| 博客 Tab | 搜索框、标签云、文章卡片（标题、分类、日期、阅读量、摘要、封面图） |
| 书签 Tab | 书签卡片网格（名称、分类、描述、复制链接按钮） |
| 右下角 | 暗色模式切换、返回顶部按钮 |
| 移动端 | 侧边栏收起/展开按钮 |

### 后台管理（`/admin`）

| 模块 | 功能 |
|------|------|
| 文章管理 | 发布、编辑、删除文章 |
| 文章字段 | 标题、分类、状态（发布/草稿）、封面图、摘要、内容、标签、置顶 |
| 编辑器 | Quill 富文本编辑器（粗体、斜体、颜色、列表、链接、图片） |
| 书签管理 | 添加、编辑、删除书签 |
| 书签字段 | 名称、网址、分类、排序（数字越小越靠前）、Logo URL、描述 |
| 站点设置 | 站点标题、副标题、国内线路链接 |
| Logo 设置 | Logo URL、Logo 跳转链接、页眉背景图 |
| 安全 | 修改管理员密码 |

### 文章详情页（`/post/:id`）

| 区域 | 功能 |
|------|------|
| 标题区 | 文章标题 |
| 元信息 | 分类、发布时间、阅读量 |
| 标签区 | 文章标签徽章 |
| 内容区 | 富文本内容 |
| 底部 | 相关文章推荐、返回首页按钮 |

### API 接口（`/api/*`）

| 接口 | 方法 | 说明 |
|------|------|------|
| `/api/config` | GET | 获取书签列表 |
| `/api/config` | POST | 添加书签 |
| `/api/config/:id` | DELETE | 删除书签 |
| `/api/blog` | GET | 获取文章列表 |
| `/api/blog` | POST | 发布文章 |
| `/api/blog/:id` | PUT | 更新文章 |
| `/api/blog/:id` | DELETE | 删除文章 |
| `/api/site-info` | GET | 获取站点信息 |
| `/api/site-info` | POST | 保存站点信息 |
| `/api/change-password` | POST | 修改密码 |
| `/api/upload` | POST | 上传图片 |
| `/api/image/:filename` | GET | 获取图片 |

## 🔧 配置说明

### 环境变量/KV 绑定

| 绑定名 | 类型 | 说明 |
|--------|------|------|
| `NAV_KV` | KV 命名空间 | 存储所有数据（必需） |

### 默认管理员密码

- 用户名：`admin`（固定）
- 密码：`admin123`（首次登录后请修改）

### KV 数据结构（自动创建）

| Key | 类型 | 说明 |
|-----|------|------|
| `sites` | JSON Array | 书签列表 |
| `blog_posts` | JSON Array | 文章列表 |
| `admin_password` | String | 管理员密码 |
| `site_title` | String | 站点标题 |
| `site_subtitle` | String | 站点副标题 |
| `site_logo` | String | Logo URL |
| `site_logo_link` | String | Logo 跳转链接 |
| `header_bg` | String | 页眉背景图 |
| `cn_link` | String | 国内线路链接 |
| `views:文章ID` | String | 文章阅读量 |
| `img:文件名` | String | 上传的图片（Base64） |
| `session:token` | String | 登录会话 |

## 🔄 部署流程总结


## 📝 注意事项

1. **KV 绑定名必须是 `NAV_KV`**，区分大小写
2. 构建命令和输出目录**必须留空**
3. 图片上传限制 5MB，自动存入 KV
4. 书签排序：数字越小越靠前
5. 置顶文章会显示在列表最前面
6. 国内线路按钮：只有在后台填写了链接才会显示
7. 文章 slug 自动从标题生成，重复时会自动添加后缀

## ❓ 常见问题

### Q: 部署后访问出现 404？
A: 检查 `.edgeone/functions.json` 和 `_routes.json` 文件是否存在，且内容正确。

### Q: 首页显示"暂无文章"？
A: 需要先在后台发布文章，并确保状态为"发布"。

### Q: 图片上传失败？
A: 检查图片大小是否超过 5MB，或格式是否为图片格式（支持 jpg、png、gif、webp）。

### Q: 富文本编辑器不显示？
A: 检查网络是否能访问 CDN，或更换其他 CDN 源。

### Q: 忘记管理员密码？
A: 在 EdgeOne KV 控制台直接修改 `admin_password` 的值。

### Q: 如何绑定自定义域名？
A: Pages 项目 → **"域名管理"** → **"添加域名"**，按提示添加 CNAME 记录。

### Q: 国内线路按钮不显示？
A: 需要在后台 **站点设置** 中填写国内线路链接才会显示。

## 📄 许可证

MIT License

总数：23 个文件
目录	文件数
.edgeone/	1
functions/ 根目录	5
functions/post/	1
functions/api/ 根目录	11
functions/api/blog/	1
functions/api/config/	1
functions/api/image/	1
根目录配置文件	2
合计	23
