---
layout: post
category : 分布式系统
tagline: "Supporting tagline"
tags : [zookeeper]
---
{% include JB/setup %}

## 一：名称解释
 1. tickTime：是一个基准时间，单位是豪秒。<br>(a).leader每隔tickTime/2就发送一次ping给follower。<br>(b)session超时范围：minSessionTime>2*tickTime,maxSessionTimeout<20*ticktime
 即5*2000=10000ms=10s.
 2. syncLimit: 该参数配置leader和follower之间发送消息, 请求和应答的最大时间长度. 此时该参数设置为2, 说明时间限制为2倍tickTime, 即4000ms.如果超过这个时间，则在判断的时候，超过一半没有响应，则Leader进入Looking状态，重新选举。
 3. initLimit: zookeeper集群中的包含多台server, 其中一台为leader, 集群中其余的server为follower. initLimit参数配置初始化连接时, follower和leader之间的最长心跳时间. 此时该参数设置为5, 说明时间限制为5倍tickTime,
 4. Leader端: 同步前与follower设置initLimit×tickTime的读取超时。同步后设置为syncLimit×tickTime读超时。
    Follower端: 同步前与Leader设置initLimit×tickTime的读取超时。同步后设置为syncLimit×tickTime读超时。
 5. maxClientCnxns:同一个客户端（同ip）连接数，默认是60，设置0为不限制
 6. autopurge.snapRetainCount=4，清理剩下文件数
 7. autopurge.purgeInterval=1清理间隔，单位小时
 8. 


## 二：总结

 - 镜像和日志
 > 
 - zxid
     1.名称解析：
> zk状态的每一次改变，都对应着一个递增的transaction id,该id称为zxid.由于zxid的递增性质，如果zxid1小于zxid2,那么zxid1肯定在zxid2前发生。

    2.zxid为一64位数字，高32位为leader信息又称为epoch，每次leader转换时递增；低32位为消息编号，Leader转换时应该从0重新开始编号
     3.客户端请求时zxid是为空的，即0xffffffffffffffff。
     4.啥时候递增zxid？在哪里递增？
> zk状态变化的时候发生（也即创建节点，更新节点，删除节点，客户端连接，客户端关闭连接等这种操作）。
在leader的preprocessor中创建事务时递增zxid。

 - 重启
 - 同步过程
   > 1.先比较确定zxid。
   > 2.在learnerHandler中比较，
    >> a.是否有commitlog?
    有：(1)在mixcommitlog和maxcommitlog之间，则同步投票和commitlog,(2)大于maxcommitlog，则先trunc。（3）,则一致则DIFF。
    无：follower的zxid是否和leader.zk.lastProcessId一致，一致则已经同步，不一致则同步镜像
    b.一致，发送DIFF
    c.否则发送SNAP(同步镜像)

---
##  三：选举

 原则：
 > 当server接受到的”提议”消息中,epoch大于或者等于当前server本地的logicalclock时,server会对此”提议”进行校验,如果检验成功,将会将本地持有的提议信息替换.[注意,此处为server之间信息比较,而非比较”投票”信息],依次比较epoch,zxid,sid.
 
 状态变化：
 （1）leader:每隔1s（即tickTime/2）向所有follower和observer发送一次ping。
 当超过tickTime×syncLimit秒(即10s)还没有回答响应，这关闭这个follower/observer。
 tickTime秒(即2s)判断一次，在syncLimit秒（即5s）内follower响应少于半数，则leader就进行重新选举。
 （2）observer:tickTime*initLimit(即20s)秒内没有读到数据，则进行选举。
 （3）follower:tickTime*initLimit(即20s)秒内没有读到数据，则进行选举。



### 客户端
 > 连接超时：connectiontime=sessiontimeout/servers, <br>读超时：readtimeout=sessiontimeout*2/3
 例子：sessiontimeout=30000,则connectiontime=10000,readtimeout=20000
 

 1. 客户端有两个线程：
     > （1）ClientCnxn.EventThread事件处理线程
       （2）ClientCnxn.SendThread连接线程
 2. 客户端IO线程异常：
（1）SessionTimeoutException:连接超时 或者已经连接后规定时间内没有收到响应（没有发送业务操作的时候，会发送ping）。
（2）EndOfStreamException：读取的数据长度小于0。一般是server关闭了连接
（3）SessionExpiredException：连接后，初始化session时，服务端返回的timeout<=0。
（4）RWServerFoundException：
（5）Throwable：


