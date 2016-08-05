#jQuery

~~����jQuery~~

##jQuery���Ĵ���	
	
###����֪ʶ

����ҳ��

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
				event.preventDefault();//��ֹĬ����Ϊ�������ӣ�
				$(this).removeClass( "test" );
				$(this).hide( "slow" );
			});
			$('a').addClass("test");
		});
	</script>
</body>
</html>
```

Ϊ��ȷ�����ǵĴ����������������ɼ��ظ��ļ�֮�����JavaScript����Ա��װ�Լ��Ĵ����ڵ�``onload	``�С�</br>

���ҵ��ǣ����벻����(����������)��ֱ������ͼ��������ϣ����������档�������д�����ļ���׼���ý��в�������Ҷ�֪��jQuery�б���Ϊ``ready``���¼�</br>

``click``�¼��п���ʹ��``event.preventDefault()``����ֹĬ����Ϊ��</br>

``addClass()``��``removeClass()``

###�����ͻص�

```jQuery
$.get( "myhtmlpage.html", myCallBack );
```
��$.get()��ɵõ�``myhtmlpage.html``ҳ��ʱ�����``myCallBack``����</br>

ע��:``myCallBack``����������ֻ�Ǽ򵥵ķ�����������String����û�����š�</br>
��������Ҫ������ʱ:
����ʾ��
```jq
$.get( "myhtmlpage.html", myCallBack( param1, param2 ) );
```
����ԭ���Ǹô�������ִ��``myCallBack``����,Ȼ��ͨ��``myCallBack``�����ķ���ֵ��������``$.get``����.��ʵ�����������``myCallBack``����,�����Ƿ���ֵ(�����Ҳ����һ������)��</br>

��ȷ����:
```jq
$.get( "myhtmlpage.html", function() {
 
    myCallBack( param1, param2 );
 
});
```

##$(document).ready()

һ��ҳ�治�ܱ���ȫ����ֱ��document'ready'.jquery����������״̬����DOM׼����ִ��JavaScript����ʱ��``$(document).ready()``�Ĵ���ֻ�ᱻִ��һ�Ρ���ֻ�е�����ҳ�涼������ϣ�����ͼƬ���ڲ����ʱ``$( window ).load(function() { ... })``�Żᱻִ�С�</br>
�����ķ���:
```jq
$( document ).ready(function() {
    console.log( "ready!" );
});
```
�̷���:
```jq
$(function() {
    console.log( "ready!" );
});
```
����������:
```jq
// ������������������������
 
function readyFn( jQuery ) {
    // Code to run when the document is ready.
}
 
$( document ).ready( readyFn );
// or:
$( window ).load( readyFn );
```

###�����ͻ
jQuery��ͼ������еĲ����������jQuery�������ռ��ڡ�һ����˵��ȫ�ֶ���洢��jQuery�������ռ���Ϊ�ã������㲻Ӧ�õõ�jQuery���κ�������֮��ĳ�ͻ����prototype.js�У�Mootools��YUI����
������ˣ���һ����Ҫע�⣺Ĭ������£�jQueryʹ��``$``��ΪjQuery�Ŀ�ݷ�ʽ.���,�����ʹ�õ���һ��JavaScript����ʹ��``$``�������ͻ���jQuery�ĳ�ͻ��Ϊ�˱�����Щ��ͻ������Ҫ��ҳ��������֮��,����ͼʹ��jQuery֮ǰ,����ʹ��jQuery���޳�ͻģʽ��

```jq
<!-- Putting jQuery into no-conflict mode. -->
<script src="prototype.js"></script>
<script src="jquery.js"></script>
<script>
 
var $j = jQuery.noConflict();
//�޳�ͻģʽ,����һ��������
 
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

����һ�ַ����������jQuery��Ϊ������</br>
�������jq����������֮ǰ��������ʹ��``$``.
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

Ԫ�ص����Կ��԰���Ӧ�ó����������Ϣ������һ����������ȡ�����������Ƿǳ���Ҫ�ġ�

####``.attr()``����

``.attr()``��������ͬʱ��get �� set �����á�``.attr()``���Խ���key ,value,�������key-value ����

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

###ѡ����
���ַ���
```jq
$( "#myId" ); // Note IDs must be unique per page.
$( ".myClass" );
$( "input[name='first_name']" );
$( "#contents ul.people li" );
$( "div.myClass, ul.people" );
```

