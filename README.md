ejs
===

我的前后端通用模板，既可以自动变成jQuery插件,也可以单独为一个前端模板,亦可以是独立的node.js模板

前端默认是使用<& &>做定界符
后端默认是使用<% %>做定界符

过滤器的使用，它只能出现<%= <&这样的左定界符内，操作对象是字符串，数组等， 我们在它后面跟一个“|”当分隔符，后面跟过滤器的名字。
过滤器都定义在$.ejs.filters之内，现在已赠送escape，unescape这两个处理字符串的过滤器，相实就我是我的lang模块的
$.String.escapeHTML与$.String.unescapeHTML。更多过滤器自己可以到https://github.com/RubyLouvre/newland/blob/master/system/mass/lang.js
中自由提取
<pre>
<&= "<aaaa>" | escape  &>
</pre>

视图helper的使用，它相当于一种独立的函数，但它通常由框架提供的与action紧密相连的辅助方法。目的是将大量的业务代码移出模板，实现重用。它会在编译时一起写进模板中

如
<pre>
var set_link = function(text, url){
  return '<a href="'+url+'">'+text +'</a>'
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
<p>本模板不使用with与eval！</p>



具体见 http://www.cnblogs.com/rubylouvre/archive/2012/08/06/2624970.html