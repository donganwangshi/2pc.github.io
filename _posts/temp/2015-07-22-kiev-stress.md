

# GZIP 压缩
2015-07-22 11:25:15 ready to start client benchmark,server is ,concurrents is: 100,clientNums is: 1,requestSize is:10500 bytes,the benchmark will end at:2015-07-22 11:28:15
----------Benchmark Statistics--------------
 Concurrents: 100
 ClientNums: 1
 RequestSize: 10500 bytes
 Runtime: 180 seconds
 Benchmark Time: 141
 Requests: 716937 Success: 100% (716937) Error: 0% (0)
 Avg TPS: 4874 Max TPS: 5107 Min TPS: 4591
 Avg RT: 20ms
 RT <= 0: 0% 0/716937
 RT (0,1]: 0% 0/716937
 RT (1,5]: 0% 6/716937
 RT (5,10]: 0% 3409/716937
 RT (10,50]: 99% 713522/716937
 RT (50,100]: 0% 0/716937
 RT (100,500]: 0% 0/716937
 RT (500,1000]: 0% 0/716937
 RT > 1000: 0% 0/716937

# 不使用压缩
 2015-07-22 11:29:45 ready to start client benchmark,server is ,concurrents is: 100,clientNums is: 1,requestSize is:10500 bytes,the benchmark will end at:2015-07-22 11:32:45
----------Benchmark Statistics--------------
 Concurrents: 100
 ClientNums: 1
 RequestSize: 10500 bytes
 Runtime: 180 seconds
 Benchmark Time: 141
 Requests: 914912 Success: 100% (914912) Error: 0% (0)
 Avg TPS: 6204 Max TPS: 6605 Min TPS: 5590
 Avg RT: 16ms
 RT <= 0: 0% 0/914912
 RT (0,1]: 0% 0/914912
 RT (1,5]: 0% 0/914912
 RT (5,10]: 0% 0/914912
 RT (10,50]: 100% 914912/914912
 RT (50,100]: 0% 0/914912
 RT (100,500]: 0% 0/914912
 RT (500,1000]: 0% 0/914912
 RT > 1000: 0% 0/914912

#  5*1024大小才压缩

# 1024bytes
 2015-07-23 05:47:33 ready to start client benchmark,server is ,concurrents is: 100,clientNums is: 1,requestSize is:1024 bytes,the benchmark will end at:2015-07-23 05:50:33
----------Benchmark Statistics--------------
 Concurrents: 100
 ClientNums: 1
 RequestSize: 1024 bytes
 Runtime: 180 seconds
 Benchmark Time: 141
 Requests: 5894766 Success: 100% (5894766) Error: 0% (0)
 Avg TPS: 39830 Max TPS: 42919 Min TPS: 35832
 Avg RT: 2ms
 RT <= 0: 0% 0/5894766
 RT (0,1]: 0% 6341/5894766
 RT (1,5]: 99% 5839449/5894766
 RT (5,10]: 0% 27973/5894766
 RT (10,50]: 0% 21003/5894766
 RT (50,100]: 0% 0/5894766
 RT (100,500]: 0% 0/5894766
 RT (500,1000]: 0% 0/5894766
 RT > 1000: 0% 0/5894766

# 2024bytes 网络49MB/s   cpu:193 mem:7.1
2015-07-23 06:07:33 ready to start client benchmark,server is ,concurrents is: 100,clientNums is: 1,requestSize is:2024 bytes,the benchmark will end at:2015-07-23 06:10:33
----------Benchmark Statistics--------------
 Concurrents: 100
 ClientNums: 1
 RequestSize: 2024 bytes
 Runtime: 180 seconds
 Benchmark Time: 141
 Requests: 3533713 Success: 100% (3533713) Error: 0% (0)
 Avg TPS: 23958 Max TPS: 25064 Min TPS: 21586
 Avg RT: 4ms
 RT <= 0: 0% 0/3533713
 RT (0,1]: 0% 0/3533713
 RT (1,5]: 96% 3407458/3533713
 RT (5,10]: 3% 109867/3533713
 RT (10,50]: 0% 16388/3533713
 RT (50,100]: 0% 0/3533713
 RT (100,500]: 0% 0/3533713
 RT (500,1000]: 0% 0/3533713
 RT > 1000: 0% 0/3533713



# 4048bytes 网络57MB/s   cpu:168 mem:6.9
2015-07-23 05:52:46 ready to start client benchmark,server is ,concurrents is: 100,clientNums is: 1,requestSize is:4024 bytes,the benchmark will end at:2015-07-23 05:55:46
----------Benchmark Statistics--------------
 Concurrents: 100
 ClientNums: 1
 RequestSize: 4024 bytes
 Runtime: 180 seconds
 Benchmark Time: 141
 Requests: 2109720 Success: 100% (2109720) Error: 0% (0)
 Avg TPS: 14235 Max TPS: 15234 Min TPS: 12362
 Avg RT: 7ms
 RT <= 0: 0% 0/2109720
 RT (0,1]: 0% 0/2109720
 RT (1,5]: 0% 1116/2109720
 RT (5,10]: 99% 2090694/2109720
 RT (10,50]: 0% 17910/2109720
 RT (50,100]: 0% 0/2109720
 RT (100,500]: 0% 0/2109720
 RT (500,1000]: 0% 0/2109720
 RT > 1000: 0% 0/2109720

