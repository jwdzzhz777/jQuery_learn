#jQuery
	����jQuery(��)
##����jQuery	
	
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

Ϊ��ȷ�����ǵĴ����������������ɼ��ظ��ļ�֮�����JavaScript����Ա��װ�Լ��Ĵ����ڵ�``onload	``��</br>

���ҵ��ǣ����벻����(����������)��ֱ������ͼ��������ϣ����������档�������д�����ļ���׼���ý��в�������Ҷ�֪��jQuery�б���Ϊ``ready``���¼�</br>

``click``�¼��п���ʹ��``event.preventDefault()``����ֹĬ����Ϊ��</br>

``addClass()``��``removeClass``

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

####ѡ���Ԫ��

jQuery�ṩ�˼���αѡ�������������ұ�Ԫ�ء���Щ���ر����õģ���Ϊ�����ܺ��Ѹ������ǵ�״̬��ʽ��Ԫ��֮��������֣�����ʹ�ñ�׼CSSѡ����롣

