---
title: hexo博客搭建记录v1.0
date: 2021-06-23 14:30:27
categories:
- 前端
tags:
- 前端
- 博客
---



## 🔷v1.0 简要

​    原本我写的公开文章一直是保存在简书的，但是最近在简书更新文章的时候，发现文章发表需要一段时间的审核，不能立即看到，还有一个问题是担心简书的安全性，如果哪天简书删库的了（虽然基本不可能，我的文章可能就都消失了。
<!-- more -->
​    利用Hexo来搭建博客实际上就是在本地写MarkDown文本，md文件是非常好备份的，所以安全性实际上非常好，现在写好的md文件实际上都存在了github上，我想github应该是永远不会倒闭的..

​    现在博客1.0版本已经搭建好了，我还把官方样式改成了普罗米亚的，部署在这个域名下：

​    https://www.alexiusll.top/

​    在2022年6月之前应该都是可以访问的，域名过期了可能就要考虑是否续费，还是换域名了。

​	![部署图](23-hexo博客搭建记录v1/100.png)

​	

## 📋v1.0 主要框架和技术

- 使用了一个静态的博客生成器 Hexo

官方网站：

https://hexo.io/zh-cn/

其实中文的文档内容不是很全，如果要看完全体的话请切换语言为英文。



- 主题使用了一个最主流的 Next

中文网站：

http://theme-next.iissnan.com/

应该是现在用的最多的一种主题，所以质量还是有保证，扩展性也很强。



## 📃v1.0 实现的功能

- 写博文，博文分类，归档，标签 （基于Hexo）

- 评论 （基于valine）

- 显示 阅读次数 （基于valine）

- 百度统计接入 （似乎也没什么用..可以考虑删了）

- 显示文章字数和大致阅读时间

- 修改 Next 的原生样式

  

## ❌部署过程中存在的坑

- **travis-ci 的部署文件**

  中文文档里面给的是用不了的，需要改一下branch，还有install，node_js

  配置文件：

  ```yaml
  sudo: false
  language: node_js
  node_js:
    - 14 # use nodejs v14 LTS
  cache: npm
  install:
    - yarn
  branches:
    only:
      - main # build master branch only
  script:
    - hexo generate # generate static files
  deploy:
    provider: pages
    skip-cleanup: true
    github-token: $GH_TOKEN
    keep-history: true
    on:
      branch: main
    local-dir: public
  ```



## 📕存在的问题

- 由于Hexo本质是其实是一个生成静态页面的工具，实际上是没有后台的，于是它有一些根本性的问题

  1.每次编译，所有的md文件都需要重新编译处理一次，编译速度会随着文章数量的增长而上升。所以未来有大量文章的情况下，可能会出现编译速度的问题，目前还没有看到一些好的解决方案，现在方案可以先凑合着用着。

  2.需要储存数据的场景下，例如评论，得储存在一些第三方的存储服务器上，例如Leancloud

- 对于图片的处理，Hexo官方的方案不是很好：

  在本地写md的时候，图片的url可能会制定到一个相对路径下，例如 xxx/1.png ，在本地就可以看到这个图片，没有什么问题。但是到了部署的时候，得使用url 1.png ，要去掉 xxx/ 这个前缀，要不然到了线上，这个图片就不显示。官方的意思的是我们本地写的时候应该直接就写成 1.png ，不加前缀，但是这样不是很方便，于是我加了一个国人写的插件 ： hexo-asset-link ，每次编译都要把路径重新制定一下。



## 🟠未来展望

由于Hexo搭建博客存在一些根本性的问题，未来可能采取的方案有：

1.直接搭建有后台系统的博客，但是可能得花费的时间很长，而且做的效果也不好很好

2.调研一些其他的博客系统 例如 wordpress

3.编译多个Hexo的网站，将比较老的文章放到另外一个Hexo网站中，不再进行编译

总而言之，现在的方案应该是能支持1-2年的使用了，问题还是可以慢慢的解决。
