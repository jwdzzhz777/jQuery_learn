#jQuery
	翻译jQuery(雾)
##关于jQuery	
	
###基础知识
	基本页面
```html
<!DOCTYPE html>
<html>
<head>
	<meta charset="utf-8">
	<title>test</title>
	<style>
		a.test {
		    font-weight: bold;
		}	
	</style>
</head>
<body>
	<a href="http://jquery.com/"></a>
	<script src="jquery.js"></script>
	<script>
		window.onload = function() {
    		alert( "welcome" );
		};
		$(document).ready(function(){
			$('a').click(function(e){
				alert( "Thanks for visiting!" );
				event.preventDefault();//阻止默认行为（打开链接）
				$(this).removeClass( "test" );
				$(this).hide( "slow" );
			});
			$('a').addClass("test");
		});
	</script>
</body>
</html>
```

为了确保他们的代码运行在浏览器完成加载该文件之后，许多JavaScript程序员包装自己的代码在的``onload	``中</br>

不幸的是，代码不运行(明明运行了)，直到所有图像都下载完毕，包括横幅广告。尽管运行代码的文件已准备好进行操作，大家都知道jQuery有被称为``ready``的事件</br>

``click``事件中可以使用``event.preventDefault()``来阻止默认行为。</br>

``addClass()``和``removeClass``

###方法和回调

```jQuery
$.get( "myhtmlpage.html", myCallBack );
```
当$.get()完成得到``myhtmlpage.html``页面时会调用``myCallBack``方法</br>
注意:``myCallBack``参数在这里只是简单的方法名而不是String而且没有括号。</br>

当方法需要传参数时:
错误示范
```jq
$.get( "myhtmlpage.html", myCallBack( param1, param2 ) );
```
错误原因是该代码立即执行``myCallBack``函数,然后通过``myCallBack``方法的返回值继续调用``$.get``方法.事实上我们想调用``myCallBack``方法,而不是返回值(这可能也不是一个方法)。</br>

正确方法:
```jq
$.get( "myhtmlpage.html", function() {
 
    myCallBack( param1, param2 );
 
});
```

##$(document).ready()

一个页面不能被安全操作直到document'ready'.jquery帮你检测这种状态。当DOM准备好执行JavaScript代码时在``$(document).ready()``的代码只会被执行一次。而只有当整个页面都加载完毕，包括图片和内部框架时``$( window ).load(function() { ... })``才会被执行。</br>
正常的方法:
```jq
$( document ).ready(function() {
    console.log( "ready!" );
});
```
短方法:
```jq
$(function() {
    console.log( "ready!" );
});
```
还可以这样:
```jq
// 传递匿名函数的命名函数。
 
function readyFn( jQuery ) {
    // Code to run when the document is ready.
}
 
$( document ).ready( readyFn );
// or:
$( window ).load( readyFn );
```

###避免冲突
jQuery库和几乎所有的插件都包含在jQuery的命名空间内。一般来说，全局对象存储在jQuery的命名空间内为好，所以你不应该得到jQuery和任何其他库之间的冲突（如prototype.js中，Mootools和YUI）。
尽管如此，有一点需要注意：默认情况下，jQuery使用``$``作为jQuery的快捷方式.因此,如果您使用的另一个JavaScript库是使用``$``变量，就会与jQuery的冲突。为了避免这些冲突，你需要在页面加载完成之后,你试图使用jQuery之前,立即使用jQuery的无冲突模式。

```jq
<!-- Putting jQuery into no-conflict mode. -->
<script src="prototype.js"></script>
<script src="jquery.js"></script>
<script>
 
var $j = jQuery.noConflict();
//无冲突模式,即起一个新名字
 
$j(document).ready(function() {
    $j( "div" ).hide();
});
 
// The $ variable now has the prototype meaning, which is a shortcut for
// document.getElementById(). mainDiv below is a DOM element, not a jQuery object.
window.onload = function() {
    var mainDiv = $( "main" );
}
 
</script>
```

还有一种方法你可以用jQuery作为方法名</br>
如果加载jq库在其他库之前可以正常使用``$``.
```jq
<!-- Loading jQuery before other libraries. -->
<script src="jquery.js"></script>
<script src="prototype.js"></script>
<script>
 
// Use full jQuery function name to reference jQuery.
jQuery( document ).ready(function() {
    jQuery( "div" ).hide();
});
 
// Use the $ variable as defined in prototype.js
window.onload = function() {
    var mainDiv = $( "main" );
};
 
</script>
```

###Attributes

元素的属性可以包含应用程序的有用信息，这样一来就能来获取和设置它们是非常重要的。

####``.attr()``方法

``.attr()``方法可以同时起到get 和 set 的作用。``.attr()``可以接受key ,value,甚至多个key-value 对象。

as a setter:
```jq
$( "a" ).attr( "href", "allMyHrefsAreTheSameNow.html" );
 
$( "a" ).attr({
    title: "all titles are the same too!",
    href: "somethingNew.html"
});
```
as a getter:
```jq
$( "a" ).attr( "href" ); 
```

###选择器
各种方法
```jq
$( "#myId" ); // Note IDs must be unique per page.
$( ".myClass" );
$( "input[name='first_name']" );
$( "#contents ul.people li" );
$( "div.myClass, ul.people" );
```

####伪选择:
```jq
$( "a.external:first" );
$( "tr:odd" );
 
// 所有输入样式的元素
$( "#myForm :input" );
$( "div:visible" );
 
// 除了前3个div外的元素
$( "div:gt(2)" );
 
// 有动画的元素
$( "div:animated" );
```
注意:当使用``visible``和``hidden``这种伪选择器时,jq会自动检测元素的可见度,不是CSS的``visibility ``或``display ``属性。jq通过查看元素宽高是否都大于0的方式检测。,</br>

然而这种方法不适用于``<tr>``元素,jq会检查``<tr>``的``display ``属性,如果``display ``设置为``none ``jq会认为该元素是不可见的。</br>

那些还没有被添加的DOM元素会被认为是隐藏的,即使通过CSS改变其可见属性。

####选择选择器

一个好的选择是提高JavaScript的性能的一种方式。太多的特异性也可能是一件坏事。

```jq
// 不能这么用！
if ( $( "div.foo" ) ) {
    ...
}
```
上述这么用是错误的,当使用``$()``时,总是会返回一个Object对象,而这个Object对象会被当成``true``。即使没有选择到任何元素,上诉代码仍然会运行。</br>

知道是否有元素被选择的好方法是``.lenght``属性,其返回的值代表了有多少个元素被选择了。如果这个值是0,则会被当作是false。
```jq
// Testing whether a selection contains elements.
if ( $( "div.foo" ).length ) {
    ...
}
```

####储存选择器
jQuery不会为你缓存,如果要多次选择一个元素,就把选择器保存在一个变量里。
```jq
var divs = $( "div" );
```
直接调用divs就可以了。

####选择表单元素

jQuery提供了几个伪选择器，帮助查找表单元素。这些是特别有用的，因为它可能很难根据它们的状态形式在元素之间进行区分，或者使用标准CSS选择键入。

