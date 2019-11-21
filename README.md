# jQuery

~~翻译jQuery~~

## jQuery核心代码	
	
### 基础知识

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

为了确保他们的代码运行在浏览器完成加载该文件之后，许多JavaScript程序员包装自己的代码在的``onload	``中。</br>

不幸的是，代码不运行(明明运行了)，直到所有图像都下载完毕，包括横幅广告。尽管运行代码的文件已准备好进行操作，大家都知道jQuery有被称为``ready``的事件</br>

``click``事件中可以使用``event.preventDefault()``来阻止默认行为。</br>

``addClass()``和``removeClass()``

### 方法和回调

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

## $(document).ready()

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

### 避免冲突
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

### Attributes

元素的属性可以包含应用程序的有用信息，这样一来就能来获取和设置它们是非常重要的。

#### ``.attr()``方法

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

### 选择器
各种方法
```jq
$( "#myId" ); // Note IDs must be unique per page.
$( ".myClass" );
$( "input[name='first_name']" );
$( "#contents ul.people li" );
$( "div.myClass, ul.people" );
```

#### 伪选择:
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

#### 选择选择器

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

#### 储存选择器
jQuery不会为你缓存,如果要多次选择一个元素,就把选择器保存在一个变量里。
```jq
var divs = $( "div" );
```
直接调用divs就可以了。

选择器只取那些选择时存在于页面上的元素。如果元素后来添加到页面，你就必须重复选择或以其他方式将它们添加到存储在变量的选择。存储选择当DOM变化时不会神奇地更新。

#### 精炼和筛选选择器
```jq
// Refining selections.
$( "div.foo" ).has( "p" );         // 包含<p>标签的div.foo元素
$( "h1" ).not( ".bar" );           // class 不为 bar 的h1元素
$("div").css("background", "#c8ebcc")
  .filter(".middle")
  .css("border-color", "red");	   //改变所有 div 的颜色，然后向类名为 "middle" 的元素添加边框：
$( "ul li" ).first();              // 对应ul元素的第一项li元素
$( "ul li" ).eq( 5 );              // 第六个li元素
```

#### 选择表单元素

jQuery提供了几个伪选择器，帮助查找表单元素。这些是特别有用的，因为它可能很难根据它们的状态形式在元素之间进行区分，或者使用标准CSS选择键入。

##### :checked
不要被``:checkbox``迷惑,它适用于复选框(checkboxes)中被选中的元素,同样适用于radio buttons和``<select>``元素(如果只有``<select>``,用下面的``:selected``).
```jq
$( "form :checked" );
```
##### :disabled
用``:disabled``伪选择标签选择任何有``disabled``属性的元素。
```jq
$( "form :disabled" );
```
##### :enabled
基本上就是``:disabled``的对立,``:enabled``可以选择的所有没有``disabled``属性的元素。
```jq
$( "form :enabled" );
```
为了更好使用``:enabled``,先用标准jq选择元素再通过``filter()``筛选enabled的元素, or precede the pseudo-selector with a tag name or some other selector.

##### :input
会选择所有包括``<input>``,``<textarea>``,``<select>``and``<button>``元素
```jq
$( "form :input" );
```
##### :selected
选择所有``<option>``元素内被选中的元素。
```jq
$( "form :selected" );
```
为了更好使用``:selected``,先用标准jq选择元素再通过``filter()``筛选selected的元素, or precede the pseudo-selector with a tag name or some other selector.

##### 通过type
*:password
*:reset
*:radio
*:text
*:submit
*:checkbox
*:button
*:image
*:file

### 使用选择器

#### getter&setter
一些jq方法可以从被选择元素中get或set一些值。当方法调用带有value作为参数时，则被认为是setter因为它设置了value。如果调用时没有参数则被认为是读取一些值。setter会作用与所有选择的元素 而getter只会作用于选择的第一个元素。如果要get所有选择的元素的值用``.text()``方法。
```jq
// 设置所有<h1>的value为 "hello world" 
$( "h1" ).html( "hello world" );
// 获得第一个<h1>的值
$( "h1" ).html();
// > "hello world"
```

setter返回的一个object对象,允许你继续调用jq方法,而getter会返回任何你要求返回的,所以你不能对getter返回的value继续调用jq方法。
```jq
// Attempting to call a jQuery method after calling a getter.
// This will NOT work:
$( "h1" ).html().addClass( "test" );
```

