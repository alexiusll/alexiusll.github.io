# alexiusll 的博客

使用 hexo 8.1.1 版本。

基于 [Hexo](https://hexo.io/) + [NexT](https://theme-next.js.org/) 构建的个人博客，部署于 GitHub Pages。

博客地址：https://alexiusll.github.io

## 本地开发

```bash
npm install

# 启动本地服务
npm run server

# 构建静态文件
npm run build

# 清除缓存
npm run clean

# 部署
npm run deploy
```

## 写作

新建文章：

```bash
# 如果已经全局安装 hexo
hexo new post "文章标题"

# 使用本地安装的 Hexo（无需全局安装）
npx hexo new post "《生化危机9》全成就记录"
```

文章存放于 `source/_posts/` 目录，按年月分类。
