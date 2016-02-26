# Web学习之跨域问题及解决方案


1.document.domain+iframe情形 
2.jQuery下通过jsonp实现跨域 
3.服务器端的跨域解决方案 
4.h5 postMessage
5.IE8下的跨域问题

1.document.domain+iframe
对于主域相同而子域不同的例子，可以通过设置document.domain的办法来解决。具体的做法是可以在
http://www.a.com/a.html和http://script.a.com/b.html两个文件中分别加上document.domain = ‘a.com’；然
后通过a.html文件中创建一个iframe，去控制iframe的contentDocument，这样两个js文件之间就可以“交互”了。
当然这种办法只能解决主域相同而二级域名不同的情况，如果你异想天开的把script.a.com的domian设为
alibaba.com那显然是会报错地！代码如下：
www.a.com上的a.html
document.domain = 'a.com';
var ifr = document.createElement_x('iframe');
ifr.src = 'http://script.a.com/b.html';
ifr.style.display = 'none';
document.body.appendChild(ifr);
ifr.onload = function(){
    var doc = ifr.contentDocument || ifr.contentWindow.document;
    // 在这里操纵b.html
    alert(doc.getElementsByTagName_r("h1")[0].childNodes[0].nodeValue);
};
script.a.com上的b.html
document.domain = 'a.com';
这种方式适用于{www.kuqin.com, kuqin.com, script.kuqin.com, css.kuqin.com}中的任何页面相互通信。
备注：
    某一页面的domain默认等于window.location.hostname。主域名是不带www的域名，例如a.com，主域名前
面带前缀的通常都为二级域名或多级域名，例如www.a.com其实是二级域名。 domain只能设置为主域名，不可以在
b.a.com中将domain设置为c.a.com。
问题：
	1、安全性，当一个站点（b.a.com）被攻击后，另一个站点（c.a.com）会引起安全漏洞。
	2、如果一个页面中引入多个iframe，要想能够操作所有iframe，必须都得设置相同domain。

2.jQuery下通过jsonp实现跨域
$.ajax({    
           url: '',  // 跨域URL   
           type: 'GET',    
           dataType: 'jsonp',    
           jsonp: 'jsoncallback', //默认callback   
           data: mydata, //请求数据   
           timeout: 5000, 
           success: function (json) { //客户端jquery预先定义好的callback函数，成功获取跨域服务器上的
json数据后，会动态执行这个callback函数    
               if(json.actionErrors.length!=0){    
                   alert(json.actionErrors);    
               }    
           },    
           complete: function(XMLHttpRequest, textStatus){    
                 
           }
       });

3.服务器端的跨域解决方案
response.setHeader("Access-Control-Allow-Origin", "*");...
Access-Control-Allow-Origin: <origin> | * // 授权的源控制
Access-Control-Max-Age: <delta-seconds> // 授权的时间
Access-Control-Allow-Credentials: true | false // 控制是否开启与Ajax的Cookie提交方式
Access-Control-Allow-Methods: <method>[, <method>]* // 允许请求的HTTP Method
Access-Control-Allow-Headers: <field-name>[, <field-name>]* // 控制哪些header能发送真正的请求 
4.h5 postMessage
http://www.cnblogs.com/dolphinX/p/3464056.html   