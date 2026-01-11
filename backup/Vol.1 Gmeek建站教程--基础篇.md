# 打造属于你的 All-in-GitHub 博客：Gmeek 高阶入门、源码解析与实战教程

## 一、为什么选择 Gmeek？
想拥有一个无需运维、可高度定制、由 GitHub 驱动的现代博客？Gmeek 正是这样一个极简框架 —— 利用 Github Pages、Issues 和 Actions，无需服务器即可一站式搞定，自动生成、自动部署，开发者零负担，随时随地写博客！

---

## 二、超清晰安装流程
### Step 1：一键创建你的博客库
直接通过 Gmeek 官方模板创建仓库，推荐命名为 `你的用户名.github.io`。此举可极大简化环境搭建，模板结构见下：

```markdown
// backup/这是Gmeek模板仓库.md
通过这个模板创建库，可以大大减少部署Gmeek博客的配置步骤。
```
点击“Use this template”一键新建，再也不会踩坑！

### Step 2：GitHub Pages 配置
在仓库的 **Settings > Pages** 里，将 Build & Deployment 的 Source 指定为 Github Actions，这样才能激活自动构建流。无需关心底层静态文件部署，Gmeek 会全自动操作。

### Step 3：写文就是发 issue
每一条 issue 都会自动变身为一篇博客文章！撰写 issue 时，记得**必须添加至少一个标签 label**，如：

```
[Label] good first issue, tech, diary
```
保存 issue，几分钟后访问 `https://你的用户名.github.io`，即可见证你的文章上线。构建进度可实时通过 Actions 页面追踪。

### Step 4：全局重构与异常修复
如果你修改了配置文件 `config.json`，或遇到构建异常，只需进入 Actions > build Gmeek，点击 Run workflow，全局重新生成即可。无需再手动部署，非常智能。

---

## 三、核心源码拆解与高级定制
### 1. 主题与前端自定义
Gmeek 博客的核心页面 HTML（如下，可直接修改，体验不一样的风格）：

```html
<!-- docs/index.html -->
<!DOCTYPE html>
<html data-color-mode="light" data-dark-theme="dark" data-light-theme="light" lang="zh-CN">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width,initial-scale=1.0">
    <link href="//cdn.staticfile.org/Primer/21.0.7/primer.css" rel="stylesheet" />
    <link rel="icon" href="https://github.githubassets.com/favicons/favicon.svg">
    <!-- 主题切换脚本 -->
    <script>
    if(localStorage.getItem("meek_theme")==null){}
    else if(localStorage.getItem("meek_theme")=="dark"){document.getElementsByTagName("html")[0].attributes.getNamedItem("data-color-mode").value="dark";}
    else if(localStorage.getItem("meek_theme")=="light"){document.getElementsByTagName("html")[0].attributes.getNamedItem("data-color-mode").value="light";}
    </script>
    <meta name="description" content="Blog description">
    <title>Blog Title</title>
</head>
<!-- 页面样式可随意自定义 -->
<style>
    body{box-sizing: border-box;min-width: 200px;max-width: 900px;margin: 20px auto;padding: 45px;font-size: 16px;font-family: sans-serif;line-height: 1.25;}
    #footer {margin-top:64px; text-align: center;font-size: small;}
</style>
```

### 2. 博客文章自动生成机制
发 issue 自动生成博客页面，文章列表、标签渲染等前端内容均由 Gmeek 动态生产，对应源码示例：

```html
<!-- docs/post/zhe-shi-Gmeek-mo-ban-cang-ku.html -->
<div class="markdown-body" id="postBody"><p>通过这个模板创建库，可以大大减少部署Gmeek博客的配置步骤。</p></div>
<!-- 评论按钮自动集成 -->
<button class="btn btn-block" type="button" onclick="openComments()" id="cmButton">评论</button>
<div class="comments" id="comments"></div>
```

### 3. 评论系统自动挂载（utterances）
无需人工部署，Gmeek 已集成 utterances，只需授权 App 即可启用评论：

