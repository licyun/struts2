##struts2通过ajax异步传递json数据
###1.action中封装请求参数的属性,并set和get来序列化每个参数。
```java
  	private Map<String , String> map
		= new HashMap<String , String>();
  	private String customName = "顾客";
  	//封装请求参数的三个属性
  	private String field1;
  	//'transient'修饰的属性不会被序列化
  	private transient String field2;
  	//没有setter和getter方法的字段不会被序列化
  	private String field3;
```
###2.struts.xml中指定返回类型
```java
  		<action name="JSONExample" class="org.crazyit.app.action.JSONExample">
			<!-- 配置类型的json的Result -->
			<result type="json">
				<!-- 为该Result指定参数 -->
				<param name="noCache">true</param>
				<param name="contentType">text/html</param>
				<!-- 设置只序列Action的map属性 -->
				<!--  param name="root">map</param -->
			</result>
		</action>
```
###3.jsp中使用jquery的ajax来获取返回参数，并解析json数组
```javascript
  		function gotClick()
		{
			//请求的地址
			var url = 'JSONExample.action';
			//将favorite表单域的值转换为请求参数
			var params = Form.serialize('form1');
			//创建Ajax.Request对象，对应于发送请求
			var myAjax = new Ajax.Request(
			url,
			{
				//请求方式：POST
				method:'post',
				//请求参数
				parameters:params,
				//指定回调函数
				onComplete: processResponse,
				//是否异步发送请求
				asynchronous:true
			});
		}
		function processResponse(request)
		{
			//使用JSON对象将服务器响应解析成JSON对象
			var res = request.responseText.evalJSON();
			alert(res);
			//遍历JSON对象的每个属性
			for(var propName in res)
			{
				$("show").innerHTML += propName + " --> " 
					+ res[propName] + "<br/>";
			}		
		}	
```
