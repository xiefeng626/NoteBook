我们可以在浏览器的 Console 窗口中使用 **$.fn.jquery** 命令查看当前 jQuery 使用的版本：

![image-20201202163941072](C:\Users\HASEE\AppData\Roaming\Typora\typora-user-images\image-20201202163941072.png)

## 一、选择器

```
1、元素（标签）选择器
$("p")
2、id选择器
$("#test")
3、.class选择器
$(".test")
4、其他
$("[href]")	选取带有 href 属性的元素
$(":button") 选取所有 type="button" 的 <input> 元素 和 <button> 元素


$("p").click(function(){
  $(this).hide();
});                                  this表示当前元素
```

```
隐藏
$("button").click(function(){
  $("p").toggle();//点击隐藏或者希纳是
});
```

```
回调函数加括号立马执行 
当 callback 函数加上括号时，函数立即执行，只会调用一次， 如果不加括号，元素显示或隐藏后调用函数，才会调用多次。
```

```
$("button").click(function(){
  $("p").hide("slow",function(){
    alert("段落现在被隐藏了");
  });
});
回调就会等这边执行完了 那边才会执行
```

## 操作DOM（**Document Object Model（文档对象模型**）

```
Jquery捕获；
  取值
	text()  :文本（标签） $("#test").test()    
	html()：html代码 $("#test").html()
	val():input或者表单的值 $("#test").val()
	attr():alert($("#runoob").attr("href")); 获取属性的值
  设置
  
     $("#runoob").attr("href","http://www.runoob.com/jquery");
     
     $("p").append("追加文本");
     $("p").prepend("在开头追加文本");
     $("img").after("在后面添加文本");
	$("img").before("在前面添加文本");
	$("#div1").remove();
	$("#div1").empty();
	$("p").remove(".italic");
	
	
	下面的例子将返回首个匹配元素的 background-color 值：

实例
$("p").css("background-color");

$("p").css("background-color","yellow");
```