#### 链
如果你对选择器调用了jq方法,其方法返回的value为object,你可以在这之后继续调用jqff而不需要分号。我们称之为链。
```jq
$( "#content" ).find( "h3" ).eq( 2 ).html( "new text for the third h3!" );
```
还可以换行:
```jq
$( "#content" )
    .find( "h3" )
    .eq( 2 )
    .html( "new text for the third h3!" );
```
你还可以通过end结束上一个链。
```jq
$( "#content" )
    .find( "h3" )
    .eq( 2 )
        .html( "new text for the third h3!" )
        .end() // Restores the selection to all h3s in #content
    .eq( 0 )
        .html( "new text for the first h3!" );
```
链很强大,从他流行开始很多库已经兼容,但是也要慎重使用--过多地使用链会导致代码难以修改或调试。没有任何的硬性规定链要有多长,但这很容易让人膨胀。

### 元素的操作

#### 获取和设置元素的相关信息
有很多方法可以去改变一个元素,其中最常见的是改变HTML的value或元素的属性。jq为此提供了简单的，跨浏览器的方法。你可以通过 getter incarnations里的很多相同的方法来得到元素的信息。下面是几种方法:
**.html()** – 获取或设置HTML的内容(code)
**.text()** – 获取或设置HTML的内容:HTML将被剥离;(text)
**.attr()** – 获取或设置属性的值
**.width()** – 获取或设置第一个元素的宽度,类型为integer
**.height()** – 获取或设置第一个元素的高度,类型为integer
**.position()** – 获取position信息(getter only)
**.val()** – 得到或获取表单元素的值

注意:这些方法会影响所有被选择到的元素,如果要做用于某几个元素在选择器上做文章。
```jq
// Changing the HTML of an element.
$( "#myDiv p:first" ).html( "New <strong>first</strong> paragraph!" );
```

#### 移动,复制和删除元素
虽然有多种方式来移动所述DOM元素，但常用的有两种方法：
*放置所选择的元件（多个）相对于另一个元件。
*放置一个元件相对于选定元素（多个）。
jq提供了``.insertAfter()``和``.after()``。``.insertAfter()``方法将选择的元素(多个)放置到作为()内参数的元素之后。而``.after()``方法将作为()内参数的元素放置到选择的元素之后。还有一些遵循这种模式的方法:
*``.insertBefore()``and``.before()``//在所选元素之前
*``.appendTo()``and``.append()``//在所选元素的结尾(仍然在内部)
*``.prependTo()``and``.prepend()``//在所选元素的开头(仍然在内部)

用什么方法取决于你选择的对象,以及是否需要为你添加的元素储存参考,如果需要保存到变量中,请一律使用前一种方法:放置所选择的元件（多个）相对于另一个元件。因为这些方法返回的是你选择(放置)的元素:``.insertAfter()``,``.insertBefore()``,``.appendTo()``and``.prependTo()``
```jq
// Moving elements using different approaches.
 
// 将列表的第一个放到最后一个
var li = $( "#myList li:first" ).appendTo( "#myList" );
 
// 同样的结果
$( "#myList" ).append( $( "#myList li:first" ) );
 
// Note that there's no way to access the list item
// that we moved, as this returns the list itself.
```

#### 复制元素
和``.appendTo()``类似,不过用元素的副本代替
```jq
// Making a copy of an element.
 
// 复制列表的第一项然后粘帖到最后一项
$( "#myList li:first" ).clone().appendTo( "#myList" );
```
如果需要复制相关的数据和事件,需要确保通过``.clone()``的参数为true.

#### 移除元素
有两种方法remove元素``.remove()``和``.detach()``,如果你想完全移除元素的话就用``.remove()``,但是他会返回你删除的元素,如果你将返回的元素重新放入页面中,元素将不会拥有之前所包含的事件和数据。而当你使用``.detach()``,你可以使用其返回的元素重新复原你删除的元素(数据和事件不会删除)<br>

如果你需要保留元素而删除其内容,可以使用``.empty()``方法。

#### 创建新元素
你可以直接使用``$()``方法创建新元素
```jq
// Creating new elements from an HTML string.
$( "<p>This is a new paragraph</p>" );
$( "<li class=\"new\">new list item</li>" );
// Creating a new element with an attribute object.
$( "<a/>", {
    html: "This is a <strong>new</strong> link",
    "class": "new",
    href: "foo.html"
});
```
注意:除非是保留字,不然属性名不需要引用。https://mathiasbynens.be/notes/reserved-keywords

