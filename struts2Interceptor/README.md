##struts2拦截器使用实例
## struts2拦截器在action类的excute方法执行前调用。当返回invocatioin.incoke()时进入下一个拦截器，下面没有拦截器时直接执行excute方法。
###1.struts.xml的包中定义拦截器
```java
  <package name="lee" extends="struts-default">
		<!-- 用户拦截器定义在该元素下 -->
		<interceptors>
			<!-- 定义了一个名为authority的拦截器 -->
			<interceptor name="authority" 
			class="org.crazyit.app.interceptor.AuthorityInterceptor"/>
		</interceptors>
```
###2.在struts.xml的action中使用该拦截器
```java
  <action name="viewBook">
			<!-- 返回success视图名时，
				转入/WEB-INF/content/viewBook.jsp页面 -->
			<result>/WEB-INF/content/viewBook.jsp</result>
			<interceptor-ref name="defaultStack"/>
			<!-- 应用自定义拦截器 -->
			<interceptor-ref name="authority"/>
		</action>
```
