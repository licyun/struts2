##Struts2上传文件及用filter实现文件过滤
###1.上传的jsp中需指定form格式为enctype="multipart/form-data 
###2.UploadAction中封装多个上传的文件属性并重写excute方法
```java
  @Override
  public String execute() throws Exception
  {
  	//以服务器的文件保存地址和原文件名建立上传文件输出流
  	FileOutputStream fos = new FileOutputStream(getSavePath()
  		+ "\\" + getUploadFileName());
  	FileInputStream fis = new FileInputStream(getUpload());
  	byte[] buffer = new byte[1024];
  	int len = 0;
  	while ((len = fis.read(buffer)) > 0)
  	{
  		fos.write(buffer , 0 , len);
  	}
  	fos.close();
  	return SUCCESS;
  }
```
###3.struts中对文件过滤
```java
  <interceptor-ref name="fileUpload">
	<!-- 配置允许上传的文件类型 -->
	<param name="allowedTypes">image/png
		,image/gif,image/jpeg</param>
	<!-- 配置允许上传的文件大小 -->
	<param name="maximumSize">2000000</param> 
  </interceptor-ref>
```
