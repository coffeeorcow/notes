> 得益于 Github 推出的 Github Pages 功能，我们可以通过使用 Github 搭建免费的个人博客

## 预备条件

1. Github 账号
2. Git 或相关工具
3. Node 开发环境（由于运行 Hexo 需要在 Node 环境下运行）

## 搭建过程

**1 首先，在 Github 上创建一个远程仓库，远程仓库的名称为 `你github的名称.github.io`** 

**2 使用如下命令安装 Hexo 工具（博客生成工具）**

```shell
npm install -g hexo-cli
```

**3 创建博客项目**

```shell
cd <博客工程的位置>
hexo init <博客工程的名称>
cd <博客工程的名称>
npm install
```

创建完成后，指定文件夹的目录如下：

```
.
├── _config.yml  (网站的配置信息)
├── package.json  (工程的所用到的工具的配置)
├── scaffolds  (模板文件夹，就是每次新建文章的时候默认填充的内容)
├── source   (存放用户资源的地方，除了 _posts，其他开头名为 _ 的文件夹都会被忽略。Markdown 和 HTML 文件会被解析放到 public 文件夹中去)
|   ├── _drafts
|   └── _posts
└── themes   (主题文件夹，Hexo 会根据主题生成静态页面)

```

博客网站的具体配置 [详见此处]( https://hexo.io/zh-cn/docs/configuration )

**4 新建博客文章**

```shell
hexo new [layout] <title>
```

layout 布局有以下三种：

| 布局  | 路径           |
| ----- | -------------- |
| post  | source/_posts  |
| page  | source         |
| draft | source/_drafts |

如果 `layout` 是草稿，可以通过以下命令让它变成 `post`

```shell
hexo publish [layout] <title>
```

**5 如何写一篇文章？**

创建一个 MarkDown 文件，文章开头使用 `Front-matter` 定义一些文章信息，然后就想正常的 MarkDown 文件那样写就行了，下面就是一个例子：

```markdown
---
title: Hello World
date: 2013/7/13 20:46:25
---

这是你的 Markdown 内容
```

下面是 hexo 预定义的一些参数

| 参数         | 描述                                                 | 默认值       |
| :----------- | :--------------------------------------------------- | :----------- |
| `layout`     | 布局                                                 |              |
| `title`      | 标题                                                 | 文章的文件名 |
| `date`       | 建立日期                                             | 文件建立日期 |
| `updated`    | 更新日期                                             | 文件更新日期 |
| `comments`   | 开启文章的评论功能                                   | true         |
| `tags`       | 标签（不适用于分页）                                 |              |
| `categories` | 分类（不适用于分页）                                 |              |
| `permalink`  | 覆盖文章网址                                         |              |
| `keywords`   | 仅用于 meta 标签和 Open Graph 的关键词（不推荐使用） |              |

> 注意分类和标签采用如下的格式进行设置

```yaml
categories:
	- cate1
	- cate2
tags:
	- tag1
	- tag2
```

> 如果添加多个分类，使用如下方式：

```yml
categories:
	- [cate1, cate2]
	- [cate1, cate3]
```

**6 预览文章**

使用 以下命令运行博客项目，查看博文

```shell
hexo server -s
# 也可以指定端口号
hexo server -p 你的端口号 -s
```

使用以下命令生成博客项目

```shell
hexo generate
```

或者完成后部署

```shell
hexo generate --depoly
hexo depoly --generate
```

**7 将博客部署到 Github 上去**

首先需要安装一个插件 `hexo-deployer-git`

```shell
npm install hexo-deployer-git --save
```

然后新增或编辑 _config.yml 文件的以下配置：

```yaml
deploy:
  type: git
  repo: https://github.com/<username>/<project>
  branch: master
```

最后运行下面的命令进行部署：

```shell
hexo clean
hexo deploy
```

**8 博客就搭建完成了**

通过访问  `https://<username>.github.io` 地址查看你的博客