----------


#### 3. wather流程：
(1)将watcher实例包装成WatchRegistration，添加到watchManager中，并设置请求×××Request的watch设置成true。并序列化发送给服务端<br>
(2)触发时，客户端接收到xid=-1的消息，然后反序列化WatcherEvent对象，包装成WatchedEvent对象，并从watchManager中查找到对应的wather添加到EventThread线程队列waitingEvents<br>
(3)EventThread线程从队列waitingEvents中取出，然后判断是否是WatcherSetEventPair类型，是则执行wather。<br>
 4. wather类型：
 (1). 共有四种操作的可以设置wather:
 > (a)zookeeper,实例化zookeeper对象时设置，这个也是默认wather。 
(b)exists
(c)getData：节点不存在，报异常
(d)getChildren：节点不存在，报异常
即在设置getData和getChildren Watcher的时候，节点必须已经存在，否则会设置失败。<br> 
(2).共有5种事件类型（客户端触发的map集合）：
>   None (-1),会话创建/会话过期/连接断开，会话创建时触发，
    NodeCreated (1)：创建节点事件，触发dataWatches和existWatches
    NodeDeleted (2)：删除节点事件，触发dataWatches和existWatches和childWatches（路径就是父了）
    NodeDataChanged (3)：节点数据变更事件，触发dataWatches和existWatches
    NodeChildrenChanged (4)：节点的（添加子节点/删除子节点）事件，触发childWatches（路径就是父了）
    当会话过期（或者连接断开）时，会触发该会话的所有临时节点执行删除操作，从而执行watcher。

 5. wather存储：
    watcher存储在ZKWatchManager的3个map中，分别是这3个existWatches，dataWatches，childWatches Map。
下面3个registration分别对象设置watcher的包装类，等这3个操作服务端返回时根据返回的ReplyHeader.err值，然后再确定添加到上面那个map:
（a）zk.exists(...,watcher)：<br>对应ExistsWatchRegistration 如果ReplyHeader.err=0添加到dataWatches，ReplyHeader.err=NONODE(-101)添加到existWatches
（b）DataWatchRegistration:zk.getData(...,watcher),如果ReplyHeader.err=0添加到dataWatches
（c）ChildWatchRegistration:zk.getChildren(...,watcher),如果ReplyHeader.err=0添加到childWatches

> 例子：    zookeeper.exists("/xnd",new Watcher(){}),
等服务端响应请求后，拿到返回的数据包，然后再把watcher注册到本地（ClientCnxn.finishPacket(packet)）。然后客户端再返回（请求过程中一直wait，等待返回结果notify）

> 一句话总结：客户端操作成功后，watcher会添加到上面3个map中的一个（具体是那个见5），触发时根据path的操作，会是5种事件中的一种，然后根据事件类型，执行map中的watcher。
 
 1. ddd

--- 
## 服务端

 2. Leader
    （1）QuorumPeer线程,选举前进行选举操作，选举完成后，向其他节点发送ping信息，一直存在。
    （2）LearnerHandler线程，选举前不存在，选举后与Follower和observer交互。
    （3）QuorumCnxManager.Listener线程，绑定选举端口，随时准备接收连接，一直存在。
    （4）QuorumCnxManager.SendWorker发送选举消息。一直存在。
    （5）QuorumCnxManager.RecvWorker接收选举消息。一直存在。
 3. Follower
    (1) QuorumPeer线程，选举前进行选举操作，选举完成后，和Leader交互，并且和learnerhandler配对
   （2）QuorumCnxManager.Listener线程，绑定选举端口，随时准备接收连接，一直存在。
   （3）QuorumCnxManager.SendWorker发送选举消息。一直存在。
   （4）QuorumCnxManager.RecvWorker接收选举消息。一直存在。
 4. Observer
    (1) QuorumPeer线程，选举前进行选举操作，选举完成后，和Leader交互，并且和learnerhandler配对
 5. 服务端超时流程（session过期）
    (1) follower会定时把存活的session通过ping附加给leader,leader的SessionTrackerImpl线程定时判断,到了过期时间还没有更新就过期了，清理session。发送closeSession消息给所有follower。
 6. 怎么确定谁（leader或者follower）转发消息给客户端？<br> request在转发的时候是没有附带客户端信息，但commitprocess的processRequest（request）的时候，request是带ServerCnxn的，所以能够确定那个follower跟客户端response。
 7. session reopen流程？<br>
    客户端发送带sessionid的请求到服务端，<br>(1).如果接收信息的是leader,则直接进行touchSession(),如果session存在，则更新session过期时间，并返回true。<br>(2).如果接收信息是follower，则转发消息到leader,消息类型(REVALIDATE),leader收到消息后，leader同样调用touchSession()，...。然后在把信息返回给follower（刚刚发送过来的follower）。<br>(3).最后1和2都将调用finishSessionInit()将消息返回给客户端(reopen成功，则发送sessionid和sessiontimeout,否则这两个值都是0)。(4).注意：如果连接的是follower，这个地方不需要维护本地的session,因为在follower端更新session是添加操作，然后在传送到leader进行管理的。
 8. watcher:
（1）watcher注册和触发流程？（拿exists举例）<br>
    a.服务端接收到客户端请求，反序列化为Request对象，然后进入RequestProcessor流程。
    b.进入FinalRequestProcessor处理类，继续反序列化为ExistsRequest对象，然后拿出watch属性，如果为ture，则添加到DataTree中的dataWatches中（key=path,value=NIOServerCnxn）。
    c.触发时，发送type=notification消息xid=-1,数据为WatcherEvent的对象（包含状态，类型和Path）
 （2）watcher在服务端的触发：
    a.dataWatches,创建/删除/更新节点，对应EventType:NodeCreated (1),NodeDeleted (2),NodeDataChanged (3),
    b.childWatches,子节点新增时父节点/子节点删除/子节点删除时父节点
 9. Leader或者Follower啥时候接收客户端请求？
 （1）接收客户端端口绑定后，就可以接收客户端请求，但在zookeeperserver没有启动前，不会接收客户端，因为ServerCnxnFactory关联的zookeeperserver对象为null,直接关闭连接。
 （2）Follower在同步后接收到Leader.UPTODATE请求后，将FollowerZookeeperServer设置到ServerCnxnFactory中，则可以接收客户端请求了。
 （3）Leader在发送完NEWLEADER后等待答复后，启动LeaderZooKeeperServer，然后根据zookeeper.leaderServes设置是否接收客户端连接请求（默认是接收）。
 （4）当Leader与Follower超时没有响应时，关闭连接，清理ServerCnxnFactory的zookeeperServer,进入LOOKING状态,拒绝客户端连接。
 10. 啥时候重新选举？
 （1）Leader在syncLimit×tickTime时间内收到的Follower的响应没有超过集群的1/2。
 （2）Leader挂了
 11. 

### 数据同步
Follower进入Looking后，Snap和Txn LOG合并出一个最后的zxid。然后开始选举投票。

---
### 其他一些疑问

 1. 重复创建同一个节点，会出现啥情况？
 客户端收到节点已经存在KeeperException$NodeExistsException异常，在第二次修改datatree时候，失败返回给客户端，但会记录两次事务日志（写log文件），这是没有问题的，在进行日志回放时，结果跟现在的datatree一致，所以没有问题。
 2. 

---



研究zk相关的文章
### 1.存储
[zookeeper 存储之文件格式分析][1]
[zookeeper的快照和日志的关系snapshot和log][2]
[zookeeper存储之实现分析-----------------------------------重要][3]
### 2.命令
[Zookeeper常用命令][4]
### 3.运维
[ZooKeeper运维之使用SnapshotFormatter可视化快照数据][5]
### 4.协议
[Zookeeper的一致性协议：Zab][6]
### 5.同步
[zookeeper的数据存储和同步][7]
[zookeeper源码分析:Leader与Follower同步数据流程][8]
### 6.测试/压测
[zookeeper节点数与watch的性能测试][9]

[1]: http://blog.csdn.net/pwlazy/article/details/8080626
[2]: http://hi.baidu.com/jiaozhenqing/item/8f4721f7e0c88e2c743c4c9f
[3]: http://blog.csdn.net/pwlazy/article/details/8137121
[4]: http://blog.csdn.net/xiaolang85/article/details/13021339
[5]: http://nileader.blog.51cto.com/1381108/983259
[6]: http://blog.csdn.net/chen77716/article/details/7309915
[7]: http://www.zhouyoudao.com/zookeeper-data/
[8]: http://www.chepoo.com/zookeeper-code-analysis-leader-follower.html
[9]: http://codemacro.com/2014/09/21/zk-watch-benchmark/
