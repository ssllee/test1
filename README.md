web项目解决XSS跨站脚本漏洞

maven项目解决方式需要配置如下：

一、web.xml

<!--防Xss start-->
	<filter>
        <filter-name>XSSChecker</filter-name>
        <filter-class>com.watchme.login.filter.RedSwallowFilterNew</filter-class>
        <init-param>
            <param-name>redswallow.filter.plugin.htmlescapechar.config.includeParamPatterns</param-name>
            <param-value>service,staffId,STAFF_ID,cond_SERIAL_NUMBER,default_pagin_pagesize,EXEC_TIME,FINISH_DATE,sp,Listener,CLIENT_WIDTH,lh_type,listener,ROUTE_VALUE,contextCode,_tradeBase
            </param-value>
        </init-param>
        <init-param>
            <param-name>redswallow.filter.charset</param-name>
            <param-value>GBK</param-value>
        </init-param>
	 </filter>
	 <filter-mapping>
        <filter-name>XSSChecker</filter-name>
        <url-pattern>/*</url-pattern>
	 </filter-mapping>
	 
	 <filter>
        <filter-name>CharacterFilter</filter-name>
        <filter-class>com.watchme.login.filter.CharacterFilter</filter-class>
        <init-param>
          <param-name>unCheckURLS</param-name>
          <param-value>
             (/.*hotspot/saveHotspot*$)|(/.*product/editProductManager*$)|(/.*product/addProductManager*$)
             |(/.*product/addMarketActivity*$)|(/.*product/editProductManager*$)|(/.*product/addProjectCase*$)
             |(/.*product/editProductManager*$) |(/.*product/productSearchDetail*$)|(/.*product/editProductInfo*$)
             |(/.*\.js$)|(/.*\.css$)|(/.*\.png$)|(/.*\.jpg$)|(/.*\.gif$)|(/.*\.ico$)
          </param-value>
        </init-param>
	 </filter>
	 <!--防Xss end-->

二、pom.xml
<!--防Xss--> 
		<dependency>  
		    <groupId>org.redswallow</groupId>  
		    <artifactId>redswallow</artifactId>  
		    <version>0.9.1</version>  
		</dependency> 
