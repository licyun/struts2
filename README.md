# exceptionHandler
##struts 的异常处理无需使用try catch块。直接抛出异常给struts框架，交给struts.xml来处理
```java
  <!-- 定义全局异常映射 -->
		<global-exception-mappings>
			<!-- 当Action中遇到SQLException异常时，
				系统将转入name为sql的结果中-->
			<exception-mapping exception="java.sql.SQLException" result="sql"/>
			<!-- 当Action中遇到Exception异常时，
				系统将转入name为root的结果中-->
			<exception-mapping exception="java.lang.Exception" result="root"/>
		</global-exception-mappings>

		<action name="login" class="org.crazyit.app.action.LoginAction">
			<!-- 定义局部异常映射， 当Action中遇到MyException异常时，
				系统将转入name为my的结果中-->
			<exception-mapping exception="org.crazyit.app.exception.MyException"
				result="my"/>
			<!-- 定义三个结果映射 -->
			<result name="my">/exception.jsp</result>
			<result name="error">/error.jsp</result>
			<result name="success">/welcome.jsp</result>
		</action>
		
		//jsp中则通过<s:property value="exceptionStack"/>来获取异常值
```
