# alibaba-sentinel-dashboard-nacos

### 阿里sentinel后台面板规则（包括gateway模式）持久化-推模式（nacos），基于版本v1.7.0改造
### 实现了sentinel规则 在后台控制面版与nacos之间的双向同步
#### 1、控制面板新增、编辑、删除规则时 自动同步到nacos进行持久化
#### 2、nacos新增、编辑、删除规则时 自动同步到项目和控制面板
###nacos配置说明
> application.properties
```
# nacos服务地址
spring.cloud.sentinel.datasource.nacos.server-addr=10.129.38.170:8848
# nacos配置分组id
spring.cloud.sentinel.datasource.nacos.groupId=DEFAULT_GROUP
#nacos命名空间，可不设,默认为public
spring.cloud.sentinel.datasource.nacos.namespace=public
```

###项目接入配置
``` 
spring:
  application:
    name: tmp-service
  cloud:
    sentinel:
      transport:
        #控制面板地址
        dashboard: 10.129.38.170:8999
      log:
        dir: ../logs/
      datasource:
        #流控
        flow-rules:
          nacos:
            ### nacos连接地址
            server-addr: 10.129.38.170:8848
            ### nacos连接的分组
            group-id: DEFAULT_GROUP
            ### 读取配置文件的 data-id
            data-id: ${spring.application.name}-flow-rules
            ### 读取培训文件类型为json
            data-type: json
            ### 路由存储规则
            rule-type: flow
        #降级
        degrade-rules:
          nacos:
            ### nacos连接地址
            server-addr: 10.129.38.170:8848
            ### nacos连接的分组
            group-id: DEFAULT_GROUP
            ### 读取配置文件的 data-id
            data-id: ${spring.application.name}-degrade-rules
            ### 读取培训文件类型为json
            data-type: json
            ### 路由存储规则
            rule-type: degrade
        #热点参数限流
        param-rules:
          nacos:
            ### nacos连接地址
            server-addr: 10.129.38.170:8848
            ### nacos连接的分组
            group-id: DEFAULT_GROUP
            ### 读取配置文件的 data-id
            data-id: ${spring.application.name}-param-rules
            ### 读取培训文件类型为json
            data-type: json
            ### 路由存储规则
            rule-type: param-flow
        #系统规则
        system-rules:
          nacos:
            ### nacos连接地址
            server-addr: 10.129.38.170:8848
            ### nacos连接的分组
            group-id: DEFAULT_GROUP
            ### 读取配置文件的 data-id
            data-id: ${spring.application.name}-system-rules
            ### 读取培训文件类型为json
            data-type: json
            ### 路由存储规则
            rule-type: system
        #授权规则
        authority-rules:
          nacos:
            ### nacos连接地址
            server-addr: 10.129.38.170:8848
            ### nacos连接的分组
            group-id: DEFAULT_GROUP
            ### 读取配置文件的 data-id
            data-id: ${spring.application.name}-authority-rules
            ### 读取培训文件类型为json
            data-type: json
            ### 路由存储规则
            rule-type: authority
```
