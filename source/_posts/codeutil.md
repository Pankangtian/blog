---
title: 验证码生成工具
date: 2018-08-28 20:56:00
tags: 
	- 工具
	- 验证码
	
categories: [Java 工具]

---
本验证码生成采用的是Google提供的第三方KAPTCHA服务，使用及其方便，使用步骤分为以下三步：   
1.添加依赖  在pom.xml文件中添加

	 <dependency>
            <groupId>com.google.code.kaptcha</groupId>
            <artifactId>kaptcha</artifactId>
            <version>2.3</version>
        </dependency>

2.在web.xml中配置servlet,可根据注释酌情配置
	
	    <servlet>
        <!-- 生成图片的Servlet -->
        <servlet-name>Kaptcha</servlet-name>
        <servlet-class>com.google.code.kaptcha.servlet.KaptchaServlet</servlet-class>

        <!-- 是否有边框 -->
        <init-param>
            <param-name>kaptcha.border</param-name>
            <param-value>no</param-value>
        </init-param>
        <!-- 字体颜色 -->
        <init-param>
            <param-name>kaptcha.textproducer.font.color</param-name>
            <param-value>red</param-value>
        </init-param>
        <!-- 图片宽度 -->
        <init-param>
            <param-name>kaptcha.image.width</param-name>
            <param-value>135</param-value>
        </init-param>
        <!-- 使用哪些字符生成验证码 -->
        <init-param>
            <param-name>kaptcha.textproducer.char.string</param-name>
            <param-value>ACDEFHKPRSTWX345679</param-value>
        </init-param>
        <!-- 图片高度 -->
        <init-param>
            <param-name>kaptcha.image.height</param-name>
            <param-value>50</param-value>
        </init-param>
        <!-- 字体大小 -->
        <init-param>
            <param-name>kaptcha.textproducer.font.size</param-name>
            <param-value>43</param-value>
        </init-param>
        <!-- 干扰线的颜色 -->
        <init-param>
            <param-name>kaptcha.noise.color</param-name>
            <param-value>black</param-value>
        </init-param>
        <!-- 字符个数 -->
        <init-param>
            <param-name>kaptcha.textproducer.char.length</param-name>
            <param-value>4</param-value>
        </init-param>
        <!-- 使用哪些字体 -->
        <init-param>
            <param-name>kaptcha.textproducer.font.names</param-name>
            <param-value>Arial</param-value>
        </init-param>
    </servlet>

    <servlet-mapping>
        <servlet-name>Kaptcha</servlet-name>
        <url-pattern>/Kaptcha</url-pattern>
    </servlet-mapping>


3.为了方便使用，此处已经将判断验证码写成了方法。前端传进来的参数验证码key必须为verifyCodeActual

	public static boolean checkVerifyCode(HttpServletRequest request) {
		String verifyCodeExpected = (String) request.getSession().getAttribute(
				com.google.code.kaptcha.Constants.KAPTCHA_SESSION_KEY);
		String verifyCodeActual = request.getParameter("verifyCodeActual");
		if (verifyCodeActual == null
				|| !verifyCodeActual.equalsIgnoreCase(verifyCodeExpected)) {
			return false;
		}
		return true;
	}

4.前端部分代码如下 (仍需自定义填写验证码的输入框，并将其参数以verifyCodeActual为key传给后端：  
	
	<img sr="/Kaptcha"  /> <!-- src 为web.xml配置的拦截路径 -->

	function changeVerifyCode(img) {
	img.src = "../Kaptcha?" + Math.floor(Math.random() * 100);
	}