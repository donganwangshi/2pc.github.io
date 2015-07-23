---
layout: post
category : performance
tagline: "Supporting tagline"
tags : [jprofiler]
---
{% include JB/setup %}


# 配置
> 需要在远程机器JAVA启动处添加agentpath.如下:
Integration type: [Generic application server]
Selected JVM: Oracle 1.8.0 (hotspot)
Startup mode: Startup immediately, connect later with the JProfiler GUI

(1) Please insert

-agentpath:/data/soft/jprofiler9/bin/linux-x64/libjprofilerti.so=port=8849,nowait

into the start command of your application server right after the java command.

A remote session named Application server on 172.16.82.174 will be created that connects to a running instance of the application server that is started with the modified start command.
