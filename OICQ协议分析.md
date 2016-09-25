#OICQ协议分析

##1 - Get status of friend
note: 心跳包  
###remote server -> localhost  
Length:	**121**  
UDP: 87  
OICQ: 79

``` 
[1] Flag: Oicq packet (0x02)
[2] Version: 0x3639
[2] Command: Get status of friend (129)
[2] Sequence: 25468
[4] Data(OICQ Number,if sender is client): 393148612
[68] Data: 

UDP Data: 02 3639 0081 637c 176ef8c4 000000f844...
```


##2 - Download group friend
note: 打开好友对话框时
###localhost -> remote server  
Length: **81**  
UDP: 47  
OICQ: 39  
  

```
[1] Flag: Oicq packet (0x02)
[2] Version: 0x3639
[2] Command: Download group friend (88)
[2] Sequence: 29245
[4] Data(OICQ Number,if sender is client): 393148612
[28] Data: \002

UDP Data: 02 3639 0058 723d 176ef8c4 020000000...
```

###remote server -> localhost  
Length: **89**  
UDP: 55  
OICQ: 47  

```
[1] Flag: Oicq packet (0x02)
[2] Version: 0x3639
[2] Command: Download group friend (88)
[2] Sequence: 29245
[4] Data(OICQ Number,if sender is client): 393148612
[36] Data:

UDP Data: 02 3639 0058 723d 176ef8c4 0000006a...
```





##3 - Get friend online
note: 请求-反馈 好几次  
###localhost -> remote server  
Length： **81**  

###remote server -> localhost  
Length: **about 1000** 



##4 - Send message
###localhost -> remote server  
Length: **>=193**
OICQ: **151**

```
[1] Flag: Oicq packet (0x02)
[2] Version: 0x3639
[2] Command: Send message (205)
[2] Sequence: (0x7260)
[4] Data(OICQ Number,if sender is client): 331006344
[36] Data:

UDP Data: 02 3639 00cd 7260 13bac188 02000000...

```


###remote server -> localhost 
Length: **73** 
OICQ: **31**

```
[1] Flag: Oicq packet (0x02)
[2] Version: 0x3639
[2] Command: Send message (205)
[2] Sequence: 
[4] Data(OICQ Number,if sender is client): 331006344
[36] Data:

UDP Data: 02 3639 00cd 7260 13bac188 000000d6...
```



##5 - Receive message
###remote server -> localhost 
Length: **about 217**  
OICQ: **175**  

```
[1] Flag: Oicq packet (0x02)
[2] Version: 0x3639
[2] Command: Send message (206)
[2] Sequence: (0xedf2)
[4] Data(OICQ Number,if sender is client): 331006344
[36] Data:

UDP Data: 02 3639 00ce edf2 13bac188 00000013...
```


###localhost -> remote server  
Length: **97**  
OICQ: **55**  

```
[1] Flag: Oicq packet (0x02)
[2] Version: 0x3639
[2] Command: Send message (205)
[2] Sequence: (0x7260)
[4] Data(OICQ Number,if sender is client): 331006344
[36] Data:

UDP Data:  02 3639 00ce edf213bac188 0200000001...
```

##6 - Request KEY
note: 极少
###localhost -> remote server  
Length： **81**  

###remote server -> localhost  
Length: **105**  
