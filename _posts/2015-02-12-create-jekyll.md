---
layout: post
title:  "Jekyll编辑功能汇总"
date:   2015-02-15 22:14:54
categories: 技术工具
excerpt: "jekyll用法汇总" 
tags: jekyll markdown 插件 github
---

* content
{:toc}

## 简介

- 使用jekyll搭建github静态页面
- 汇总各类小技巧

## 技巧汇总

### jupyter notebook
- 【2020-02-11】[Jekyll中支持Jupyter Notebook](https://www.jianshu.com/p/2857dba1c565)

**方法一** 转成markdown文件
- 将ipynb文件直接转成markdown文件
- nbconvert 命令：
```shell
ipython nbconvert jekyll_test.ipynb --to markdown
```
- 注意：转换图片会保存到jekyll_test_files, 即nb名_files文件夹
- 参考：[Linode: Display Jupyter Notebooks with Jekyll](https://www.linode.com/docs/applications/project-management/jupyter-notebook-on-jekyll/)

**方法二** 自动转html——<font color='red'>实验失败！</font>
- 用gem库：自动将ipynb转为html——更灵活
   - [Github: Jekyll Jupyter Notebook plugin](https://github.com/red-data-tools/jekyll-jupyter-notebook)
   - 安装命令：
```shell
gem install jekyll-jupyter-notebook
```
   - 改配置
```shell
# paginate 2020-2-15 增加jupyter文件自动转html功能
plugins: [jekyll-paginate,jekyll-jupyter-notebook]
```

- （1）直接生成html
   - 将notebook文件放入到_post/文件夹内, 并保持2018-01-01-titile.ipynb 类似的格式. 在执行jekyll server后, 会将ipynb转换成html格式, 会生成/2018/01/01/title/index.html.
- （2）嵌入markdown
   - 注意：ipynb文件不能像上述一样放在_post内, 否则转换后不能使用
   - 嵌入命令：

```shell
\{\% jupyter_notebook "/notebook/sample.ipynb" \%\}
```

- 出错：jekyll 3.8.5 Error:  invalid byte sequence in GBK
- 解决：设置编码, [Jekyll在Windows下面中文编码问题解决方案](https://www.cnblogs.com/aleda/articles/Jekyll-in-Windows-following-Chinese-encoding-problem-solutions.html)，引发原有文章编译问题
- 结论：不管用！


### Markdown使用
* [github官方markdown指南](https://guides.github.com/features/mastering-markdown/ "英文版")
* [github readme语法简介](http://blog.csdn.net/guodongxiaren/article/details/23690801?utm_source=tuicool&utm_medium=referral "跟一般markdown语法不同")
* [MarkDown语法笔记（完整版）](http://blog.csdn.net/witnessai1/article/details/52551362)
* [马克飞象markdown语法在线测试](https://maxiang.io/ "可以在线测试MD语言！")


### 编辑功能
- 注释

> 注释在此。。。

- 代码高亮

```python
import os
print "hello"
```
- 字体大小
   - <font size=2>二号字尺寸式样 </font> 
- **加粗**, *斜体*
- <font color='green'>彩色字体</font>


### 图片嵌入

- 默认方法
   - ![](https://img3.doubanio.com/lpic/s28012945.jpg)
- 限制大小
   - <img src="https://img3.doubanio.com/lpic/s28012945.jpg" height="100%" width="100" />

- 【2020-6-20】如何插入自己的图片？[Jekyll博客中如何用相对路径来加载图片？](https://www.zhihu.com/question/31123165)
   - 不要在\_posts下面建立目录，在根目录,也就是 yourname.github.io/ 下面建立一个新目录pics放图片。
   - 然后引用即可。 
```html
<figure>
   <a><img src="{{site.url}}/pics/branch.png"></a>
</figure>

或者：

![](pics/xxxx)

```

### 公式嵌入
* [Latex在线调试](https://latexbase.com/)，[吴文中数学公式编辑器](http://latex.91maths.com/)，公式在线编辑，所见所得，支持图片输出

- Github自带公式显示LaTeX，[LATEX数学公式基本语法](https://www.cnblogs.com/houkai/p/3399646.html)

$$f \left( x _ { n + 1 } \right) - f \left( x _ { n } \right) = f ^ { \prime } \left( x _ { n } \right) \left( x _ { n + 1 } - x _ { n } \right)$$

- 知乎提供公式生成图片服务：https://www.zhihu.com/equation?tex=y+%3D+%5Cphi%28%5Csum+W_%7Bij%7DX_j+%2B+b%29+
- 效果：

![](https://www.zhihu.com/equation?tex=y+%3D+%5Cphi%28%5Csum+W_%7Bij%7DX_j+%2B+b%29+)



### 视屏嵌入
---
【2019-04-29】嵌入视频

代码：

```html
<iframe src="//player.bilibili.com/player.html?aid=26722471&cid=45968926&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"  height="600" width="100%"> </iframe>
```

- 超级工程

<iframe src="//player.bilibili.com/player.html?aid=26722471&cid=45968926&page=1" scrolling="no" border="0" frameborder="no" framespacing="0" allowfullscreen="true"  height="600" width="100%"> </iframe>

- [网易云课堂](http://open.163.com/movie/2006/1/1/9/M6HV755O6_M6HV8DF19.html)

代码：

```html
<object width="640" height="360"><param name="movie" value="//open.163.com/openplayer/-M6HV755O6-M6HV8DF19-http://open-image.nosdn.127.net/a5954850efaf429189dd8247a999be22.jpg-openPlayer.swf?isUserAutoPlay=1"></param><param name="allowScriptAccess" value="always"></param><param name="wmode" value="transparent"></param><embed src="//open.163.com/openplayer/-M6HV755O6-M6HV8DF19-http://open-image.nosdn.127.net/a5954850efaf429189dd8247a999be22.jpg-openPlayer.swf?isUserAutoPlay=1" type="application/x-shockwave-flash" width="640" height="360" allowFullScreen="true" wmode="transparent" allowScriptAccess="always"></embed></object>
```


---

### 脑图嵌入
- processon

```html
<iframe id="embed_dom" name="embed_dom" frameborder="0" style="display:block;width:700px; height:900px;" src="https://www.processon.com/embed/mind/581dee8ee4b0c6fe57213cd9"></iframe>
```

- xmind脑图
   - 【2019-08-02】[xmind图](https://www.xmind.net/m/YPMsKe/#)

```html
<iframe src='https://www.xmind.net/embed/YPMsKe/' width='750' height='540' frameborder='0' scrolling='no' allowfullscreen="true"></iframe>
```

<iframe src='https://www.xmind.net/embed/T9Nm/' width='750' height='540' frameborder='0' scrolling='no' allowfullscreen="true"></iframe>

### 访问统计
- 国外的插件

代码

```html
<script type="text/javascript" src="//rf.revolvermaps.com/0/0/1.js?i=5q2837r7gjo&amp;s=265&amp;m=7&amp;v=true&amp;r=false&amp;b=000000&amp;n=false&amp;c=ff0000" async="async"></script>
```

- [不蒜子](http://busuanzi.ibruce.info/) 静态站点统计, 两行代码搞定
![](http://busuanzi.ibruce.info/images/garlic.png)

```html
<script async src="//busuanzi.ibruce.info/busuanzi/2.3/busuanzi.pure.mini.js"></script>
<span id="busuanzi_container_site_pv">本站总访问量<span id="busuanzi_value_site_pv"></span>次</span>
```




### 评论插件

- 评论插件 [Share.js](https://github.com/overtrue/share.js/)，一键分享到微博、QQ空间、QQ好友、微信、腾讯微博、豆瓣、Facebook、Twitter、Linkedin、Google+、点点等

![](https://cloud.githubusercontent.com/assets/1472352/11433126/05f8b0e0-94f4-11e5-9fca-74dc9d1b633f.png)

- 来必力，源自韩国

```html
<!-- 来必力City版安装代码 -->
<div>
    <script type="text/javascript">
           (function(d, s) {
               var j, e = d.getElementsByTagName(s)[0];
               if (typeof LivereTower === 'function') { return; }
               j = d.createElement(s);
               j.src = 'https://cdn-city.livere.com/js/embed.dist.js';
               j.async = true;
               e.parentNode.insertBefore(j, e);
           })(document, 'script');
   </script>
   <noscript> 为正常使用来必力评论功能请激活JavaScript</noscript>
</div>
<!-- City版安装代码已完成 -->
```

#### [GitMent评论系统](https://frankjkl.github.io/2019/01/08/blogbuild-在Jekyll博客添加gitment评论系统)

本文章转载于http://xichen.pub/2018/01/31/2018-01-31-gitment/，并在其基础上进行完善

##### 1、注册

- 在[setting - OAuth Application 注册页面](https://github.com/settings/applications/new)完成注册

```
Application Name: gitment评论 //随便填
Homepage Url: https://frankjkl.github.io //博客的域名
Application description: //随便填，留空也可以
Authorization Callback URL: https://frankjkl.github.io //一定要写自己Github Pages的URL
```

注册成功后会得到`Client ID`和`Client Secret`


##### 2、在jekyll博客调用gitment

如gitment项目页Readme所示，在你需要添加评论系统的地方，一般是`_layout/`目录下的 `post.html`, 添加一下代码

```javascript
<div id="container"></div>
<link rel="stylesheet" href="https://jjeejj.github.io/css/gitment.css">
<script src="https://jjeejj.github.io/js/gitment.js"></script>
<script>
var gitment = new Gitment({
  id: '\{\{ page.date \}\}', #对应文章评论所形成issue的label，默认为文章的url,为了防止url过长导致评论初始化失败，这里设置label为文章yaml中的时间。这一项无需更改，\为转义字符，应用时需要删掉
  owner: 'FrankJKL', #Github Pages博客所在的github账户名
  repo: 'FrankJKL.github.io', #Github Pages博客所在仓库名
  oauth: {
    client_id: 'xxxxxxx', #第1步所申请到的Client ID
    client_secret: 'xxxxxxxxxx',#第1步所申请到的Client Secret
  },
})
gitment.render('container')
</script>
```

填写完上面的内容，把代码保存上传到github就可以了。

##### 3、为每篇博文初始化评论系统

由于gitment的原理是为每一篇博文以其YAML中的标题作为标识创建一个github issue， 对该篇博客的评论就是对这个issue的评论。因此，我们需要为每篇博文初始化一下评论系统，初始化后，会在你的github上会创建相对应的issue。

接下来，介绍一下如何初始化评论系统

1. 上面第2步代码添加成功并上传后，你就可以在你的博文页下面看到一个评论框，还有看到以下错误`Error: Comments Not Initialized`，提示该篇博文的评论系统还没初始化

   ![1546944230319](https://frankjkl.github.io/assert/1546944230319.png)

2. 点击`Login with GitHub`后，使用自己的github账号（必须跟第二步owner用户名相同的账号）登录后，就可以在上面错误信息处看到一个`Initialize Comments`的按钮

   ![](https://jacobpan3g.github.io/img/gitment-in-jekyll.png)

3. 点击`Initialize Comments`按钮后，就可以开始对该篇博文开始评论了， 同时也可以在对应的github仓库看到相应的issue

   ![1546944090342](https://frankjkl.github.io/assert/1546944090342.png)



##### 遇到的一些坑

###### Error：NOT FOUND

owner或者repo配置错误了，照着第二步来就好，网页端生成后如下

```javascript
<script>
    var gitment = new Gitment({
        id: '\{\{ page.date \}\}', #\为转义字符，应用时需要删掉
        owner: 'FrankJKL',
        repo: 'FrankJKL.github.io',
        oauth: {
            client_id: 'xxxxxxxx',
            client_secret: 'xxxxxxxxxxxxxxxxxxxxxxxxx',
        },
    })
    gitment.render('container')
</script>
```



###### Error: Comments Not Initialized

- 在步骤一中，给`Authorization callback URL`指定的地址错了
- 还没有在该页面的Gitment评论区登陆GitHub账号

###### Object ProgressEvent

最近gitment作者的服务器过期了，所以登陆GitHub时一直报Object ProgressEvent。我在本文第二步添加的gitment代码是没有这个问题的。

解决：

将`_layout/post.html`中gitment的代码：

```javascript
<link rel="stylesheet" href="//imsun.github.io/gitment/style/default.css">
<script src="//imsun.github.io/gitment/dist/gitment.browser.js"></script>
```

修改为

```javascript
<link rel="stylesheet" href="https://jjeejj.github.io/css/gitment.css">
<script src="https://jjeejj.github.io/js/gitment.js"></script>
```

或

```javascript
<link rel="stylesheet" href="https://jjeejj.github.io/css/gitment.css">
<script src="https://www.wenjunjiang.win/js/gitment.js"></script>
```

登陆时就不会再报错了，这是别人新搭建的服务器。参考https://github.com/jjeejj/jjeejj.github.io/issues/8

###### Error：validation failed

**发生时间：**评论的初始化时

原因：由于gitment的评论是基于GitHub issue的，所以评论初始化时，会生成文章对应的issue，以及通过https://jjeejj.github.io/js/gitment.js 生成issue的label。其中的labels有两个，一个是gitment，另一个就是文章的URL，但是label的最大长度限制是50个字符，而我们的URL中包含域名与文章名，有时会超出限制。所以才会发生validation failed

**解决：**

gitment.js中`labels: labels.concat(['gitment', id])`id默认为`window.location.href`也就是文章的URL，这里的id的作用是每篇文章的评论是要根据id动态加载的，写死的话导致所有的文章共享一个issue。参考前面第二步中将id修改为`'\{\{ page.date \}\}'\为转义字符，应用时需要删掉`，就可以覆盖gitment.js中的id。这样传给github issue的label是定长的，不会超过长度限制。同时`date`可以自己写，只要精确到分秒，区分文章不是问题。Good job!

- PS：一个date的例子：`date: 2019-01-07 00:00:00 +0000` 这个date是写到文章顶部的YAML中
- PS：[xjzsq](https://github.com/xjzsq)的方法也很好，思想是用副标题作id，可以看下[他的文章](http://www.xjdesyxx.top/2018/02/07/errsln/)

参考https://github.com/imsun/gitment/issues/118


### 分享插件

- 采用百度分享

```html
<div class="bdsharebuttonbox">
    <a href="#" class="bds_more" data-cmd="more"></a>
    <a href="#" class="bds_weixin" data-cmd="weixin" title="分享到微信"></a>
    <a href="#" class="bds_qzone" data-cmd="qzone" title="分享到QQ空间"></a>
    <a href="#" class="bds_tsina" data-cmd="tsina" title="分享到新浪微博"></a>
    <a href="#" class="bds_tqq" data-cmd="tqq" title="分享到腾讯微博"></a>
</div>
<script>window._bd_share_config={"common":{"bdSnsKey":{},"bdText":"鹤啸九天的技术博客","bdMini":"2","bdMiniList":false,"bdPic":"http://news.zx123.cn/uploadfile/news68/1800961ad02811e7b1c400163e010ef1.jpg","bdStyle":"0","bdSize":"32"},"share":{},"image":{"viewList":["qzone","tsina","tqq","renren","weixin"],"viewText":"分享到：","viewSize":"32"},"selectShare":{"bdContainerClass":null,"bdSelectMiniList":["qzone","tsina","tqq","renren","weixin"]}};with(document)0[(getElementsByTagName('head')[0]||body).appendChild(createElement('script')).src='http://bdimg.share.baidu.com/static/api/js/share.js?v=89860593.js?cdnversion='+~(-new Date()/36e5)];
</script>
```
- 【2019-11-05】直接使用[Share工具](https://github.com/overtrue/share.js), 添加以下代码即可

![](https://cloud.githubusercontent.com/assets/1472352/11433126/05f8b0e0-94f4-11e5-9fca-74dc9d1b633f.png)

```html
<!-- https://github.com/overtrue/share.js -->
<div class="social-share"></div>
<!--  css & js -->
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/social-share.js/1.0.16/css/share.min.css">
<script src="https://cdnjs.cloudflare.com/ajax/libs/social-share.js/1.0.16/js/social-share.min.js"></script>
```


### 打赏

- 参考：[jekyll下添加打赏功能](http://www.twistedwg.com/2018/05/06/jekyll-reward.html)
- 步骤：
   - 下载css文件，保存到jekyll里的css/myrewards.css
   - 准备支付二维码图片，放到自定义文件夹里，如wqw/fig/wqw.png
   - _include/head.html添加css文件：（注意：需要修改主目录地址）
   
```html
<link href="{{ "/css/myreward.css " | prepend: site.baseurl }}" rel="stylesheet" type="text/css">
_layout/post.html添加插件
    <!-- 【2019-08-06】打赏功能,  http://www.twistedwg.com/2018/05/06/jekyll-reward.html-->
    <div class="reward">
		<div class="reward-button">赏 <span class="reward-code">
			<span class="alipay-code"> <img class="alipay-img wdp-appear" src="/assets/wqw/fig/alipay.png"><b>支付宝打赏</b> </span>
			<span class="wechat-code"> <img class="wechat-img wdp-appear" src="/assets/wqw/fig/wechatpay.png"><b>微信打赏</b> </span> </span>
		</div>
		<p class="reward-notice">您的打赏是对我最大的鼓励！</p>
	</div>
```

### 文档搜索

- [Jekyll 静态博客实现搜索功能](https://juejin.im/post/5aa7d9c6f265da23866f918e)
   - 提前安装[Simple-Jekyll-Search](https://github.com/christian-fei/Simple-Jekyll-Search)
![](https://user-gold-cdn.xitu.io/2018/3/13/1621faaa92d3cae7?imageslim)


### 加地图插件

- [如何加百度地图插件](http://www.shejidaren.com/tian-jia-baidu-di-tu-dai-ma.html)

## Jekyll语法

- [Jekyll 语法简单笔记](http://github.tiankonguse.com/blog/2014/11/10/jekyll-study.html)
- 【2018-6-10】[github page jeklly主题](https://github.com/Gaohaoyang/gaohaoyang.github.io/blob/master/README-zh-cn.md)
- 【2019-04-29】[Jeklly主题大全](http://jekyllthemes.org/)

- [Jekyll](https://jekyllrb.com/)中的配置和模板语法



## 搭建过程

在jekyll的官网上 [http://jekyllrb.com/](http://jekyllrb.com/) 其实已经说得比较明白了，我在这里还是简单的说一下吧。我用的是Windows系统。    
主要环节有：安装Ruby，安装RubyGems，安装jekyll，安装代码高亮插件，安装node.js

### 安装Ruby

- ruby官网下载安装：[https://www.ruby-lang.org/en/downloads/](https://www.ruby-lang.org/en/downloads/)
- 安装完成后配置环境变量
- 在命令提示符中，得到ruby版本号，如下图，即安装成功

![](http://ww4.sinaimg.cn/large/7011d6cfjw1f2ue0e393vj20cu00t748.jpg)

### 安装RubyGems

官网下载 [http://rubygems.org/pages/download](http://rubygems.org/pages/download) rubygems-2.4.5.zip   

cd到RubyGems目录   

![](http://ww1.sinaimg.cn/large/7011d6cfjw1f2ue1l2yscj20gk02amxj.jpg)

执行安装   

![](http://ww1.sinaimg.cn/large/7011d6cfjw1f2ue1w8eqnj20bx00hglg.jpg)  

### 用RubyGems安装Jekyll

执行下面的语句安装   

![](http://ww4.sinaimg.cn/large/7011d6cfjw1f2ue2g2p3uj207x00ft8j.jpg)

安装结束画面   

![](http://ww4.sinaimg.cn/large/7011d6cfjw1f2ue32drwhj20hv09xq5m.jpg)

至此jekyll就已经安装完毕了，后续就是个性化的自己设定了。

### 创建博客

在d盘新建一个工作区jekyllWorkspace

cd到jekyllWorkspace   

执行jekyll new name创建新的工作区   

![](http://ww3.sinaimg.cn/large/7011d6cfjw1f2ue3lt31nj20cj02nt8u.jpg)

文件结构如下：   

![](http://ww1.sinaimg.cn/large/7011d6cfjw1f2ue3ujsybj20ek06wabh.jpg)

cd到博客文件夹，开启服务器   

![](http://ww1.sinaimg.cn/large/7011d6cfjw1f2ue47y9lgj20ao00f0sl.jpg)

watch为了检测文件夹内的变化，即修改后不需要重新启动jekyll

我的环境下启动报错(你的可能没有)，再安装yajl-ruby和rouge  

![](http://ww4.sinaimg.cn/large/7011d6cfjw1f2ue4nelnxj20dd077q49.jpg)

再次启动服务器成功

![](http://ww4.sinaimg.cn/large/7011d6cfjw1f2ue4v42koj20g505bdgy.jpg)

访问 http://localhost:4000/   

![](http://ww1.sinaimg.cn/large/7011d6cfjw1f2ue56ckwoj20je0eumz3.jpg)

详细文章页面   

![](http://ww2.sinaimg.cn/large/7011d6cfjw1f2ue5f3j9cj20je0gyq7a.jpg)

## 后续

*  整个安装过程参考了jekyll官网，注意jekyll还有一个简体中文官网，不过比较坑（我就被坑了），有些内容没有翻译过来，有可能会走弯路，建议如果想看中文的相关资料，也要中英对照着阅读。[jekyll中文网 http://jekyllcn.com](http://jekyllcn.com), [jekyll英文网 http://jekyllrb.com](http://jekyllrb.com)
*  jekyll中的css是用sass写的，当然直接在`_sass/_layout.scss`中添加css也是可以的。
*  本文是用Markdown格式来写的，相关语法可参考： [Markdown 语法说明 (简体中文版) http://wowubuntu.com/markdown/](http://wowubuntu.com/markdown/)  
*  按照本文的说明搭建完博客后，用`github Pages`托管就可以看到了。注意，在github上面好像不支持rouge，所以要push到github上时，我将配置文件_config.yml中的代码高亮改变为`highlighter: pygments`就可以了
*  博客默认是没有评论系统的，本文的评论系统使用了多说，详细安装办法可访问[多说官网 http://duoshuo.com/](http://duoshuo.com/)，当然也可以使用[搜狐畅言 http://changyan.sohu.com/](http://changyan.sohu.com/)作为评论系统。
*  也可以绑定自己的域名，如果没有域名，可以在[godaddy http://www.godaddy.com/](http://www.godaddy.com/)上将域名放入购物车等待降价，买之。
*  祝各位新年快乐！

---

# 可能出现的问题

### `hitimes/hitimes (LoadError)`

**错误代码：**

```
C:/Ruby22/lib/ruby/2.2.0/rubygems/core_ext/kernel_require.rb:54:in `require': cannot load such file -- hitimes/hitimes (LoadError)
```

**解决方法：**

在stackoverflow上又一个很好的解决方法。[hitimes require error when running jekyll serve on windows 8.1](http://stackoverflow.com/questions/28985481/hitimes-require-error-when-running-jekyll-serve-on-windows-8-1) 虽然上面的题主问的是 win 8.1 系统下的情况，但是同样适用于 win7。下面我简单翻译一下错误原因和解决方法。

> 可能是 Ruby 2.2 和 hitimes-1.2.2-x86-mingw32 中有一些 ABI 变化，少了一些相关的类库。
>
> 所以卸载 hitimes 并通过 `--platform ruby` 重装即可。代码如下：

```
gem uni hitimes
**Remove ALL versions**
gem ins hitimes -v 1.2.1 --platform ruby
```

> 然后将自动重新编译 hitimes 并适用于 Ruby 2.2

下面是我自己的卸载和安装过程：

```
E:\GitWorkSpace\gaohaoyang.github.io>gem uni hitimes

You have requested to uninstall the gem:
        hitimes-1.2.2-x86-mingw32

timers-4.0.1 depends on hitimes (>= 0)
If you remove this gem, these dependencies will not be met.
Continue with Uninstall? [yN]  y
Successfully uninstalled hitimes-1.2.2-x86-mingw32

E:\GitWorkSpace\gaohaoyang.github.io>gem ins hitimes -v 1.2.1 --platform ruby
Fetching: hitimes-1.2.1.gem (100%)
Temporarily enhancing PATH to include DevKit...
Building native extensions.  This could take a while...
Successfully installed hitimes-1.2.1
Parsing documentation for hitimes-1.2.1
Installing ri documentation for hitimes-1.2.1
Done installing documentation for hitimes after 1 seconds
1 gem installed
```


关于，[hitimes](https://rubygems.org/gems/hitimes/versions/1.2.2) 是一个快速的高效的定时器解决方案库，详情可以去官网查看。



