# 综合网站 · 个人导航 & 博客系统

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