####αѡ��:
```jq
$( "a.external:first" );
$( "tr:odd" );
 
// ����������ʽ��Ԫ��
$( "#myForm :input" );
$( "div:visible" );
 
// ����ǰ3��div���Ԫ��
$( "div:gt(2)" );
 
// �ж�����Ԫ��
$( "div:animated" );
```
ע��:��ʹ��``visible``��``hidden``����αѡ����ʱ,jq���Զ����Ԫ�صĿɼ���,����CSS��``visibility ``��``display ``���ԡ�jqͨ���鿴Ԫ�ؿ���Ƿ񶼴���0�ķ�ʽ��⡣,</br>

Ȼ�����ַ�����������``<tr>``Ԫ��,jq����``<tr>``��``display ``����,���``display ``����Ϊ``none ``jq����Ϊ��Ԫ���ǲ��ɼ��ġ�</br>

��Щ��û�б���ӵ�DOMԪ�ػᱻ��Ϊ�����ص�,��ʹͨ��CSS�ı���ɼ����ԡ�

####ѡ��ѡ����

һ���õ�ѡ�������JavaScript�����ܵ�һ�ַ�ʽ��̫���������Ҳ������һ�����¡�

```jq
// ������ô�ã�
if ( $( "div.foo" ) ) {
    ...
}
```
������ô���Ǵ����,��ʹ��``$()``ʱ,���ǻ᷵��һ��Object����,�����Object����ᱻ����``true``����ʹû��ѡ���κ�Ԫ��,���ߴ�����Ȼ�����С�</br>

֪���Ƿ���Ԫ�ر�ѡ��ĺ÷�����``.lenght``����,�䷵�ص�ֵ�������ж��ٸ�Ԫ�ر�ѡ���ˡ�������ֵ��0,��ᱻ������false��
```jq
// Testing whether a selection contains elements.
if ( $( "div.foo" ).length ) {
    ...
}
```

####����ѡ����
jQuery����Ϊ�㻺��,���Ҫ���ѡ��һ��Ԫ��,�Ͱ�ѡ����������һ�������
```jq
var divs = $( "div" );
```
ֱ�ӵ���divs�Ϳ����ˡ�

ѡ����ֻȡ��Щѡ��ʱ������ҳ���ϵ�Ԫ�ء����Ԫ�غ�����ӵ�ҳ�棬��ͱ����ظ�ѡ�����������ʽ��������ӵ��洢�ڱ�����ѡ�񡣴洢ѡ��DOM�仯ʱ��������ظ��¡�

####������ɸѡѡ����
```jq
// Refining selections.
$( "div.foo" ).has( "p" );         // ����<p>��ǩ��div.fooԪ��
$( "h1" ).not( ".bar" );           // class ��Ϊ bar ��h1Ԫ��
$("div").css("background", "#c8ebcc")
  .filter(".middle")
  .css("border-color", "red");	   //�ı����� div ����ɫ��Ȼ��������Ϊ "middle" ��Ԫ����ӱ߿�
$( "ul li" ).first();              // ��ӦulԪ�صĵ�һ��liԪ��
$( "ul li" ).eq( 5 );              // ������liԪ��
```

####ѡ���Ԫ��

jQuery�ṩ�˼���αѡ�������������ұ�Ԫ�ء���Щ���ر����õģ���Ϊ�����ܺ��Ѹ������ǵ�״̬��ʽ��Ԫ��֮��������֣�����ʹ�ñ�׼CSSѡ����롣

#####:checked
��Ҫ��``:checkbox``�Ի�,�������ڸ�ѡ��(checkboxes)�б�ѡ�е�Ԫ��,ͬ��������radio buttons��``<select>``Ԫ��(���ֻ��<select>,�������``:selected``).
```jq
$( "form :checked" );
```
#####:disabled
��``:disabled``αѡ���ǩѡ���κ���``disabled``���Ե�Ԫ�ء�
```jq
$( "form :disabled" );
```
#####:enabled
�����Ͼ���``:disabled``�Ķ���,``:enabled``����ѡ�������û��``disabled``���Ե�Ԫ�ء�
```jq
$( "form :enabled" );
```
Ϊ�˸���ʹ��``:enabled``,���ñ�׼jqѡ��Ԫ����ͨ��``filter()``ɸѡenabled��Ԫ��, or precede the pseudo-selector with a tag name or some other selector.

