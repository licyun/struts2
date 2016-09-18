##struts2配合jquery 的ajax实现数据交互及异步加载
###1.action中需要返回一个二进制的inputstream流
```java
  	//判断用户名、密码，生成对应的响应
		inputStream = user.equals("crazyit.org") && pass.equals("leegang")
			? new ByteArrayInputStream("恭喜你，登录成功!"
				.getBytes("UTF-8"))
			: new ByteArrayInputStream("对不起，用户名、密码不匹配！"
				.getBytes("UTF-8"));
```
###2.struts.xml中指定返回文件的参数
```xml
  	<result name="success" type="stream">
		<!-- 指定下载文件的文件类型 -->
		<param name="contentType">text/html</param>
		<!-- 指定由getResult()方法返回输出结果的InputStream -->
		<param name="inputName">result</param>
	</result>
```
###3.jsp中配合jquery的ajax实现数据交互,主要使用$.get()获取数据
```javascript
	//为id为loginBn的按钮绑定事件处理函数
	$("#loginBn").click(function()
	{
		//指定向loginPro发送请求，以id为loginForm表单里各表单控件作为请求参数
		$.get("loginPro" , $("#loginForm").serializeArray() , 
			//指定回调函数
			function(data , statusText)
			{
				$("#show").height(80)
					.width(300)
					.css("border" , "1px solid black")
					.css("background-color" , "#efef99")
					.css("color" , "#ff0000")
					.css("padding" , "20px")
					.empty();
				$("#show").append("登录结果：" + data + "<br />");
				$("#show").show(2000);
			},
			//指定服务器响应为html
			"html");
	});
```
