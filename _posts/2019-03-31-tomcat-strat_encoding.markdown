# tomcat启动日志中文乱码解决

> 修改conf文件下logging.properties  路径: apache-tomcat-9.0.17\conf\logging.properties  

   
  找到下面这一行将其编码改为GBK     
  
  java.util.logging.ConsoleHandler.encoding = UTF-8      
  
  修改后    
  
  java.util.logging.ConsoleHandler.encoding = GBK
