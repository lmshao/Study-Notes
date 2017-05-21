> http://blog.csdn.net/chenchong_219/article/details/37990541

# 1.码流总体结构
H.264分为两层：视频编码层**VCL**和网络提取层**NAL**。H.264的编码视频序列包括一系列的**NAL**单元，每个**NAL**单元包含一个**RBSP**。一个原始的H.264 NALU单元常由 **[StartCode]**+**[NALU Header]**+**[NALU Payload]** 三部分组成，其中 Start Code 用于标示这是一个NALU 单元的开始，必须是"00 00 00 01" 或"00 00 01"。   

NAL单元序列：   

StartCode | NALU Header | NALU Payload | StartCode | NALU Header | NALU Payload | ...
---|---|---|---|---|---|---

## NALU Payload
### SODB --> RBSP
视频编码后的压缩数据比特流片段成为 SODB，因为 SODB 长度可能不是字节对齐的，为了使数据都是8bit对齐的，所以可能需要在SODB后面添加RBSP尾部数据，这样就生成了 原始字节序列载荷（RBSP）数据。

RBSP 结构：   

SODB | RBSP尾 
---|---


### RBSP --> NALU Payload
 
NALU Payload 由 原始字节序列载荷（RBSP） 数据组成，因为 RBSP 数据的开始和结束可能与 NALU 起始码相同，为了避免冲突，需要对RSP字节流作如下处理：   
- 0x000000 ------> 0x00000300
- 0x000001 ------> 0x00000301
- 0x000002 ------> 0x00000302
- 0x000003 ------> 0x00000303

经过冲突避免后的RBSP可以直接作为 NALU载荷。

## NALU Header
NALU Header占用1字节，结构为：

forbidden_bit(1) | nal_ref_idc(2) | nal_unit_type(5) |  
---|---|---


- forbidden_bit：设为0
- nal_reference_bit：当前NAL的优先级，值越大，该NAL越重要。
- nal_unit_type ：NAL类型。参见下表：

### NAL 单元类型码   
Rec. ITU-T H.264 (02/2014)    

nal_unit_type | NAL类型
:---:|---
0 | 未指定
1 | 非 IDR 图像的编码片
2 | 编码片 数据分割块 A
3 | 编码片 数据分割块 B 
4 | 编码片 数据分割块 C
5 | IDR 图像编码片
6 | 辅助增强信息 SEI
7 | 序列参数集 SPS
8 | 图像参数集 PPS
9 | 访问单元分隔符
10 | 序列结尾
11 | 流结尾
12 | 填充数据
13 | 序列参数集扩展
14 | 前缀NALU
15 | 子集序列参数集 SSPS
16 | 深度参数及 DPS
17-18 | 保留
19 | 未分割的辅助编码图像的编码条带
20 | 编码条带扩展
21 | 深度视频组件编码条带扩展或3D-AVC纹理视图组件
20-23 | 保留
24-31 | 未指定

例如：
```
00 00 00 01 06 ... 00 00 00 01 67 ... 00 00 00 01 68... 00 00 00 01 65 ...
    SEI                 SPS                PPS               IDR Slice
00 00 00 01 61 ... 00 00 00 01 41 ...
非IDR 编码片        非IDR 编码片
```