放入页面
```jq
// Getting a new element on to the page.
 
var myNewElement = $( "<p>New element</p>" );
 
myNewElement.appendTo( "#content" );
 
myNewElement.insertAfter( "ul:last" ); // 这样做会删除上面"#content"里的<p>元素。
 
$( "ul" ).last().after( myNewElement.clone() ); //这样做就不会删除啦
```
你也可以在创建元素的同时添加到页面,但这么做你将无法得到元素的引用。
```jq
// Creating and adding an element to the page at the same time.
$( "ul" ).append( "<li>list item</li>" );
```
反复的添加会造成巨大的性能开销,所以如果需要添加大量元素,将这些元素储存在一个容器中。
```jq
var myItems = [];
var myList = $( "#myList" );
 
for ( var i = 0; i < 100; i++ ) {
    myItems.push( "<li>item " + i + "</li>" );
}
 
myList.append( myItems.join( "" ) );
```
#### 属性操作
jq的属性操作很简单,但``.attr()``也可以用于更复杂的操作,他可以设置明确的值,也可以设置方法的返回值,当使用方法时可以传入两个参数,当前选择器的index值和当前的属性值。
```jq
// Manipulating a single attribute.
$( "#myDiv a:first" ).attr( "href", "newDestination.html" );

// Manipulating multiple attributes.
$( "#myDiv a:first" ).attr({
    href: "newDestination.html",
    rel: "nofollow"
	
// Using a function to determine an attribute's new value.
$( "#myDiv a:first" ).attr({
    rel: "nofollow",
    href: function( idx, href ) {
        return "/new/" + href;
    }
});
 
$( "#myDiv a:first" ).attr( "href", function( idx, href ) {
    return "/new/" + href;
});
```
### jQuery对象

当创建新元素（或选择现有的元素），jQuery会返回一个元素的集合。许多开发者认为这是一个数组。它有一个从0开始的元素序列,一些类似数组的方法,以及``.length``属性。事实上，jQuery对象是比这更复杂。

#### DOM和DOM元素

Document Object Model (简称DOM)是HTML文档的表示。它可以包含任何数目的DOM元素。说玄乎点,一个DOM元素可以被认为是一个拼凑的网页。它可以包含文本和/或其它的DOM元素。 DOM元素是由一个类型描述，例如``<div>``,``<a>``,或``<p>``,而且包括任意数量的属性如``src``,``href``,``class``等的。有关更详尽的说明，请参阅来自W3C官方的DOM规范。

就像javaScript一样,元素也有对应的属性,就像``.tagName ``和``.appendChild()``这些属性是javaScript和网页交互的唯一途径.

#### jQuery对象
jQuery让我们可以直接对DOM对象进行操作,jQuery定义了许多方法让开发者不需要太多的经验,jQuery对象的好处包括:<br>
兼容性 - 元素的调用方法会根据浏览器供应商和版本的不同而不同,下面片段尝试将``<tr>``元素储存在一个``target``变量中:
```jq
var target = document.getElementById( "target" );
target.innerHTML = "<td>Hello <b>World</b>!</td>";
```
大多情况下可行,但它会在Internet Explorer的大多数版本下失败。在这种情况下，推荐的方法是使用纯DOM方法代替。把``target``变量包装成jQuery对象,这样可以在所有浏览器实现。
```jq
// Setting the inner HTML with jQuery.
 
var target = document.getElementById( "target" );
 
$( target ).html( "<td>Hello <b>World</b>!</td>" );
```
方便 - 也有很多共同的DOM操作的用尴尬的纯DOM方法来完成。例如在得到一个``target ``元素之后插入一个新创建的元素会有一个很长的方法:
```jq
// Inserting a new element after another with the native DOM API.
 
var target = document.getElementById( "target" );
 
var newElement = document.createElement( "div" );
 
target.parentNode.insertBefore( newElement, target.nextSibling );
```
用jQuery就很方便了:
```jq
// Inserting a new element after another with jQuery.
 
var target = document.getElementById( "target" );
 
var newElement = document.createElement( "div" );
 
$( target ).after( newElement );
```
#### 将元素包装成jQuert对象。
```jq
// Selecting all <h1> tags.
 
var headings = $( "h1" );
```
``headings ``是一个包含了所有``<h1>``标签的jQuery元素,你可以用``.length ``属性验证。
```jq
// Viewing the number of <h1> tags on the page.
 
var headings = $( "h1" );
 
alert( headings.length );
```
如果要选择第一个元素,有很多方法``eq()``是其中之一。
```jq
// Selecting only the first <h1> element on the page (in a jQuery object)
 
var headings = $( "h1" );
 
var firstHeading = headings.eq( 0 );
```
现在``firstHeading``是一个仅包含页面第一个``<h1>``元素的jQuery对象,正因为如此,可以用``.html()``方法和``.after()``方法。你也可以用``get()``方法来得到第一个元素,唯一的区别是``get()``返回的不是jq包裹的DOM对象,而是DOM对象他本身。
```jq
// Selecting only the first <h1> element on the page.
 
var firstHeadingElem = $( "h1" ).get( 0 );
```
另外,jq对象和数组很想,所以它可以用括号:
```jq
// Selecting only the first <h1> element on the page (alternate approach).
 
var firstHeadingElem = $( "h1" )[ 0 ];
```
``firstHeadingElem``包含了DOM元素,它拥有DOM属性比如``.innerHTML``和``.appendChild()``,但是不能使用jq方法比如``.html()``和``.after()``。我们很难对``firstHeadingElem ``元素进行操作,但总有情况需要用到它.

