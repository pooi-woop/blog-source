---
title: hexo-butterfly添加头图的方法暨测试
tags: 测试,hexo,Butterfly,博客,头图
cover: img/9fde1f954a608ba02a492108e6e13a2972233788 .jpg
banner: img/9fde1f954a608ba02a492108e6e13a2972233788 .jpg
date: 2026-03-18 18:00:33
---

# hexo-butterfly添加头图的方法暨测试
## 大多数现代 Hexo 主题都支持在文章 Front-matter 中配置 cover 和 banner 图片。
---
title: 文章标题
date: 2024-01-01 12:00:00
### 头图配置
cover: /images/cover.jpg        # 封面图路径
banner: /images/banner.jpg      # 顶部大图（部分主题用 banner）
thumbnail: /images/thumb.jpg   # 缩略图（列表页显示）
photos:                        # 相册模式（部分主题）
  - /images/pic1.jpg
  - /images/pic2.jpg
---
## 图片路径说明
方式1：绝对路径（推荐，以 / 开头，基于 source 目录）
cover: /images/2024/cover.jpg

方式2：相对路径（与文章同目录）
cover: cover.jpg

方式3：使用图床/外链
cover: https://cdn.example.com/image.jpg
# 目录结构示例
source/
├── _posts/
│   └── my-post.md
└── images/
    └── 2024/
        └── cover.jpg
        └── banner.jpg
        └── thumb.jpg
        └── pic1.jpg
        └── pic2.jpg



饿了饿了,赶紧测试完下去吃完饭
