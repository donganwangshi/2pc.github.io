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
```

# 使用

1. 创建Mock对象

```
//方式一:使用注解
@Mock
Cluster clusterMock;

@Before
public void before(){
    MockitoAnnotations.initMocks(this);
}

//方式二:代码
KievClient client = mock(KievClient.class);
```
2.
