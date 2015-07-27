---
layout: post
category : performance
tagline: "Supporting tagline"
tags : [btrace]
---
{% include JB/setup %}

# btrace监控zookeeper ping
1. 下载btrace-bin.tar.gz.
2. 解压btrace
3. 执行如下命令, 将文件写到当前目录中

> btrace -cp build:/opt/zookeeper-3.4.6/zookeeper-3.4.6.jar -p 2021 8503 ZKClientTracingScript.java > zk.log&

4. 脚本代码如下:

```
package org.apache.zookeeper;
import com.sun.btrace.annotations.*;
import org.apache.zookeeper.ClientCnxn.Packet;

import java.lang.reflect.Field;
import java.nio.channels.SelectionKey;
import java.util.LinkedList;
import java.util.List;

import static com.sun.btrace.BTraceUtils.*;

@BTrace
public class ZKClientTracingScript {

    @OnMethod(
            clazz = "org.apache.zookeeper.ClientCnxnSocketNIO",
            method = "doTransport",
            location = @Location(Kind.ENTRY)
    )
    public static void traceExecute(@Self Object self, int waitTimeOut, List<Packet> pendingQueue,
                                    LinkedList<Packet> outgoingQueue, ClientCnxn cnxn) {
        // 获取对象属性值
        Field sockKey = field("org.apache.zookeeper.ClientCnxnSocketNIO", "sockKey");
        SelectionKey selectionKey = (SelectionKey) get(sockKey, self);
        Field readyOps = field("sun.nio.ch.SelectionKeyImpl", "readyOps");
        int ro = (Integer) get(readyOps, selectionKey);

        println(strcat(strcat(strcat(strcat(strcat(strcat(Time.timestamp("yyyy-MM-dd:hh mm ss SSS"), "@-waitTimeOut:"), str(waitTimeOut)), "@-outGoingQueueSize:"), str(com.sun.btrace.BTraceUtils.Collections.size(outgoingQueue))),"  @readyOps"),str(ro)));
    }

}
```
