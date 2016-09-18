# downDemo
##struts2实现下载中文及用struts.xml控制授权下载
###1.直接下载出现中文乱码，使用DownloadAction中的getTargetFile()从struts.xml中获取inputPath初始值,并返回一个InputStream,交由struts.xml控制下载
```java
  		<action name="download" class="org.crazyit.app.action.FileDownloadAction">
		<!-- 指定被下载资源的位置 -->
			<param name="inputPath">\images\疯狂联盟.jpg</param>
			<!-- 配置结果类型为stream的结果 -->
			<result name="success" type="stream">
				<!-- 指定下载文件的文件类型 -->
				<param name="contentType">image/jpg</param>
				<!-- 指定由getTargetFile()方法返回被下载文件的InputStream -->
				<param name="inputName">targetFile</param>
				<param name="contentDisposition">filename="wjc_logo.jpg"</param>
				<!-- 指定下载文件的缓冲大小 -->
				<param name="bufferSize">4096</param>
			</result>
		</action>
```
###2.授权下载在AuthorityDownloadAction中判断sessoin的用户名是否正确，正确返回success，然后交由struts.xml控制下载。
```java
  		<action name="download2" class="org.crazyit.app.action.AuthorityDownAction">
			<!-- 定义被下载文件的物理资源 -->
			<param name="inputPath">\images\wjc_logo.zip</param>
			<result name="success" type="stream">
				<!-- 指定下载文件的文件类型 -->
				<param name="contentType">application/zip</param>
				<!-- 指定由getTargetFile()方法返回被下载文件的InputStream -->
				<param name="inputName">targetFile</param>
				<param name="contentDisposition">filename="wjc_logo.zip"</param>
				<!-- 指定下载文件的缓冲大小 -->
				<param name="bufferSize">4096</param>
			</result>
			<!-- 定义一个名为login的结果 -->
			 <result name="login">/WEB-INF/content/login.jsp</result>
		</action>
```
