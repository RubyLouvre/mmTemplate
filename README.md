ejs
===

我的前后端通用模板，既可以自动变成jQuery插件,也可以单独为一个前端模板,亦可以是独立的node.js模板

前端默认是使用<& &>做定界符
后端默认是使用<% %>做定界符

<strong>过滤器的使用</strong>，它只能出现<%= <&这样的左定界符内，操作对象是字符串，数组等， 我们在它后面跟一个“|”当分隔符，后面跟过滤器的名字。
过滤器都定义在$.ejs.filters之内，现在已赠送escape，unescape这两个处理字符串的过滤器，相实就我是我的lang模块的
$.String.escapeHTML与$.String.unescapeHTML。更多过滤器自己可以到https://github.com/RubyLouvre/newland/blob/master/system/mass/lang.js
中自由提取
<pre>
&lt;&= "&lt;aaaa&gt;" | escape  &&gt;
</pre>

<strong>视图helper的使用</strong>，它相当于一种独立的函数，但它通常由框架提供的与action紧密相连的辅助方法。目的是将大量的业务代码移出模板，实现重用。它会在编译时一起写进模板中

如
<pre>
var set_link = function(text, url){
  return '&lt;a href="'+url+'"&gt;'+text +'&lt;/a&gt;';
}

var fn = $.ejs.compile(source, {
  helpers:{
      set_link: set_link
   }
})
</pre>
那么我们就可以直接在模板中使用此方法
<pre>
&lt;&= set_link("rubylouvre","http://www.cnblogs.com/rubylouvre/") %&gt;
</pre>

<h3>模板的编译函数的缓存</h3>
<p>在前端我们可以通过选择器来缓存模板,比如</p>
<pre>
var html = $.ejs("#js_tmpl", {
   aaa:"xxx",
   bbb:[1,2,3,4]
})
</pre>
<p>它的第一个参数是CSS选择器，如果你是用jQuery或mass Framework，你可以使用jQuery的任意表达式(mass Framework完全兼容jQuery的自定义伪类)，
如果你没有使用框架，它会尝试用querySelectorAll来寻找元素，否则它使用getElementById找元素，当然它在这之前会去掉最前的#</p>
<p>总之，在前端它是使用第一个参数做模板的键，与编译好的函数作为一个键值对放在$.ejs.cache中</p>
<p>在后端，我们可以利用第三个参数的tid作为模板的键</p>
<pre>
var html = $.ejs(source, {
   aaa:"xxx",
   bbb:[1,2,3,4]
},{tid:"first_tmpl"})
</pre>

<h3>子模板的使用或layout的指定<h3>
<p>它们都是使用视图helper实现的，比如我们用include函数作为引入子模板的函数</p>
<pre>
var fn = $.ejs(source, data, {
  helpers:{
     include: $.ejs
   }
})
</pre>
<p>至于指定layout,可以详看我的newlandjs的set_layout方法与位于/app/views/...中的使用示例</p>



<p>吸收Tj大神的ejs模块的全部优点（向Tj致敬），如准确定位错误与模板套嵌。本模板不使用with与eval！</p>
<p>本模板最先在博客园公布，版本迭代已到v10，并有一批C#的忠实用户在使用，我也长期用于任职公司的内部使用，历经考验。</p>



具体见 http://www.cnblogs.com/rubylouvre/archive/2012/08/06/2624970.html