```js
// 评论挂载脚本片段
function openComments() {
    var script=document.createElement("script");
    script.setAttribute("src","https://utteranc.es/client.js");
    script.setAttribute("repo","你的用户名/github.io");
    script.setAttribute("issue-term","title");
    script.setAttribute("theme",localStorage.getItem("meek_theme")=="dark"?"dark-blue":"github-light");
    script.setAttribute("crossorigin","anonymous");
    script.setAttribute("async","");
    document.getElementById("comments").appendChild(script);
}
```

### 4. 博客运行天数脚本、版权信息自动显示

```js
// 自动计算网站运行天数
if(""!=""){
    var now=new Date();
    var startSite=new Date("");
    var diffDay=Math.floor((now.getTime()-startSite.getTime())/(1000*60*60*24));
    document.getElementById("year").innerHTML=now.getFullYear();
    document.getElementById("runday").innerHTML=" • "+"网站运行"+diffDay+"天"+" • ";
}
```

---

## 四、config.json 配置详解与高级技巧

`config.json` 控制博客的全部参数，格式如下，建议每次修改后都全局重构：

```json
{
    "title": "你的博客标题",
    "subTitle": "个性签名或名言",
    "avatarUrl": "https://github.githubassets.com/favicons/favicon.svg",
    "GMEEK_VERSION": "last",

    ↑ 以上是必须字段
    ↓ 以下是自定义字段，可以选择添加

    "displayTitle": "主页面展示的标题",
    "homeUrl": "http://blog.xxx.com",
    "faviconUrl": "https://github.githubassets.com/favicons/favicon.svg",
    "email": "xxx@xxx.com",
    "startSite": "01/01/2024",
    "filingNum": "",
    "onePageListNum": 30,
    "singlePage": ["about"],
    "iconList": { "music": "M0 ..." },
    "exlink": { "music": "https://music.xxx.com" },
    "commentLabelColor": "#006b75",
    "yearColorList": ["#bc4c00", "#0969da"],
    "i18n": "CN",
    "UTC": 8,
    "themeMode": "manual",
    "dayTheme": "light",
    "nightTheme": "dark_colorblind",
    "urlMode": "pinyin",
    "style": "",
    "script": "",
    "head": "",
    "allHead": "",
    "indexStyle": "",
    "indexScript": "",
    "showPostSource": 0,
    "rssSplit": "sentence",
    "bottomText": "转载请注明出处",
    "ogImage": "https://cdn.jsdelivr.net/gh/Meekdai/meekdai.github.io/logo64.jpg",
    "primerCSS": "<link href='...primer.css' rel='stylesheet' />",
    "needComment": 1
}
```
#### 关键配置表
| 参数                | 说明                               |
|---------------------|------------------------------------|
| title,subTitle      | 必填，决定博客的主副标题            |
| avatarUrl           | 必填，头像 URL                      |
| displayTitle        | 头像右侧标题，自定义或与主标题一致   |
| homeUrl             | 启用独立域名时必填                  |
| commentLabelColor   | 评论数量标签配色                    |
| yearColorList       | 年份标签配色                        |
| i18n,UTC            | 多语言与时区支持                    |
| themeMode,dayTheme  | 主题切换/主题配置                   |
| urlMode             | 文章链接生成策略                    |
| primerCSS           | 前端样式 CDN                        |
| needComment         | 是否启用评论（1为启用）             |

---

## 五、故障排查、进阶建议

- **构建失败？** 检查 issue 是否添加 label，config.json 修改后是否全局重构。可参考以下案例排查思路：
  - [案例1](https://github.com/Meekdai/Gmeek/issues/14)
  - [案例2](https://github.com/Meekdai/Gmeek/issues/18)
- **评论报错？** 按提示安装 utterances APP 即可修复，无需手动集成代码。
- **部署异常？** 关注 Actions 的日志输出，根据提示搜索相关 issue，再动手修复。

---

## 六、结语：玩转 Gmeek，构建你的技术成长新据点

Gmeek 能让你专注内容而非框架，支持无限定制和持续进阶。建议你结合官方文档与本教程深度探索，实现真正属于你的高颜值、自动化博客！