#####:input
��ѡ�����а���``<input>``,``<textarea>``,``<select>``and``<button>``Ԫ��
```jq
$( "form :input" );
```
#####:selected
ѡ������``<option>``Ԫ���ڱ�ѡ�е�Ԫ�ء�
```jq
$( "form :selected" );
```
Ϊ�˸���ʹ��``:selected``,���ñ�׼jqѡ��Ԫ����ͨ��``filter()``ɸѡselected��Ԫ��, or precede the pseudo-selector with a tag name or some other selector.

#####ͨ��type
*:password
*:reset
*:radio
*:text
*:submit
*:checkbox
*:button
*:image
*:file

###ʹ��ѡ����

####getter&setter
һЩjq�������Դӱ�ѡ��Ԫ����get��setһЩֵ�����������ô���value��Ϊ����ʱ������Ϊ��setter��Ϊ��������value���������ʱû�в�������Ϊ�Ƕ�ȡһЩֵ��setter������������ѡ���Ԫ�� ��getterֻ��������ѡ��ĵ�һ��Ԫ�ء����Ҫget����ѡ���Ԫ�ص�ֵ��``.text()``������
```jq
// ��������<h1>��valueΪ "hello world" 
$( "h1" ).html( "hello world" );
// ��õ�һ��<h1>��ֵ
$( "h1" ).html();
// > "hello world"
```

setter���ص�һ��object����,�������������jq����,��getter�᷵���κ���Ҫ�󷵻ص�,�����㲻�ܶ�getter���ص�value��������jq������
```jq
// Attempting to call a jQuery method after calling a getter.
// This will NOT work:
$( "h1" ).html().addClass( "test" );
```

####��
������ѡ����������jq����,�䷽�����ص�valueΪobject,���������֮���������jqff������Ҫ�ֺš����ǳ�֮Ϊ����
```jq
$( "#content" ).find( "h3" ).eq( 2 ).html( "new text for the third h3!" );
```
�����Ի���:
```jq
$( "#content" )
    .find( "h3" )
    .eq( 2 )
    .html( "new text for the third h3!" );
```
�㻹����ͨ��end������һ������
```jq
$( "#content" )
    .find( "h3" )
    .eq( 2 )
        .html( "new text for the third h3!" )
        .end() // Restores the selection to all h3s in #content
    .eq( 0 )
        .html( "new text for the first h3!" );
```
����ǿ��,�������п�ʼ�ܶ���Ѿ�����,����ҲҪ����ʹ��--�����ʹ�����ᵼ�´��������޸Ļ���ԡ�û���κε�Ӳ�Թ涨��Ҫ�ж೤,����������������͡�

###Ԫ�صĲ���

####��ȡ������Ԫ�ص������Ϣ
�кܶ෽������ȥ�ı�һ��Ԫ��,����������Ǹı�HTML��value��Ԫ�ص����ԡ�jqΪ���ṩ�˼򵥵ģ���������ķ����������ͨ�� getter incarnations��ĺܶ���ͬ�ķ������õ�Ԫ�ص���Ϣ�������Ǽ��ַ���:
**.html()** �C ��ȡ������HTML������(code)
**.text()** �C ��ȡ������HTML������:HTML��������;(text)
**.attr()** �C ��ȡ���������Ե�ֵ
**.width()** �C ��ȡ�����õ�һ��Ԫ�صĿ��,����Ϊinteger
**.height()** �C ��ȡ�����õ�һ��Ԫ�صĸ߶�,����Ϊinteger
**.position()** �C ��ȡposition��Ϣ(getter only)
**.val()** �C �õ����ȡ��Ԫ�ص�ֵ

ע��:��Щ������Ӱ�����б�ѡ�񵽵�Ԫ��,���Ҫ������ĳ����Ԫ����ѡ�����������¡�
```jq
// Changing the HTML of an element.
$( "#myDiv p:first" ).html( "New <strong>first</strong> paragraph!" );
```

