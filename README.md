# 我的博客

欢迎访问：👆 [https://www.laoliang.ink](https://www.laoliang.ink)

这是一个基于 博客框架 [Hexo](https://hexo.io/zh-cn/) 构建的静态博客生成项目

除了 Hexo，还应用到了以下资源：

- Hexo 主题：[volantis](https://volantis.js.org/)
- 无后台评论系统：[valine](https://valine.js.org/)

在此感谢相关资源作者 👍

## 开始

清除缓存文件 (db.json) 和已生成的静态文件 (public)

```sh
npm run clean
```

生成静态文件

```sh
npm run build
```

启动本地服务器预览（默认启动在： http://localhost:4000/）

```sh
npm run server
```

部署网站

```sh
npm run deploy
```

## 写作

新建一篇文章

```sh
npm run new "文章标题"
```
