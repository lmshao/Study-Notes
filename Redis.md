# Redis

## 哈希 Hash
CMD | note
:--- | :---
HMSET key field value [field value] | 同时存多个键值对到key中
HMGET key filed [filed] | 查看特定字段值
HGETALL key | 查看key中键值对
HDEL key field1 [field2] | 删除某个键值对
HEXISTS key field | 查看指定字段是否存在
HGET key field | 获取key中指定字段
HINCRBY key field num | 给指定字段的整数值加上增量，+=num
HKEYS key | 获取所有字段名
KLEN key | 获取所有字段数量
HSET key filed value | 将哈希表中字段设为value
HVALS key | 获取所有值，不包括字段名


## 列表 List
类似stack

CMD | note
:--- | :---
LPUSH key value1 value2 | 压入元素到列表头部
LPOP key | 弹出列表头部元素
RPUSH key value3 value4 | 列表尾部插入元素
RPOP key | 列表尾部弹出元素
LRANGE key 0 9  | 查询0-9号元素
LLEN key | 返回列表长度
LINDEX key index | 返回索引号对应的元素(索引号0-)
LSET key index value | 修改索引号对应的元素
LPUSHX key value | 列表头部插入一个元素
RPUSHX key value | 列表尾部插入一个元素

## 集合 Set

CMD | note
:--- | :---
SADD key mem1 mem2 | 添加成员
SMEMBERS key   | 返回成员
SCARD key | 返回成员数
SPOP key | 随机返回并移除一个成员
SREM key mem1 mem2 | 移除指定成员


