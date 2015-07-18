---
layout: post
category : Unittest
tagline: "Supporting tagline"
tags : [mockito]
---
{% include JB/setup %}

# 配置依赖
```
      <dependency>
           <groupId>org.mockito</groupId>
           <artifactId>mockito-all</artifactId>
           <version>1.9.5</version>
           <scope>test</scope>
       </dependency>
       <dependency>
           <groupId>org.powermock</groupId>
           <artifactId>powermock-module-junit4</artifactId>
           <version>1.5.5</version>
           <scope>test</scope>
       </dependency>
       <dependency>
           <groupId>org.powermock</groupId>
           <artifactId>powermock-api-mockito</artifactId>
           <version>1.5.5</version>
           <scope>test</scope>
       </dependency>
       <dependency>
           <groupId>org.powermock</groupId>
           <artifactId>powermock-core</artifactId>
           <version>1.5.5</version>
           <scope>test</scope>
       </dependency>
```

# 使用

0. 准备工作
> 在测试类上添加如下内容

```
@RunWith(PowerMockRunner.class)
@PrepareForTest(Cluster.class)
public class ClusterTest {
}  

```
1. 使用