#### 不是所有被创建的jQuery对象都相等(``===``)
一个重要的细节是每一个jq包裹的对象都是唯一的,即使对象用相同的方法创建或含有完全相同的DOM元素的引用。
```jq
// Creating two jQuery objects for the same element.
 
var logo1 = $( "#logo" );
var logo2 = $( "#logo" );
// Comparing jQuery objects.
 
alert( $( "#logo" ) === $( "#logo" ) ); // alerts "false"
```
但是这两个jq对象拥有相同的DOM,通过``get()``方法可以确定这两个DOM是否是同一个。
```jq
// Comparing DOM elements.
 
var logo1 = $( "#logo" );
var logo1Elem = logo1.get( 0 );
 
var logo2 = $( "#logo" );
var logo2Elem = logo2.get( 0 );
 
alert( logo1Elem === logo2Elem ); // alerts "true"
```
很多人喜欢在命名用于保存jq对象的变量时加``$``在名字前面,这不是什么神奇的做法,仅仅帮助区分变量储存的是jq对象还是DOM元素。
```jq
// Comparing DOM elements (with more readable variable names).
 
var $logo1 = $( "#logo" );
var logo1 = $logo1.get( 0 );
 
var $logo2 = $( "#logo" );
var logo2 = $logo2.get( 0 );
 
alert( logo1 === logo2 ); // alerts "true"
```
无论使用哪种命名规范,区分jq对象和DOM元素都是很重要的,DOM元素不能使用jq方法,反之亦然。如果出现"event.target.closest is not a function"' 或者 "TypeError: Object [object Object] has no method 'setAttribute'"这种报错说明犯了这种错误。
#### jq不是活的
当页面元素发生变化,jq对象不会对该变化做出反应,即不会做出任何改变。

