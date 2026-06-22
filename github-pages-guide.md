# GitHub Pages 静态网站托管指南

适用场景：把本地的旅行 H5 页面发布成一个公网 HTTPS 链接，然后复制到微信里分享。

## 为什么本地打开会出问题

你现在从文件里打开，地址通常是 `file:///C:/.../index.html`。这个地址只存在于你的电脑上，别人和微信都访问不到。

另外，页面里的地图、图片、分享按钮依赖浏览器网络和 HTTPS 环境。本地文件模式下常见问题包括：

- OpenStreetMap 地图 iframe 超时或不显示。
- 外链图片加载慢、被限制、或在微信内置浏览器里失败。
- `navigator.share` 分享接口不可用，或者只能复制本地路径。
- 微信分享本地文件时，别人打不开。

发布到 GitHub Pages 后，你会得到类似这样的链接：

```text
https://你的GitHub用户名.github.io/仓库名/
```

这个链接可以在微信里发给别人。

## 准备文件

我已经帮你准备好了 GitHub Pages 默认入口文件：

```text
outputs/index.html
```

你也可以一起上传：

```text
outputs/thailand-trip-planner.html
outputs/thailand-trip-readme.md
outputs/github-pages-guide.md
```

最少只需要上传 `index.html`。

## 方法一：全程网页操作，适合新手

### 1. 注册或登录 GitHub

打开：

```text
https://github.com
```

登录你的账号。没有账号就先注册。

### 2. 新建仓库

1. 点击右上角 `+`。
2. 选择 `New repository`。
3. Repository name 填一个英文名，例如：

```text
thailand-trip
```

4. 选择 `Public`。
5. 可以勾选 `Add a README file`。
6. 点击 `Create repository`。

注意：GitHub Free 账号使用 GitHub Pages 时，公开仓库最稳妥。

### 3. 上传文件

进入新建好的仓库页面：

1. 点击 `Add file`。
2. 点击 `Upload files`。
3. 把 `outputs/index.html` 拖进去。
4. 页面底部点击 `Commit changes`。

如果你想连说明文件一起放上去，也可以同时拖入：

```text
thailand-trip-readme.md
github-pages-guide.md
```

### 4. 开启 GitHub Pages

1. 在仓库页面点击 `Settings`。
2. 左侧找到 `Pages`。
3. 在 `Build and deployment` 下面：
   - Source 选择 `Deploy from a branch`
   - Branch 选择 `main`
   - Folder 选择 `/ (root)`
4. 点击 `Save`。

### 5. 等待发布

GitHub 通常需要几十秒到几分钟部署。官方说明里提到，变更发布最多可能需要约 10 分钟。

部署完成后，在 `Settings -> Pages` 页面会出现访问地址，一般长这样：

```text
https://你的GitHub用户名.github.io/thailand-trip/
```

点开这个地址，就能看到旅行页面。

## 方法二：用 GitHub Desktop，适合以后经常改

如果你以后想反复改路线、穿搭、图片，建议用 GitHub Desktop。

1. 安装 GitHub Desktop：

```text
https://desktop.github.com/
```

2. 登录 GitHub。
3. Clone 你的 `thailand-trip` 仓库到本地。
4. 把 `outputs/index.html` 复制到仓库文件夹根目录。
5. 在 GitHub Desktop 里填写提交信息，例如：

```text
publish trip planner
```

6. 点击 `Commit to main`。
7. 点击 `Push origin`。

只要 Pages 已经开启，之后每次 push 都会自动更新网站。

## 微信分享方式

发布成功后：

1. 用手机打开 GitHub Pages 链接。
2. 确认页面能看到地图和图片。
3. 点击微信右上角 `...` 分享给朋友或群。

页面顶部的“分享”按钮在部分手机浏览器里可用；如果微信不支持这个接口，就直接用微信右上角分享。

## 常见问题

### 页面 404

检查：

- 仓库是否是 Public。
- `Settings -> Pages` 是否选择了 `main` 和 `/ (root)`。
- 根目录是否有 `index.html`。
- 是否刚保存，还没等够几分钟。

### 打开后还是没有图片

这说明图片源在你的网络或微信浏览器里加载失败。当前页面使用外部图片链接，发布到 GitHub Pages 后会比本地稳定，但仍可能受网络影响。

更稳定的做法是：把图片下载到仓库里，例如放到 `images/` 文件夹，再把 HTML 里的图片地址改成本地相对路径：

```html
<img src="images/doi-suthep.jpg">
```

这样图片会跟网页一起从 GitHub Pages 加载。

### 地图显示超时

OpenStreetMap 在某些网络下会慢。可选方案：

- 多刷新一次。
- 改成 Google Maps 链接按钮为主。
- 如果主要给国内朋友看，可后续改成腾讯地图/高德地图链接或静态截图。

### 可以变成真正微信小程序吗

可以，但不是直接上传 HTML。真正微信小程序需要：

- 微信小程序 AppID。
- 微信开发者工具。
- 把页面改成 WXML/WXSS/JS。
- 地图改用微信 `map` 组件。
- 协作数据改用云开发数据库或后端接口。

建议先用 GitHub Pages 验证内容和路线，确认满意后再迁移成微信小程序。

## 官方参考

- GitHub Pages 创建站点：https://docs.github.com/en/pages/getting-started-with-github-pages/creating-a-github-pages-site
- GitHub Pages 发布源设置：https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site
