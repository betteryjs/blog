## 报错信息

```
psutil/_psutil_common.c:9:20: fatal error: Python.h: No such file or directory
     #include <Python.h>
                        ^
    compilation terminated.
    error: command 'gcc' failed with exit status 1
```

## 检查

- 检查`gcc`是否安装

```
sudo -y yum install gcc 
```

- 再检查`python3-devel` 或者`python2-devel`是否安装

## 解决方案

- 如果你使用的是`python2`

```
sudo yum install python2-devel
```

- 如果你使用的是`python3`

```
sudo yum install python3-devel
```