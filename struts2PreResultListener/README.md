# preResultListener
## 1.定义action的不同方法
```java
  //为每个action写一个method 
  	<action name="regist" class="org.crazyit.app.action.LoginRegistAction"
			method="regist">
  			<!-- 定义逻辑视图和物理视图之间的映射关系 -->
  			<result name="input">/login.jsp</result>
  			<result name="error">/error.jsp</result>
  			<result name="success">/welcome.jsp</result>
	</action>
	//或使用通配符匹配，避免同一个类，相同的返回类型写多个方法(但此时form表单的action名称需要一致)
		<action name="*Action" class="org.crazyit.app.action.LoginRegistAction"
			method="{1}">
  			<!-- 定义逻辑视图和物理视图之间的映射关系 -->
  			<result name="input">/login.jsp</result>
  			<result name="error">/error.jsp</result>
  			<result name="success">/welcome.jsp</result>
		</action>
```
##2.在Action转入实际的物理视图前通过ActionInvocation的addResultListener方法完成回调。
```java
        //在action的excute方法中添加监听addPreResultListener
        ActionInvocation invocation = ActionContext
			.getContext().getActionInvocation();
		invocation.addPreResultListener(new PreResultListener() 
		{
			public void beforeResult(ActionInvocation invocation, 
				String resultCode) 
			{
				System.out.println("返回的逻辑视图名字为："
					+ resultCode);
				//在返回Result之前加入一个额外的数据。
				invocation.getInvocationContext().put("extra"
					, new java.util.Date() + "由" 
					+ resultCode + "逻辑视图名转入");
				//也可加入日志等
			}
		});
	//物理视图的jsp中使用struts的方法获取回调的属性标签
	<s:property value="extra"/>
```
