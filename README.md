---

## 新建文章

两种方式

### 1、使用 hexo 命令

若要使用hexo，需要首先安装 nodejs 等，安装方式：

nodejs 安装参看官方页面介绍：[nodejs.org](https://nodejs.org/en/)，推荐安装LTS(长期维护稳定版)版本。

拉取我们的文档项目，执行初始化

```bash
# 拉取项目
git clone git@github.com:syuanyuan708/blog.git
# 进入项目 && 初始化依赖
cd blog && yarn install
```

本地创建文章

```bash
yarn hexo new "post title with whitespace"
```

本地启动服务

```bash
yarn hexo server -l
```

更多hexo命令参看：[Hexo 指令](https://hexo.io/zh-cn/docs/commands)

### 2、手动创建

在 `./source/_posts/` 目录下创建新文章的 markdown 即可