# 5124bytes 网络2.8MB/s   cpu:150 mem:6.9
2015-07-23 05:57:16 ready to start client benchmark,server is ,concurrents is: 100,clientNums is: 1,requestSize is:5124 bytes,the benchmark will end at:2015-07-23 06:00:16
----------Benchmark Statistics--------------
 Concurrents: 100
 ClientNums: 1
 RequestSize: 5124 bytes
 Runtime: 180 seconds
 Benchmark Time: 141
 Requests: 1851550 Success: 100% (1851550) Error: 0% (0)
 Avg TPS: 12554 Max TPS: 12817 Min TPS: 12207
 Avg RT: 7ms
 RT <= 0: 0% 0/1851550
 RT (0,1]: 0% 8/1851550
 RT (1,5]: 1% 26352/1851550
 RT (5,10]: 95% 1765916/1851550
 RT (10,50]: 3% 59274/1851550
 RT (50,100]: 0% 0/1851550
 RT (100,500]: 0% 0/1851550
 RT (500,1000]: 0% 0/1851550
 RT > 1000: 0% 0/1851550

# 5524bytes 网络2.52MB/s   cpu:146 mem:6.8
2015-07-23 06:02:50 ready to start client benchmark,server is ,concurrents is: 100,clientNums is: 1,requestSize is:5524 bytes,the benchmark will end at:2015-07-23 06:05:50
----------Benchmark Statistics--------------
 Concurrents: 100
 ClientNums: 1
 RequestSize: 5524 bytes
 Runtime: 180 seconds
 Benchmark Time: 141
 Requests: 1724530 Success: 100% (1724530) Error: 0% (0)
 Avg TPS: 11713 Max TPS: 12090 Min TPS: 11076
 Avg RT: 8ms
 RT <= 0: 0% 0/1724530
 RT (0,1]: 0% 1/1724530
 RT (1,5]: 1% 24145/1724530
 RT (5,10]: 94% 1623911/1724530
 RT (10,50]: 4% 76473/1724530
 RT (50,100]: 0% 0/1724530
 RT (100,500]: 0% 0/1724530
 RT (500,1000]: 0% 0/1724530
 RT > 1000: 0% 0/1724530

# 8192bytes 网络1.69MB/s   cpu:169 mem:7.0
2015-07-23 06:13:15 ready to start client benchmark,server is ,concurrents is: 100,clientNums is: 1,requestSize is:8192 bytes,the benchmark will end at:2015-07-23 06:16:15
----------Benchmark Statistics--------------
 Concurrents: 100
 ClientNums: 1
 RequestSize: 8192 bytes
 Runtime: 180 seconds
 Benchmark Time: 141
 Requests: 1047387 Success: 100% (1047387) Error: 0% (0)
 Avg TPS: 7079 Max TPS: 8383 Min TPS: 6094
 Avg RT: 14ms
 RT <= 0: 0% 0/1047387
 RT (0,1]: 0% 0/1047387
 RT (1,5]: 0% 1890/1047387
 RT (5,10]: 12% 131984/1047387
 RT (10,50]: 87% 913342/1047387
 RT (50,100]: 0% 71/1047387
 RT (100,500]: 0% 100/1047387
 RT (500,1000]: 0% 0/1047387
 RT > 1000: 0% 0/1047387

---

#  10*1024大小才压缩
# 8192bytes 网络61MB/s   cpu:190 mem:6.9
2015-07-23 06:18:38 ready to start client benchmark,server is ,concurrents is: 100,clientNums is: 1,requestSize is:8192 bytes,the benchmark will end at:2015-07-23 06:21:38
----------Benchmark Statistics--------------
 Concurrents: 100
 ClientNums: 1
 RequestSize: 8192 bytes
 Runtime: 180 seconds
 Benchmark Time: 141
 Requests: 1144589 Success: 100% (1144589) Error: 0% (0)
 Avg TPS: 7718 Max TPS: 8285 Min TPS: 6646
 Avg RT: 12ms
 RT <= 0: 0% 0/1144589
 RT (0,1]: 0% 0/1144589
 RT (1,5]: 0% 0/1144589
 RT (5,10]: 0% 20/1144589
 RT (10,50]: 99% 1144469/1144589
 RT (50,100]: 0% 0/1144589
 RT (100,500]: 0% 100/1144589
 RT (500,1000]: 0% 0/1144589
 RT > 1000: 0% 0/1144589
