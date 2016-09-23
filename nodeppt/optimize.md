title: 浅谈前端性能优化
speaker: 汪洋
url: https://github.com/ksky521/nodePPT
transition: vertical3d
theme: moon
files: /js/demo.js,/css/demo.css

[slide]

# 浅谈前端性能优化
## 演讲者：汪洋

[slide data-transition="circle"]

# 目的 {:&.flexbox.vleft}
## 让大家了解我们是如何从前端层面针对页面加载速度进行性能优化的

[slide data-transition="zoomin"]
# 为什么要进行前端性能优化
[magic data-transition="earthquake"]
-----
![](http://odde4a116.bkt.clouddn.com/images/q.jpg)
=====
* 用户方面  {:&.rollIn}
###### 打开速度快，操作响应及时，体验友好

* 服务器方面
###### 减少页面请求数以及带宽，节省资源用来下片
<img src="http://odde4a116.bkt.clouddn.com/cls.png" width='386' height='69'>
[/magic]

[slide data-transition="glue"]
# 如何测试网站的性能
[magic data-transition="cover-circle"]
## PageSpeed {:&.flexbox.vleft}
-----
<img src="http://odde4a116.bkt.clouddn.com/pagespeed.png" width='949' height='486'>
=====
## PageSpeed Insights {:&.flexbox.vleft}
-----
> https://developers.google.com/speed/pagespeed/insights/

<img src="http://odde4a116.bkt.clouddn.com/p.png" width='949' height='486'>
=====
## YSlow {:&.flexbox.vleft}
-----
<img src="http://odde4a116.bkt.clouddn.com/y.png" width='1920' height='525'>
=====
## WebPagetest {:&.flexbox.vleft}
-----
> https://www.webpagetest.org/

<img src="http://odde4a116.bkt.clouddn.com/WebPage.png" width='1920' height='525'>
=====
## Network {:&.flexbox.vleft}
-----
<img src="http://odde4a116.bkt.clouddn.com/console.png" width='1920' height='525'>
=====
[/magic]

[slide data-transition="move"]
[magic data-transition="cover-circle"]
# 如何优化加载过慢的页面 {:&.flexbox.vleft}
* 静态资源压缩混淆 {:&.bounceIn}
* 减少http请求数
* 模块化管理
* http缓存
* 图片懒加载
[/magic]

[slide]
# 静态资源压缩混淆 {:&.flexbox.vleft}
[magic data-transition="zoomin"]
## 自动化工具gulp
-----
```
gulp.task('jsmin',function(){
	return gulp.src(sourcePath+'.js')
	.pipe(uglify({
		mangle:false,
		compress:false
	}))
	.pipe(gulp.dest(targetPath));
});
```
=====
## 压缩前的js文件
-----
![](http://odde4a116.bkt.clouddn.com/before.png)
=====
## 压缩后的js文件
![](http://odde4a116.bkt.clouddn.com/after.png)
[/magic]

[slide data-transition="pulse"]
# 减少http请求数 {:&.flexbox.vleft}
[magic data-transition="circle"]
## seajs-combo
-----
> 需要配合服务器的 nginx-http-concat 服务

```
location /static/css/ {
    concat on;
    concat_max_files 20;
}

location /static/js/ {
    concat on;
    concat_max_files 30;
}
```
=====
## 合并前的js文件
-----
![](http://odde4a116.bkt.clouddn.com/cbbefore.png)
![](http://odde4a116.bkt.clouddn.com/rebefore.png)
=====
## 合并后的js文件
![](http://odde4a116.bkt.clouddn.com/cbafter.png)
![](http://odde4a116.bkt.clouddn.com/reafter.png)
[/magic]

[slide]

# 模块化管理
seajs

[slide]
# 按需加载
[magic data-transition="newspaper"]
-----
![](http://odde4a116.bkt.clouddn.com/jz.png)
=====

-----
```
// a.js
define(function(require, exports) {

	var doSomething = function(){
		// xxx代码
	}  

});
```
=====

```
// b.js
define(function(require, exports) {

	// 获取模块 a 的接口
  var a = require('./a');

  // 调用模块 a 的方法
  a.doSomething();

});
```
[/magic]

[slide]

# 图片懒加载 {:&.flexbox.vleft}
[magic data-transition="horizontal"]
------
> 当访问一个页面的时候，先把img元素或是其他元素的背景图片路径替换成一张大小为1*1px图片的路径（这样就只需请求一次），只有当图片出现在浏览器的可视区域内时，才设置图片正真的路径，让图片显示出来。这就是图片懒加载。
<img src="http://odde4a116.bkt.clouddn.com/load.png" width="550" height="660" />
======

<img src="http://odde4a116.bkt.clouddn.com/150946520643678.gif" width="100" height="100" />

```
// html
<img src="菊花.gif" data-src="xxx.jpg" alt="">

// js
$('xxx').live('scroll',function(){
	var imgSrc = $('xxx').attr('data-src');	//获取图片真是路径
	$('xxx').attr('src',imgSrc);	//设置图片路径
})

// lazy-load
$('img').LazyLoad({
    container: window,
    event:'scroll',
    effect: 'show',
    effectArgs: 'slow',
    loadImg:'loading.gif',
    load: null,
    offset: 0
});
```
[/magic]

[slide]

# Thanks
