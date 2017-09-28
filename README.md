## Github+Hexo搭建个人博客
##### 参考资料
1. [20分钟教你使用hexo搭建github博客](http://www.jianshu.com/p/e99ed60390a8)
2. [如何在不同电脑上同时写hexo博客?](http://chown-jane-y.coding.me/2017/03/15/%E5%A6%82%E4%BD%95%E5%9C%A8%E4%B8%8D%E5%90%8C%E7%94%B5%E8%84%91%E4%B8%8A%E5%90%8C%E6%97%B6%E5%86%99hexo%E5%8D%9A%E5%AE%A2%EF%BC%9F/)

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

##### 操作
###### 1、clone项目 
  ```java
	git clone git@github.com:WhiteCode2016/HexoBlog.git
	
  ```
###### 2、本地部署
  ```java
	npm install hexo
	npm install
	npm install hexo-deployer-git --save
  ```
###### 3、新建博文
  ```java
	git pull origin hexo
	hexo new "work PC test"
  ```
###### 4、本地运行查看（localhost:4000）
  ```java
	hexo server
  ```
###### 5、推送到hexo分支
  ```java
	git add .
	git commit -m "add work PC test"
	git push origin hexo
  ```
###### 6、部署到master分支
  ```java
	hexo g -d
  ```