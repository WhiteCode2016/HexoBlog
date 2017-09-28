---
title: Github+Hexo搭建个人博客
date: 2017-08-31 11:15:23
categories: 配置
---
##### 参考资料
1. [20分钟教你使用hexo搭建github博客](http://www.jianshu.com/p/e99ed60390a8)
2. [如何在不同电脑上同时写hexo博客?](http://chown-jane-y.coding.me/2017/03/15/%E5%A6%82%E4%BD%95%E5%9C%A8%E4%B8%8D%E5%90%8C%E7%94%B5%E8%84%91%E4%B8%8A%E5%90%8C%E6%97%B6%E5%86%99hexo%E5%8D%9A%E5%AE%A2%EF%BC%9F/)
<!-- more -->
##### 代码仓库
- [github](http://www.github.com)
- [coding](http://www.coding.net) 

##### 主题和第三方插件
1. 主题：[Next](http://theme-next.iissnan.com/getting-started.html)
2. 评论：[LiveRe(来必力)](http://www.laibili.com.cn)
3. 分享：[JiaThis](http://www.jiathis.com/)
4. 统计：[LeanCloud](https://leancloud.cn)
5. 搜索：[algolia](https://www.algolia.com)
6. 图片存储：[七牛云](https://portal.qiniu.com)
7. RSS

##### 细节
1. 圆形头像
	修改主题next\source\css\_common\components\sidebar\sidebar-author.styl
  ```css
	.site-author-image {
	  display: block;
	  margin: 0 auto;
	  padding: $site-author-image-padding;
	  max-width: $site-author-image-width;
	  height: $site-author-image-height;
	  border: $site-author-image-border-width solid $site-author-image-border-color;
	  /*头像圆形*/
	  border-radius: 80px;
	  -webkit-border-radius: 80px;
	  -moz-border-radius: 80px;
	}
  ```
2. 七牛云存储图片
	- [使用七牛为Hexo存储图片等资源](https://yuchen-lea.github.io/2016-01-21-use-qiniu-store-file-for-hexo/)