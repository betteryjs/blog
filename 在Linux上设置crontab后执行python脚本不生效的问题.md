# 在Linux上设置crontab后执行python脚本不生效的问题

 [2022-03-02 ](https://blog.11451400.xyz/2022/03/02/在Linux上设置crontab后执行python脚本不生效的问题/) [杂项](https://blog.11451400.xyz/tags/杂项/) [评论](https://blog.11451400.xyz/2022/03/02/在Linux上设置crontab后执行python脚本不生效的问题/#comments) 字数统计: 608(字) 阅读时长: 2(分)

目前有一个需求是定时执行某个 `python` 脚本，但是在 `Linux `上设置 `crontab `后，不生效？手动执行生效？于是使用下面的方法执行即可：

大体思路为先写一个 `shell` 脚本，脚本中执行 `python` 文件，然后定时执行 `shell` 脚本即可。具体原因是

`crontab `使用的`PATH` 跟`python`使用的不在一条道上面 只能改道行

## 使用如下命令创建脚本：

```
vim test.sh
```

## xxxxxxxxxx class MinStack {private:    stack<int> x_stack;    stack<int> minStack;public:    MinStack() {        minStack.push(INT_MAX);​    }    void push(int x) {        x_stack.push(x);        minStack.push(min(minStack.top(), x));    }    void pop() {        x_stack.pop();        minStack.pop();    }    int top() {        return x_stack.top();    }    int getMin() {        return minStack.top();    }};cpp

```
#!/usr/bin/bash
cd /home/test/  # 写你自己py文件的文件夹
/usr/bin/python3 test.py
```

## 在`test.py`文件的头部加入

```
#!/usr/bin/python
# -*- coding: UTF-8 -*-
```

## 给`test.py`和`test.sh`授予执行权限

```
chmod a+x test.py
chmod a+x test.sh
```

## 然后使用如下命令，编辑定时任务：

```
crontab -e
```

## 假如设定每天 8 点执行脚本，设置如下：

```
0 8 * * * /home/test/test.sh
```

## 保存定时任务，几分钟后自动生效。

> **注意**：所有的路径都使用**绝对路径**，否则仍然无效。

## `crontab`命令

我们用**crontab -e**进入当前用户的工作表编辑，是常见的vim界面。每行是一条命令。

crontab的命令构成为 时间+动作，其时间有**分、时、日、月、周**五种，操作符有

- ***** 取值范围内的所有数字
- **/** 每过多少个数字
- **-** 从X到Z
- **，**散列数字

## 实例

### 实例1：每1分钟执行一次`myCommand`

```
* * * * * myCommand
```

### 实例2：每小时的第`3`和第`15`分钟执行

```
3,15 * * * * myCommand
```

### 实例3：在上午`8`点到`11`点的第`3`和第`15`分钟执行

```
3,15 8-11 * * * myCommand
```

### 实例4：每隔两天的上午`8`点到`11`点的第`3`和第`15`分钟执行

```
3,15 8-11 */2  *  * myCommand
```

### 实例5：每周一上午`8`点到`11`点的第`3`和第`15`分钟执行

```
3,15 8-11 * * 1 myCommand
```

### 实例6：每晚的`21:30`重启`smb`

```
30 21 * * * /etc/init.d/smb restart
```

### 实例7：每月`1`、`10`、`22`日的`4 : 45`重启`smb`

```
45 4 1,10,22 * * /etc/init.d/smb restart
```

### 实例8：每周六、周日的`1 : 10`重启`smb`

```
10 1 * * 6,0 /etc/init.d/smb restart
```

### 实例9：每天`18 : 00`至`23 : 00`之间每隔`30`分钟重启`smb`

```
0,30 18-23 * * * /etc/init.d/smb restart
```

### 实例10：每星期六的晚上`11 : 00 pm`重启`smb`

```
0 23 * * 6 /etc/init.d/smb restart
```

### 实例11：每一小时重启`smb`

```
* */1 * * * /etc/init.d/smb restart
```

### 实例12：晚上`11`点到早上`7`点之间，每隔一小时重启`smb`

```
* 23-7/1 * * * /etc/init.d/smb restart
```