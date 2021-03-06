# 移动端手势与双指缩放

上周遇见一个双指缩放的问题，同时这个双指缩放也比较常见，于是决定对移动端手势做一个学习和总结，并给出一个双指缩放的实例，希望对读者提供一些帮助。
## 前言

当年乔布斯的iphone第一次支持多点触控时，确实惊艳了世人，而现在大部分手机都支持多点触控，这就有了手势这个概念，通过多点触控，形成不同的手势，开发者根据不同手势，提供不同功能，比如双指缩放，是很常见的。

### ios的多点触摸

ios的Safari浏览器是第一个支持多点触摸的浏览器，并提供触摸API供开发者使用，到后来Android 3也开始支持多点触摸，各大浏览器也借鉴Safari提出了触摸API，除了个别硬件支持属性外，大致相同，这是值得庆幸的。

### IE10的多点触摸

虽然现在市场上WP手机越来越少，但是为了更完整的学习理解手势知识，我们也需要进行学习。IE10支持多点触摸，但是其多点触摸与ios和android不同，ios和android浏览器为多点触摸提供一个包含touches数组的事件，包含所有多点触摸对象，而IE10为多点触摸的每一个触摸点创建一个单独的触摸事件。

## 渐进增强与手势

我们知道手势很方便，用户也很喜欢手势，但是我们也要明白手势并不总是能使用，有些设备或浏览器还是不支持的，所以我们最合适的是基于普通点击和触摸事件交互的页面，将手势作为增强的交互，这就是通常所说的渐进增强思想。

## 触摸事件

既然是要渐进增强，那就必须从基础点击和触摸事件说起，点击事件就不再多说，关于触摸事件，之前也有一篇文章介绍过[移动开发之轻触与单击事件](http://blog.codingplayboy.com/2016/07/24/mobile_touch_tap/)，关于触摸四种基础事件和事件对象，可以查看该文章，这里就不重复了，这里要对触摸事件的处理进行说明。

### 浏览器兼容

通常我们在触摸和手势事件处理函数内会添加CSS3动画处理，这个时候需要进行浏览器兼容处理。

```

	var TRANSITION = 'transition';
	var TRANSITION_END = 'transitionend';
	var TRANSFORM = 'transform';
	
	if (typeof document.body.style.webkitTransform !== undefined) {
		TRANSITION = 'webkitTransition';
		TRANSITION_END = 'webkitTransitionEnd';
	}
```










