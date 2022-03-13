# Linux命令总结

本文总结Linux的基本概念和常用的命令

## 基本概念

计算机硬件是由运算器，控制器，存储器，和输出/输出设备共同组成，而让各种硬件各司其职且能协同运行的就是系统内核。Linux的系统内核负责完成对硬件资源的分配，调度管理任务。而对于我们Linux用户而言，我们Linux提供的基于系统调用借口开发的程序或服务来管理计算机。Shell就是其中的一个命令行工具，它采用Bash(Bourne-Again SHell)解释器，可以将用户的命令翻译为内核可以理解的方式。



Linux的基本命令格式由命令名称，参数，和对象组成：

```shell
命令名称 [命令参数] [命令对象]
```

- 命令对象指要处理的文件，目录，用户等资源
- 命令参数是执行命令的一些配置项，通常有长格式(--加上完整的选项名称)和短格式(-加单个字母)两种写法



## 常用系统工作命令

| 命令       | 说明                                                         |
| ---------- | ------------------------------------------------------------ |
| `man`      | 用于查看命令的详细描述信息，示例: `man echo`                 |
| `echo`     | 用于在终端输出字符串或变量提取后的值，格式：`echo [字符串|$变量]`示例：`echo Hello andre!`, `echo $SHELL` |
| `date`     | 用于显示及设置系统的时间和日期，格式为 `date [选项] [+指定的格式]` |
| `reboot`   | 重启系统                                                     |
| `poweroff` | 关机                                                         |
| `who`      | 用于查看当前所有登入主机的用户信息                           |
| `whoami`   | 显示系统当前用户名                                           |
| `ps -aux`  | ps命令用于查看系统中的进程状态，格式为：`ps [参数]`， aux是参数，详细解释见后文 |
| `top`      | top命令用于动态地监视进程活动与系统负载等信息，相当于linux下的任务管理器 |
| `wget`     | 用于在终端中下载网络文件，格式为：`wget [参数] 下载地址`     |
| `pidof`    | 用于查询某个指定服务的pid号，格式：`pidof [参数] [名称]`     |
| `kill`     | 用于终止某个指定pid的服务进程，格式：`kill [参数] [进程名称]` |
| `killall`  | 用于终止某个指定名称的服务所对应的全部进程，格式：`kill [参数] [进程]` |

## 常用系统状态检测命令

| 命令       | 说明                                                         |
| ---------- | ------------------------------------------------------------ |
| `ifconfig` | 该命令用于获取网卡配置与网络状态等信息，格式为：`ifconfig [网络设备] [参数]` |
| `uname -a` | 查看系统内和与系统版本等信息                                 |
| `uptime`   | uptime用于查看系统的负载信息，包括系统时间，系统已运行时间，启用终端数量，和平均负载值等信息 |
| `free -h`  | free命令用于显示当前系统的内存使用量等信息                   |
| `last`     | last命令用于查看所有系统的登记记录                           |
| `history`  | history命令用于显示历史执行过的命令.`history -c`, -c代表清空所有命令历史记录 |

## 常用文本编辑命令

| 命令   | 说明                                                         |
| ------ | ------------------------------------------------------------ |
| `cat`  | cat命令用于查看内容较少的纯文本文件(.txt/.html/.md文档)，格式为：`cat [选项] [文件]`，文件显示同时带上行号：`cat -h [文件]` |
| `more` | more命令用于查看内容较多的纯文本文件，格式：`more [选项] [文件]` |
| `head` | head命令用于查看纯文本文档的前N行，格式：`head [选项] [文件]` |
| `tail` | tail命令用于查看纯文本文档的后N行或持续刷新内容，如查看循环刷新的日志文件：`tail -f /var/log` |
| `diff` | diff命令 用于比较多个文本文件的差异，如显示两个文件内容的具体不同之处：`diff -c a.txt b.txt` |

## 常用文件目录管理命令

| 命令    | 说明                                                         |
| ------- | ------------------------------------------------------------ |
| `touch` | 用于创建空白文件或设置文件的时间，示例1: `touch andre.txt`, 示例2: `touch -d "2017-01-01 09:00" andre.txt` |
| `mkdir` | 用于创建空白的目录，示例: `mkdir -p andre/a/b`, -p代表递归创建有嵌套关系的文件目录 |
| `cp`    | 用于复制文件或目录，格式: `cp [选项] 源文件 目标文件`        |
| `mv`    | 用于剪切或者将文件重命名，格式: `mv [选项] [目标路径|目标文件名]` |
| `rm`    | 用于删除和文件或目录，删库跑路示例: `rm -rf *`               |
| `file`  | 用于查看文件的类型，格式: `file [文件名]`                    |

## 常用文件压缩/搜索命令

