### LeetCode

> 项目地址：[xxx](https://xxx.com)

```
*/***
* *   Title
* * Description
* * 
* ****@param***l1*

* ****@return**
**/*
You code
```


### Review

- 原文地址：[Article](http://xx.com/)

> 最好的语言需要一些情形

- 是否需要性能
- 生态系统如何
- 社区如何，出现问题是否容易解决
- 团队的技能是什么
- 商业选择

> 最后结论：A programming language is just a tool; what matters is the way you overcome your problems
> 程序语言仅仅是工具，重要的是解决你的问题

### T：技术技巧

> 学习Http相关的知识：先列一个目录
> 参考：
> 1. Http权威指南
> 2. 网络资料


 Http基础知识
	- Http发展历程
	- 基本网络模型
	- 三次握手
	- URL/URI/URN
	- 报文格式
- Http特性
	- Http客户端
	- 跨域
	- Cros跨域请求
	- Cache
	- 缓存验证Last-Modified和ETag的使用
	- Cookie和Session
	- 长连接
	- 内容协商
	- Redirect
	- CSP


### Share：分享


- Git中基于Rebase的工作流

> 基于master拉取分支dev

![flow](http://p783z0zp1.bkt.clouddn.com/img/20180621210934.png)

> dev分支commit2次

![dev commit](http://p783z0zp1.bkt.clouddn.com/img/20180621213049.png)

> origin/master修改，master分支pull
> 可以看到master分支从commit C8之后加了一个commit A1

![origin/master](http://p783z0zp1.bkt.clouddn.com/img/20180621213221.png)

> 切换到dev分支，rebase onto master

![dev分支移动到了master commit之后](http://p783z0zp1.bkt.clouddn.com/img/20180621213421.png)

> 切换到master分支, rebase onto dev
> master分支指针指到dev，dev分支的commit没了

![master分支指针指到dev，dev分支删除](http://p783z0zp1.bkt.clouddn.com/img/20180621213545.png)

> push，将master和origin/master同步

![push](http://p783z0zp1.bkt.clouddn.com/img/20180621213707.png)

> 视频地址

- [A better Git workflow with rebase - YouTube](https://www.youtube.com/watch?v=f1wnYdLEpgI)


### 总结这周工作内容

> 本周主要做了如下事情：

- 健身
- 基本工作内容
- 深入学习Http
- 了解机器学习
- 学习设计模式

> 健身

从今年年初开始健身，身体明显发生了一些改变，主要改变有几点：
- 去年跑3公里就不想跑了，今年跑10公里也不怎么累
- 长跑中锻炼心态，逼迫自己不要太着急，慢点慢点

> 工作内容

- 在开发过程中重构了一个接口，但是因为在之前没有做出设计，在过代码的时候被否，也给自己一些思考

> 深入学习Http

- Http用的很多，但是了解的也很基础，之前看了一遍`图解Http`但是没有总结，这次深入学习，学习Http，给自己的目标是写一篇或者多篇高质量的Http文章
- 网络中，特别是TCP的一些策略还是比较值得学习

> 了解机器学习

- 机器学习在一些特定的领域还是比较有发展，有些代码不太好解决的问题机器学习很方便的可以解决，先了解下

> 学习设计模式
> 推荐书籍：

- 图解设计模式
- 大话设计模式
- 重构
- 重构与模式
````