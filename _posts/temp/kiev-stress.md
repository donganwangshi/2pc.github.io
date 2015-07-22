

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