####�ƶ�,���ƺ�ɾ��Ԫ��
��Ȼ�ж��ַ�ʽ���ƶ�����DOMԪ�أ������õ������ַ�����
*������ѡ���Ԫ����������������һ��Ԫ����
*����һ��Ԫ�������ѡ��Ԫ�أ��������
jq�ṩ��``.insertAfter()``��``.after()``��``.insertAfter()``������ѡ���Ԫ��(���)���õ���Ϊ()�ڲ�����Ԫ��֮�󡣶�``.after()``��������Ϊ()�ڲ�����Ԫ�ط��õ�ѡ���Ԫ��֮�󡣻���һЩ��ѭ����ģʽ�ķ���:
*``.insertBefore()``and``.before()``//����ѡԪ��֮ǰ
*``.appendTo()``and``.append()``//����ѡԪ�صĽ�β(��Ȼ���ڲ�)
*``.prependTo()``and``.prepend()``//����ѡԪ�صĿ�ͷ(��Ȼ���ڲ�)

��ʲô����ȡ������ѡ��Ķ���,�Լ��Ƿ���ҪΪ����ӵ�Ԫ�ش���ο�,�����Ҫ���浽������,��һ��ʹ��ǰһ�ַ���:������ѡ���Ԫ����������������һ��Ԫ������Ϊ��Щ�������ص�����ѡ��(����)��Ԫ��:``.insertAfter()``,``.insertBefore()``,``.appendTo()``and``.prependTo()``
```jq
// Moving elements using different approaches.
 
// ���б�ĵ�һ���ŵ����һ��
var li = $( "#myList li:first" ).appendTo( "#myList" );
 
// ͬ���Ľ��
$( "#myList" ).append( $( "#myList li:first" ) );
 
// Note that there's no way to access the list item
// that we moved, as this returns the list itself.
```

####����Ԫ��
��``.appendTo()``����,������Ԫ�صĸ�������
```jq
// Making a copy of an element.
 
// �����б�ĵ�һ��Ȼ��ճ�������һ��
$( "#myList li:first" ).clone().appendTo( "#myList" );
```
�����Ҫ������ص����ݺ��¼�,��Ҫȷ��ͨ��``.clone()``�Ĳ���Ϊtrue.

####�Ƴ�Ԫ��
�����ַ���removeԪ��``.remove()``��``.detach()``,���������ȫ�Ƴ�Ԫ�صĻ�����``.remove()``,�������᷵����ɾ����Ԫ��,����㽫���ص�Ԫ�����·���ҳ����,Ԫ�ؽ�����ӵ��֮ǰ���������¼������ݡ�������ʹ��``.detach()``,�����ʹ���䷵�ص�Ԫ�����¸�ԭ��ɾ����Ԫ��(���ݺ��¼�����ɾ��)<br>

�������Ҫ����Ԫ�ض�ɾ��������,����ʹ��``.empty()``������

####������Ԫ��
�����ֱ��ʹ��``$()``����������Ԫ��
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
ע��:�����Ǳ�����,��Ȼ����������Ҫ���á�https://mathiasbynens.be/notes/reserved-keywords

����ҳ��
```jq
// Getting a new element on to the page.
 
var myNewElement = $( "<p>New element</p>" );
 
myNewElement.appendTo( "#content" );
 
myNewElement.insertAfter( "ul:last" ); // ��������ɾ������"#content"���<p>Ԫ�ء�
 
$( "ul" ).last().after( myNewElement.clone() ); //�������Ͳ���ɾ����
```
��Ҳ�����ڴ���Ԫ�ص�ͬʱ��ӵ�ҳ��,����ô���㽫�޷��õ�Ԫ�ص����á�
```jq
// Creating and adding an element to the page at the same time.
$( "ul" ).append( "<li>list item</li>" );
```
��������ӻ���ɾ޴�����ܿ���,���������Ҫ��Ӵ���Ԫ��,����ЩԪ�ش�����һ�������С�
```jq
var myItems = [];
var myList = $( "#myList" );
 
for ( var i = 0; i < 100; i++ ) {
    myItems.push( "<li>item " + i + "</li>" );
}
 
myList.append( myItems.join( "" ) );
```
####���Բ���
jq�����Բ����ܼ�,��``.attr()``Ҳ�������ڸ����ӵĲ���,������������ȷ��ֵ,Ҳ�������÷����ķ���ֵ,��ʹ�÷���ʱ���Դ�����������,��ǰѡ������indexֵ�͵�ǰ������ֵ��
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
###jQuery����

��������Ԫ�أ���ѡ�����е�Ԫ�أ���jQuery�᷵��һ��Ԫ�صļ��ϡ���࿪������Ϊ����һ�����顣����һ����0��ʼ��Ԫ������,һЩ��������ķ���,�Լ�``.length``���ԡ���ʵ�ϣ�jQuery�����Ǳ�������ӡ�

####DOM��DOMԪ��

Document Object Model (���DOM)��HTML�ĵ��ı�ʾ�������԰����κ���Ŀ��DOMԪ�ء�˵������,һ��DOMԪ�ؿ��Ա���Ϊ��һ��ƴ�յ���ҳ�������԰����ı���/��������DOMԪ�ء� DOMԪ������һ����������������``<div>``,``<a>``,��``<p>``,���Ұ�������������������``src``,``href``,``class``�ȵġ��йظ��꾡��˵�������������W3C�ٷ���DOM�淶��

����javaScriptһ��,Ԫ��Ҳ�ж�Ӧ������,����``.tagName ``��``.appendChild()``��Щ������javaScript����ҳ������Ψһ;��.

####jQuery����
jQuery�����ǿ���ֱ�Ӷ�DOM������в���,jQuery��������෽���ÿ����߲���Ҫ̫��ľ���,jQuery����ĺô�����:<br>
������ - Ԫ�صĵ��÷���������������Ӧ�̺Ͱ汾�Ĳ�ͬ����ͬ,����Ƭ�γ��Խ�``<tr>``Ԫ�ش�����һ��``target``������:
```jq
var target = document.getElementById( "target" );
target.innerHTML = "<td>Hello <b>World</b>!</td>";
```
�������¿���,��������Internet Explorer�Ĵ�����汾��ʧ�ܡ�����������£��Ƽ��ķ�����ʹ�ô�DOM�������档��``target``������װ��jQuery����,�������������������ʵ�֡�
```jq
// Setting the inner HTML with jQuery.
 
var target = document.getElementById( "target" );
 
$( target ).html( "<td>Hello <b>World</b>!</td>" );
```
���� - Ҳ�кܶ๲ͬ��DOM�����������εĴ�DOM��������ɡ������ڵõ�һ��``target ``Ԫ��֮�����һ���´�����Ԫ�ػ���һ���ܳ��ķ���:
```jq
// Inserting a new element after another with the native DOM API.
 
var target = document.getElementById( "target" );
 
var newElement = document.createElement( "div" );
 
target.parentNode.insertBefore( newElement, target.nextSibling );
```
��jQuery�ͺܷ�����:
```jq
// Inserting a new element after another with jQuery.
 
var target = document.getElementById( "target" );
 
var newElement = document.createElement( "div" );
 
$( target ).after( newElement );
```
####��Ԫ�ذ�װ��jQuert����
```jq
// Selecting all <h1> tags.
 
var headings = $( "h1" );
```
``headings ``��һ������������``<h1>``��ǩ��jQueryԪ��,�������``.length ``������֤��
```jq
// Viewing the number of <h1> tags on the page.
 
var headings = $( "h1" );
 
alert( headings.length );
```
���Ҫѡ���һ��Ԫ��,�кܶ෽��``eq()``������֮һ��
```jq
// Selecting only the first <h1> element on the page (in a jQuery object)
 
var headings = $( "h1" );
 
var firstHeading = headings.eq( 0 );
```
����``firstHeading``��һ��������ҳ���һ��``<h1>``Ԫ�ص�jQuery����,����Ϊ���,������``.html()``������``.after()``��������Ҳ������``get()``�������õ���һ��Ԫ��,Ψһ��������``get()``���صĲ���jq������DOM����,����DOM����������
```jq
// Selecting only the first <h1> element on the page.
 
var firstHeadingElem = $( "h1" ).get( 0 );
```
����,jq������������,����������������:
```jq
// Selecting only the first <h1> element on the page (alternate approach).
 
var firstHeadingElem = $( "h1" )[ 0 ];
```
``firstHeadingElem``������DOMԪ��,��ӵ��DOM���Ա���``.innerHTML``��``.appendChild()``,���ǲ���ʹ��jq��������``.html()``��``.after()``�����Ǻ��Ѷ�``firstHeadingElem ``Ԫ�ؽ��в���,�����������Ҫ�õ���.

