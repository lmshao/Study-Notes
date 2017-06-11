# 常用Shell脚本

## 1. 使用MD5重命名文件

```sh
#!/bin/bash
# Rename .jpg file using md5
for file in `ls *.jpg`
do
  name=`md5sum $file | awk '{print $1".jpg"}'`
  if [ "$file" != "$name" ]
  then
    mv -f $file $name
  fi
done
```
处理带空格的文件名，改进版

```sh
#!/bin/bash
# Rename .jpg file using md5
ls *.mp3 | while read file
do
  name=`md5sum "$file" | awk '{print $1".mp3"}'`
  if [ "$file" != "$name" ]
  then
    mv -f "$file" $name
  fi
done
```

## 2. 