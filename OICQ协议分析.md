#OICQ协议分析

##Get status of friend
###Command: Get status of friend (129)
remote server -> localhost  
Length:	121
UDP: 87  
OICQ: 79

```
[79]  
[1] Flag: Oicq packet (0x02)  
[2] Version: 0x3639  
[2] Command: Get status of friend (129)  
[2] Sequence: 48520  
[4] Data(OICQ Number,if sender is client): 393148612  
[68] Data: 
```

##Download group friend
###localhost -> remote server  
Length: 81  

###remote server -> localhost  
Length: 89  

##Request KEY

###localhost -> remote server  
Length： 81  

###remote server -> localhost  
Length: 105  