####�������б�������jQuery�������(``===``)
һ����Ҫ��ϸ����ÿһ��jq�����Ķ�����Ψһ��,��ʹ��������ͬ�ķ�������������ȫ��ͬ��DOMԪ�ص����á�
```jq
// Creating two jQuery objects for the same element.
 
var logo1 = $( "#logo" );
var logo2 = $( "#logo" );
// Comparing jQuery objects.
 
alert( $( "#logo" ) === $( "#logo" ) ); // alerts "false"
```
����������jq����ӵ����ͬ��DOM,ͨ��``get()``��������ȷ��������DOM�Ƿ���ͬһ����
```jq
// Comparing DOM elements.
 
var logo1 = $( "#logo" );
var logo1Elem = logo1.get( 0 );
 
var logo2 = $( "#logo" );
var logo2Elem = logo2.get( 0 );
 
alert( logo1Elem === logo2Elem ); // alerts "true"
```
�ܶ���ϲ�����������ڱ���jq����ı���ʱ��``$``������ǰ��,�ⲻ��ʲô���������,�����������ֱ����������jq������DOMԪ�ء�
```jq
// Comparing DOM elements (with more readable variable names).
 
var $logo1 = $( "#logo" );
var logo1 = $logo1.get( 0 );
 
var $logo2 = $( "#logo" );
var logo2 = $logo2.get( 0 );
 
alert( logo1 === logo2 ); // alerts "true"
```
����ʹ�����������淶,����jq�����DOMԪ�ض��Ǻ���Ҫ��,DOMԪ�ز���ʹ��jq����,��֮��Ȼ���������"event.target.closest is not a function"' ���� "TypeError: Object [object Object] has no method 'setAttribute'"���ֱ���˵���������ִ���
####jq���ǻ��
��ҳ��Ԫ�ط����仯,jq���󲻻�Ըñ仯������Ӧ,�����������κθı䡣

###����
���Ա���ѡ��Ķ���,���Է��ʵ���,�ӻ�ͬ���Ķ���,jq�ṩ�˺ܶ�򵥵ķ�����
####Parents
��������``.parent()``,``.parents()``,``.parentsUntil()``and``.closest()``.
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
 
// ѡ�����еĸ�Ԫ��,������������ѡ����
 
// returns [ div.parent ]
$( "span.subchild" ).parents( "div.parent" );
 
// returns [ div.child, div.parent, div.grandparent ]
$( "span.subchild" ).parents();
 
// ѡ�����еĸ�Ԫ��,����������ѡ����ѡ���
 
// returns [ div.child, div.parent ]
$( "span.subchild" ).parentsUntil( "div.grandparent" );
 
// ѡ������ĸ�Ԫ��,ֻ��һ����
// ���Լ�Ҳ�ᱻѡ��
 
// returns [ div.child ]
$( "span.subchild" ).closest( "div" );
 
// returns [ div.child ] as the selector is also included in the search:
$( "div.child" ).closest( "div" );
```
####��Ԫ��
���ǿ���ͨ��``.children()``��``.find()``�����ҵ���Ԫ��,���ߵ����������漰�ķ�Χ,``.children()``ֻ���ҵ�ѡ�����Ԫ��,``.find()``�ҵ���Ԫ���⻹������Ԫ�ص���Ԫ�ء�
```jq
// Selecting an element's direct children:
 
// returns [ div.parent, div.surrogateParent1, div.surrogateParent2 ]
$( "div.grandparent" ).children( "div" );
 
// Finding all elements within a selection that match the selector:
 
// returns [ div.child, div.parent, div.surrogateParent1, div.surrogateParent2 ]
$( "div.grandparent" ).find( "div" );
```
####ͬ��Ԫ��
ʣ�µ�jq����������������ͬ��Ԫ�ص�,�м��������Ƚ�ƫ���ڱ���,``.prev()``ǰһ��ͬ��,``.next()``�ҵ���һ��ͬ��,``.siblings()``ѡ������ͬ��Ԫ�ء����к���Щ����ģʽ��ͬ�ķ���:``.nextAll()``,``.nextUntil()``,``.prevAll()``and``.prevUntil()``��
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
###CSS ��ʽ�ͳߴ�
jq�кܶ෽���ı�Ԫ�ص�CSS���ԡ�
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
����һ�����ö������.<br>

####ʹ��CSS��������ʽ��
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

####�ߴ�
jq�ṩ������޸ĺͻ�ȡԪ�سߴ��λ����Ϣ�ķ���
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
###���ݵķ���
��ᾭ����ҪΪһ��Ԫ�ش���һ������,��JavaScript,��ֻ��ͨ��������Ե�DOMԪ��,���ұ��봦����������ڴ�й©����,jq�Ϳ��԰�������Щ����.
```jq
// Storing and retrieving data related to an element.
 
