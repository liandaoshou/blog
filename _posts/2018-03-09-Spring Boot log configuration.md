---
layout: post
title:  "Spring Boot 添加日志配置 (一) "
date:   2018-03-09 14:23:00 +0800
categories: Spring Boot log configuration
tag: tools
---
#Spring Boot 添加日志配置 (一) 
@(Spring Boot)[log|slf4j|logback] 

spring.io下载或者idea生成Spring Boot
### pom.xml 添加配置
``` 
<dependency>
	<groupId>ch.qos.logback</groupId>
	<artifactId>logback-classic</artifactId>
</dependency>
<dependency>
	<groupId>org.slf4j</groupId>
	<artifactId>jcl-over-slf4j</artifactId>
</dependency>
```

### src\main\resources  添加文件 logback-spring.xml
``` 
<?xml version="1.0" encoding="UTF-8"?>  
<configuration>  
    <!--定义日志文件的存储地址 勿在 LogBack的配置中使用相对路径 -->  
    <property name="LOG_HOME" value="/log" />  
    <!-- 控制台输出 -->  
    <appender name="STDOUT" class="ch.qos.logback.core.ConsoleAppender">  
        <encoder class="ch.qos.logback.classic.encoder.PatternLayoutEncoder">  
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{30} - %msg%n</pattern>  
        </encoder>  
    </appender>  
  
    <!-- 按照每天生成日志文件 -->  
    <appender name="FILE"  
        class="ch.qos.logback.core.rolling.RollingFileAppender">  
        <rollingPolicy class="ch.qos.logback.core.rolling.TimeBasedRollingPolicy">  
            <FileNamePattern>${LOG_HOME}/logs/demo.log.%d{yyyy-MM-dd}.log</FileNamePattern>  
            <!--日志文件保留天数 -->  
            <MaxHistory>30</MaxHistory>  
        </rollingPolicy>  
        <encoder class="ch.qos.logback.classic.encoder.PatternLayoutEncoder">  
            <!--格式化输出：%d表示日期，%thread表示线程名，%-5level：级别从左显示5个字符宽度%msg：日志消息，%n是换行符 -->  
            <pattern>%d{yyyy-MM-dd HH:mm:ss.SSS} [%thread] %-5level %logger{30} - %msg%n</pattern>  
        </encoder>  
        <!--日志文件最大的大小 -->  
        <triggeringPolicy class="ch.qos.logback.core.rolling.SizeBasedTriggeringPolicy">  
            <MaxFileSize>10MB</MaxFileSize>  
        </triggeringPolicy>  
    </appender>  
       
    <!-- 日志输出级别 -->  
    <root level="INFO">  
        <appender-ref ref="STDOUT" />  
        <appender-ref ref="FILE" />  
    </root>  
  
    <!-- 定义各个包的详细路径，继承root宝的值 -->  
    <logger name="com.example.demo.controller" level="INFO" />
    <logger name="com.example.demo" level="TRACE" />
      
    <!-- 此值由 application.properties的spring.profiles.active=dev指定-->  
    <springProfile name="dev">  
        <!--定义日志文件的存储地址 勿在 LogBack 的配置中使用相对路径 -->  
        <property name="LOG_HOME" value="/log" />  
        <logger name="org.springboot.sample" level="DEBUG" />  
    </springProfile>  
    <springProfile name="pro"> 
        <!--定义日志文件的存储地址 勿在 LogBack 的配置中使用相对路径 -->  
        <property name="LOG_HOME" value="/log" />
        <logger name="org.springboot.sample" level="DEBUG" />  
    </springProfile> 
</configuration>  
``` 
### 使用示例
``` 
@RestController
public class HelloWorldController {

    private static final Logger log = LoggerFactory.getLogger(HelloWorldController.class);

    @RequestMapping("/hello")
    public String index() {
        log.info("Hello World");
        return "Hello World";
    }
}
``` 