### 遍历
可以遍历选择的对象,可以访问到父,子或同级的对象,jq提供了很多简单的方法。
#### Parents
方法包括``.parent()``,``.parents()``,``.parentsUntil()``and``.closest()``.
```jq
<div class="grandparent">
    <div class="parent">
        <div class="child">
            <span class="subchild"></span>
        </div>
    </div>
    <div class="surrogateParent1"></div>
    <div class="surrogateParent2"></div>
</div>
// Selecting an element's direct parent:
 
// returns [ div.child ]
$( "span.subchild" ).parent();
 
// 选择所有的父元素,你甚至可以用选择器
 
// returns [ div.parent ]
$( "span.subchild" ).parents( "div.parent" );
 
// returns [ div.child, div.parent, div.grandparent ]
$( "span.subchild" ).parents();
 
// 选择所有的父元素,不包括后面选择器选择的
 
// returns [ div.child, div.parent ]
$( "span.subchild" ).parentsUntil( "div.grandparent" );
 
// 选择最近的父元素,只有一个。
// 他自己也会被选择。
 
// returns [ div.child ]
$( "span.subchild" ).closest( "div" );
 
// returns [ div.child ] as the selector is also included in the search:
$( "div.child" ).closest( "div" );
```
#### 子元素
我们可以通过``.children()``和``.find()``方法找到子元素,两者的区别在于涉及的范围,``.children()``只能找到选择的子元素,``.find()``找到子元素外还包括子元素的子元素。
```jq
// Selecting an element's direct children:
 
// returns [ div.parent, div.surrogateParent1, div.surrogateParent2 ]
$( "div.grandparent" ).children( "div" );
 
// Finding all elements within a selection that match the selector:
 
// returns [ div.child, div.parent, div.surrogateParent1, div.surrogateParent2 ]
$( "div.grandparent" ).find( "div" );
```
#### 同级元素
剩下的jq方法都是用来处理同级元素的,有几个方法比较偏向于遍历,``.prev()``前一个同级,``.next()``找到后一个同级,``.siblings()``选择所有同级元素。还有和这些方法模式相同的方法:``.nextAll()``,``.nextUntil()``,``.prevAll()``and``.prevUntil()``。
```jq
// Selecting a next sibling of the selectors:
 
// returns [ div.surrogateParent1 ]
$( "div.parent" ).next();
 
// Selecting a prev sibling of the selectors:
 
// returns [] as No sibling exists before div.parent
$( "div.parent" ).prev();
 
// Selecting all the next siblings of the selector:
 
// returns [ div.surrogateParent1, div.surrogateParent2 ]
$( "div.parent" ).nextAll();
 
// returns [ div.surrogateParent1 ]
$( "div.parent" ).nextAll().first();
 
// returns [ div.surrogateParent2 ]
$( "div.parent" ).nextAll().last();
 
// Selecting all the previous siblings of the selector:
 
// returns [ div.surrogateParent1, div.parent ]
$( "div.surrogateParent2" ).prevAll();
 
// returns [ div.surrogateParent1 ]
$( "div.surrogateParent2" ).prevAll().first();
 
// returns [ div.parent ]
$( "div.surrogateParent2" ).prevAll().last();

// Selecting an element's siblings in both directions that matches the given selector:
 
// returns [ div.surrogateParent1, div.surrogateParent2 ]
$( "div.parent" ).siblings();
 
// returns [ div.parent, div.surrogateParent2 ]
$( "div.surrogateParent1" ).siblings();
```
### CSS 样式和尺寸
jq有很多方法改变元素的CSS属性。
```jq
// Getting CSS properties.
 
$( "h1" ).css( "fontSize" ); // Returns a string such as "19px".
 
$( "h1" ).css( "font-size" ); // Also works.
// Setting CSS properties.
 
$( "h1" ).css( "fontSize", "100px" ); // Setting an individual property.
 
// Setting multiple properties.
$( "h1" ).css({
    fontSize: "100px",
    color: "red"
});
```
可以一次设置多个对象.<br>

#### 使用CSS类设置样式。
```jq
// Working with classes.
 
var h1 = $( "h1" );
 
h1.addClass( "big" );
h1.removeClass( "big" );
h1.toggleClass( "big" );
 
if ( h1.hasClass( "big" ) ) {
    ...
}
```

#### 尺寸
jq提供了许多修改和获取元素尺寸和位置信息的方法
```jq
// Basic dimensions methods.
 
// Sets the width of all <h1> elements.
$( "h1" ).width( "50px" );
 
// Gets the width of the first <h1> element.
$( "h1" ).width();
 
// Sets the height of all <h1> elements.
$( "h1" ).height( "50px" );
 
// Gets the height of the first <h1> element.
$( "h1" ).height();
 
 
// Returns an object containing position information for
// the first <h1> relative to its "offset (positioned) parent".
$( "h1" ).position();
```
### 数据的方法
你会经常需要为一个元素储存一个数据,用JavaScript,你只能通过添加属性到DOM元素,而且必须处理浏览器的内存泄漏问题,jq就可以帮你解决这些问题.
```jq
// Storing and retrieving data related to an element.
 
$( "#myDiv" ).data( "keyName", { foo: "bar" } );
 
$( "#myDiv" ).data( "keyName" ); // Returns { foo: "bar" }
```
任何类型的数据都可以储存在元素上。而且数据可以用来作为和其他元素的联系。

举个例子,你可能想在一个list列表和一个div之间建立联系,而div刚好在list里,我们可以通过``.data()``(太难表达,直接看代码)
```jq
// Storing a relationship between elements using .data()
 
$( "#myList li" ).each(function() {
 
    var li = $( this );
    var div = li.find( "div.content" );
 
    li.data( "contentDiv", div );
 
});
 
// Later, we don't have to find the div again;
// we can just read it from the list item's data
var firstLi = $( "#myList li:first" );
 
firstLi.data( "contentDiv" ).html( "new content" );
```
我们可以通过数据直接选择到div而不需要再用选择器选择div了

### 实用方法
jQuery提供在$命名空间中的几个实用方法。这些方法对于日常完成的编程任务很有帮助。
```jq
$.trim()
```
消除开头和结尾的空格
```jq
// Returns "lots of extra whitespace"
$.trim( "    lots of extra whitespace    " );
```
```jq
$.each()
```
遍历数组和对象
```jq
$.each([ "foo", "bar", "baz" ], function( idx, val ) {
    console.log( "element " + idx + " is " + val );
});
 
$.each({ foo: "bar", baz: "bim" }, function( k, v ) {
    console.log( k + " : " + v );
});
```
``.each()``不同于``$.each()``它可以迭代所有选择器选择的元素。$().each(function(index,element){ ... })
```jq
$.inArray()
```
返回元素的index值,如果不在数组中则返回-1。
```jq
var myArray = [ 1, 2, 3, 5 ];
 
if ( $.inArray( 4, myArray ) !== -1 ) {
    console.log( "found it!" );
}
```
```jq
$.extend()
```
将后面对象的属性合并到前面对象。
```jq
var firstObject = { foo: "bar", a: "b" };
var secondObject = { foo: "baz" };
 
var newObject = $.extend( firstObject, secondObject );
 
console.log( firstObject.foo ); // "baz"
console.log( newObject.foo ); // "baz"

```
如果你不想改变任何传递给``$.extend()``的对象，传递一个空对象作为第一个参数:
```jq
var myFunction = function() {
    console.log( this );
};
var myObject = {
    foo: "bar"
};
 
myFunction(); // window
 
var myProxyFunction = $.proxy( myFunction, myObject );
 
myProxyFunction(); // myObject
```
```jq
$.proxy()
```
让方法的上下文(this)设置为后面的对象。
```jq
var myFunction = function() {
    console.log( this );
};
var myObject = {
    foo: "bar"
};
 
myFunction(); // window
 
var myProxyFunction = $.proxy( myFunction, myObject );
 
myProxyFunction(); // myObject

//或者
var myObject = {
    myFn: function() {
        console.log( this );
    }
};
 
$( "#foo" ).click( myObject.myFn ); // HTMLElement #foo
$( "#foo" ).click( $.proxy( myObject, "myFn" ) ); // myObject
```
#### 检测类型
有时``typeof``运算符可能会造成混淆或不一致，因此而不是使用typeof运算，jQuery提供了实用方法来帮助确定一个值的类型。
```jq
$.isArray([]); // true
$.isFunction(function() {}); // true
$.isNumeric(3.14); // true
```
```jq
$.type( true ); // "boolean"
$.type( 3 ); // "number"
$.type( "test" ); // "string"
$.type( function() {} ); // "function"
 
$.type( new Boolean() ); // "boolean"
$.type( new Number(3) ); // "number"
$.type( new String('test') ); // "string"
$.type( new Function() ); // "function"
 
$.type( [] ); // "array"
$.type( null ); // "null"
$.type( /test/ ); // "regexp"
$.type( new Date() ); // "date"
```
### 遍历jq对象和非jq对象
简单的就不说了。下面是一些可以当``.each()``用的方法
*.attr() (getter)
*.css() (getter)
*.data() (getter)
*.height() (getter)
*.html() (getter)
*.innerHeight()
*.innerWidth()
*.offset() (getter)
*.outerHeight()
*.outerWidth()
*.position()
*.prop() (getter)
*.scrollLeft() (getter)
*.scrollTop() (getter)
*.val() (getter)
*.width() (getter)
Note that in most cases, the "getter" signature returns the result from the first element in a jQuery collection while the setter acts over the entire collection of matched elements. The exception to this is .text() where the getter signature will return a concatenated string of text from all matched elements.

In addition to a setter value, the attribute, property, CSS setters, and DOM insertion "setter" methods (i.e. .text() and .html()) accept anonymous callback functions that are applied to each element in the matching set. The arguments passed to the callback are the index of the matched element within the set and the result of the 'getter' signature of the method.

~~翻译不来~~
```jq
$( "input" ).each( function( i, el ) {
    var elem = $( el );
    elem.val( elem.val() + "%" );
});
 
$( "input" ).val(function( index, value ) {
    return value + "%";
});
```
这样是一样的