$( "#myDiv" ).data( "keyName", { foo: "bar" } );
 
$( "#myDiv" ).data( "keyName" ); // Returns { foo: "bar" }
```
�κ����͵����ݶ����Դ�����Ԫ���ϡ��������ݿ���������Ϊ������Ԫ�ص���ϵ��

�ٸ�����,���������һ��list�б��һ��div֮�佨����ϵ,��div�պ���list��,���ǿ���ͨ��``.data()``(̫�ѱ��,ֱ�ӿ�����)
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
���ǿ���ͨ������ֱ��ѡ��div������Ҫ����ѡ����ѡ��div��

###ʵ�÷���
jQuery�ṩ��$�����ռ��еļ���ʵ�÷�������Щ���������ճ���ɵı��������а�����
```jq
$.trim()
```
������ͷ�ͽ�β�Ŀո�
```jq
// Returns "lots of extra whitespace"
$.trim( "    lots of extra whitespace    " );
```
```jq
$.each()
```
��������Ͷ���
```jq
$.each([ "foo", "bar", "baz" ], function( idx, val ) {
    console.log( "element " + idx + " is " + val );
});
 
$.each({ foo: "bar", baz: "bim" }, function( k, v ) {
    console.log( k + " : " + v );
});
```
``.each()``��ͬ��``$.each()``�����Ե�������ѡ����ѡ���Ԫ�ء�$().each(function(index,element){ ... })
```jq
$.inArray()
```
����Ԫ�ص�indexֵ,��������������򷵻�-1��
```jq
var myArray = [ 1, 2, 3, 5 ];
 
if ( $.inArray( 4, myArray ) !== -1 ) {
    console.log( "found it!" );
}
```
```jq
$.extend()
```
�������������Ժϲ���ǰ�����
```jq
var firstObject = { foo: "bar", a: "b" };
var secondObject = { foo: "baz" };
 
var newObject = $.extend( firstObject, secondObject );
 
console.log( firstObject.foo ); // "baz"
console.log( newObject.foo ); // "baz"

```
����㲻��ı��κδ��ݸ�``$.extend()``�Ķ��󣬴���һ���ն�����Ϊ��һ������:
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
�÷�����������(this)����Ϊ����Ķ���
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

//����
var myObject = {
    myFn: function() {
        console.log( this );
    }
};
 
$( "#foo" ).click( myObject.myFn ); // HTMLElement #foo
$( "#foo" ).click( $.proxy( myObject, "myFn" ) ); // myObject
```
####�������
��ʱ``typeof``��������ܻ���ɻ�����һ�£���˶�����ʹ��typeof���㣬jQuery�ṩ��ʵ�÷���������ȷ��һ��ֵ�����͡�
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
###����jq����ͷ�jq����
�򵥵ľͲ�˵�ˡ�������һЩ���Ե�``.each()``�õķ���
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
Posted in: Using jQuery Core
Iterating over jQuery and non-jQuery Objects
jQuery provides an object iterator utility called $.each() as well as a jQuery collection iterator: .each(). These are not interchangeable. In addition, there are a couple of helpful methods called $.map() and .map() that can shortcut one of our common iteration use cases.

link$.each()

$.each() is a generic iterator function for looping over object, arrays, and array-like objects. Plain objects are iterated via their named properties while arrays and array-like objects are iterated via their indices.

$.each() is essentially a drop-in replacement of a traditional for or for-in loop. Given:

1
2
3
var sum = 0;
 
var arr = [ 1, 2, 3, 4, 5 ];
Then this:

1
2
3
4
5
for ( var i = 0, l = arr.length; i < l; i++ ) {
    sum += arr[ i ];
}
 
console.log( sum ); // 15
Can be replaced with this:

1
2
3
4
5
$.each( arr, function( index, value ){
    sum += value;
});
 