| 命令   | 说明                                                         |
| ------ | ------------------------------------------------------------ |
| `tar`  | 对文件进行打包压缩或解压。格式: `tar [选项] [文件]` 参数-c用于创建压缩文件，-x用于解压文件 |
| `grep` | 用于在文本中执行关键词搜索并显示匹配的结果。格式: `grep [选项] [文件]` |
| `find` | 用于按照指定的条件查找文件，格式为: `find [路径] 查找条件 操作` 。示例: ` find ~/Desktop -name "self-driving" -print` 找到Desktop文件夹下有关"self-driving"的文件并打印。 |

## 实用命令分析

### ps命令

Linux中的ps命令是Process Status的缩写。ps命令用来列出系统中当前运行的那些进程。**ps命令列出的是当前那些进程的快照**，就是执行ps命令的那个时刻的那些进程，如果想要动态的显示进程信息，就可以使用top命令。

常用参数：

- `-a`: 显示所有进程
- `-u`: 显示特定用户的进程
- `-x`: 显示没有控制终端的进程

**显示所有进程信息**

```shell
andre@andre-CN15S:~$ ps -A
  PID TTY          TIME CMD
    1 ?        00:00:36 systemd
    2 ?        00:00:00 kthreadd
    4 ?        00:00:00 kworker/0:0H
    6 ?        00:00:00 mm_percpu_wq
    7 ?        00:00:00 ksoftirqd/0
    8 ?        00:00:08 rcu_sched
```

**列出目前所有的正在内存中的程序**

```shell
andre@andre-CN15S:~$ ps aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.0 226188  9800 ?        Ss   10:49   0:37 /sbin/init splash
root         2  0.0  0.0      0     0 ?        S    10:49   0:00 [kthreadd]
root         4  0.0  0.0      0     0 ?        I<   10:49   0:00 [kworker/0:0H]
root         6  0.0  0.0      0     0 ?        I<   10:49   0:00 [mm_percpu_wq]
root         7  0.0  0.0      0     0 ?        S    10:49   0:00 [ksoftirqd/0]
root         8  0.0  0.0      0     0 ?        I    10:49   0:08 [rcu_sched]
root         9  0.0  0.0      0     0 ?        I    10:49   0:00 [rcu_bh]
root        10  0.0  0.0      0     0 ?        S    10:49   0:00 [migration/0]
root        11  0.0  0.0      0     0 ?        S    10:49   0:00 [watchdog/0]
root        12  0.0  0.0      0     0 ?        S    10:49   0:00 [cpuhp/0]
root        13  0.0  0.0      0     0 ?        S    10:49   0:00 [cpuhp/1]
root        14  0.0  0.0      0     0 ?        S    10:49   0:00 [watchdog/1]
root        15  0.0  0.0      0     0 ?        S    10:49   0:00 [migration/1]
root        16  0.0  0.0      0     0 ?        S    10:49   0:00 [ksoftirqd/1]
root        18  0.0  0.0      0     0 ?        I<   10:49   0:00 [kworker/1:0H]
```

**ps 与grep 组合使用，查找特定进程**

```shell
andre@andre-CN15S:~$ ps -ef|grep tencent
andre    24861 17712  0 21:41 pts/2    00:00:00 grep --color=auto tencent
```

注：

linux上进程有5种状态:

- 运行(正在运行或在运行队列中等待)
- 中断(休眠中, 受阻, 在等待某个条件的形成或接受到信号)
- 不可中断(收到信号不唤醒和不可运行, 进程必须等待直到有中断发生)
- 僵死(进程已终止, 但进程描述符存在, 直到父进程调用wait4()系统调用后释放)
- 停止(进程收到SIGSTOP, SIGTSTP, SIGTTIN, SIGTTOU信号后停止运行运行)

ps工具标识进程的几种状态码:

- D 不可中断 uninterruptible sleep (usually IO)
- R 运行 runnable (on run queue)
- S 中断 sleeping
- T 停止 traced or stopped
- Z 僵死 a defunct (”zombie”) process
- <: 高优先顺序的进程

### ifconfig

Linux查看本机IP有两种方法，一种方法是使用废弃的ifconfig，第二种方法是使用内置的ip。目前在ubuntu18.04中ifconfig已被废弃，其对应的net-tools也不再被维护，想要使用ifconfig需要手动安装。

```shell
# 采用ifconfig查看本机IP 
sudo apt-get install net-tools
ifconfig

# 采用内置的ip命令查看
ip a
```



### 磁盘管理

示硬盘及所属分区情况:

```shell
sudo fdisk -l
```

显示硬盘挂载情况：

```shell
df -l
```





## 参考资料

关于Linux的资源

1. 一个很全面的webbook：https://linuxtools-rst.readthedocs.io/zh_CN/latest/index.html
2. 《Linux就该这么学》
3. linux command line cheat sheet