console.log( sum ); // 15
Notice that we don't have to access arr[ index ] as the value is conveniently passed to the callback in $.each().

In addition, given:

1
2
3
4
5
var sum = 0;
var obj = {
    foo: 1,
    bar: 2
}
Then this:

1
2
3
4
5
for (var item in obj) {
    sum += obj[ item ];
}
 
console.log( sum ); // 3
Can be replaced with this:

1
2
3
4
5
$.each( obj, function( key, value ) {
    sum += value;
});
 
console.log( sum ); // 3
Again, we don't have to directly access obj[ key ] as the value is passed directly to the callback.

Note that $.each() is for plain objects, arrays, array-like objects that are not jQuery collections.

This would be considered incorrect:

1
2
3
4
// Incorrect:
$.each( $( "p" ), function() {
    // Do something
});
For jQuery collections, use .each().

link.each()

.each() is used directly on a jQuery collection. It iterates over each matched element in the collection and performs a callback on that object. The index of the current element within the collection is passed as an argument to the callback. The value (the DOM element in this case) is also passed, but the callback is fired within the context of the current matched element so the this keyword points to the current element as expected in other jQuery callbacks.

For example, given the following markup:

1
2
3
4
5
<ul>
    <li><a href="#">Link 1</a></li>
    <li><a href="#">Link 2</a></li>
    <li><a href="#">Link 3</a></li>
</ul>
.each() may be used like so:

1
2
3
4
5
6
7
8
$( "li" ).each( function( index, element ){
    console.log( $( this ).text() );
});
 
// Logs the following:
// Link 1
// Link 2
// Link 3
link The Second Argument

The question is often raised, "If this is the element, why is there a second DOM element argument passed to the callback?"

Whether intentional or inadvertent, the execution context may change. When consistently using the keyword this, it's easy to end up confusing ourselves or other developers reading the code. Even if the execution context remains the same, it may be more readable to use the second parameter as a named parameter. For example:

1
2
3
4
5
6
7
8
9
10
11
12
13
14
$( "li" ).each( function( index, listItem ) {
 
    this === listItem; // true
 
    // For example only. You probably shouldn't call $.ajax() in a loop.
    $.ajax({
        success: function( data ) {
            // The context has changed.
            // The "this" keyword no longer refers to listItem.
            this !== listItem; // true
        }
    });
 
});
link Sometimes .each() Isn't Necessary

Many jQuery methods implicitly iterate over the entire collection, applying their behavior to each matched element. For example, this is unnecessary:

1
2
3
$( "li" ).each( function( index, el ) {
    $( el ).addClass( "newClass" );
});
And this is fine:

1
$( "li" ).addClass( "newClass" );
Each <li> in the document will have the class "newClass" added.

On the other hand, some methods do not iterate over the collection. .each() is required when we need to get information from the element before setting a new value.

This will not work:

1
2
3
4
// Doesn't work:
$( "input" ).val( $( this ).val() + "%" );
 
// .val() does not change the execution context, so this === window
Rather, this is how it should be written:

1
2
3
4
$( "input" ).each( function( i, el ) {
    var elem = $( el );
    elem.val( elem.val() + "%" );
});
The following is a list of methods that require .each():

.attr() (getter)
.css() (getter)
.data() (getter)
.height() (getter)
.html() (getter)
.innerHeight()
.innerWidth()
.offset() (getter)
.outerHeight()
.outerWidth()
.position()
.prop() (getter)
.scrollLeft() (getter)
.scrollTop() (getter)
.val() (getter)
.width() (getter)
Note that in most cases, the "getter" signature returns the result from the first element in a jQuery collection while the setter acts over the entire collection of matched elements. The exception to this is .text() where the getter signature will return a concatenated string of text from all matched elements.

In addition to a setter value, the attribute, property, CSS setters, and DOM insertion "setter" methods (i.e. .text() and .html()) accept anonymous callback functions that are applied to each element in the matching set. The arguments passed to the callback are the index of the matched element within the set and the result of the 'getter' signature of the method.

~~���벻��~~
```jq
$( "input" ).each( function( i, el ) {
    var elem = $( el );
    elem.val( elem.val() + "%" );
});
 
$( "input" ).val(function( index, value ) {
    return value + "%";
});
```
������һ����
