# linux分类

## debian
- debian 适合系统管理员和高级用户
- ubuntu debian衍生版，使用apt软件管理工具安装和更新软件，适合入门
  
## redhat
- redhat 面向商业市场的linux发行版。使用yum程序包管理器，安全性比较好，缺点是太多旧程序包，支持成本很高
- centos 使用yum管理软件包，可以在桌面端测试服务器的运作原理
- fedora dnf管理软件包

## 其他
- Arch linux pacman管理软件包
- opensuse yast管理软件包

# 关键软件包

## apt
Advanced Package Tool
- 提供模糊查询  `sudo apt-cache search xxx` 查询关键字或者简介包含xxx的包
- `dpkg -l` 显示本机所有安装的软件包， `dpkg -l | grep xxx` 筛选含有xxx关键字的软件包
- `apt-get install` 安装
- `apt-get remove` 卸载，仅仅删除软件包本身
- `apt-get upgrade` 更新
- `apt-get purge` 处理删除软件包，还会删除相应的配置文件
- `apt-get autoremove` 删除多余的包
- `apt-get check` 检查错误依赖
  
## yum
- `yum list` 查询所有已安装和可安装的软件包
- `yum list 包名`查询执行软件包的安装情况
- `yum search 关键字`从 yum 源服务器上查找与关键字相关的所有软件包
- `yum info 包名`查询执行软件包的详细信息
- `yum -y install 包名`
- `yum -y update 包名`升级特定的软件包
- `yum remove 包名`

# 命令

## 查看硬件
- 查看制造商  `dmidecode`
- 查看cpu `cat /proc/cpuinfo`
- 查看内存 `cat /proc/meminfo` 或者`free -m`
- 网线链接 `mii-tool`
- 全双工还是半双工、传输速率  `ethtool eth0`
- 网卡驱动版本 `ethtool -i eth0`
- 分区情况 `fdisk -l`
- pci设备 `lspci`
- usb设备 `lsusb`
  
## 查看系统
- 当前目录 `pwd`
- 当前时间 `date`
- 格式化时间输出 `date "+%Y-%m-%d %H:%M:%S"`
- 发行版 `cat /etc/issue`
- 查看系统环境变量 `env`
- 修改系统环境变量  `export 某一项=xxx`
- 内核版本  `uname -r`
- 查看系统服务情况  `chkconfig --list`
- 设置服务开机启动or关闭 `chkconfig -level 等级号 服务名 on/off`
- 通用的开机启动 `vim etc/rc.local`
- 查看运行级别 `run level` 或者 `grep default /etc/inittab`
- 查看网卡ip `ifconfig`
- 查看某个网卡ip `ifconfig  网卡`

## 查看目录
- 改变modify和change `touch filename`
- 查看当前目录大小 `du -sh`
- 查看指定目录深度的目录大小 `du -h --max-depth= num`
- 查看分区容量大小 `df -h`
- 统计目录和文件个数 `ls -l |wc -l`

## 操作目录
- 递归创建目录 `mkdir -p path`
- 复制目录 `cp dir1 dir2`
- 递归复制 `cp -R dir1 dir2`
- 保留原目录的属性、权限 `cp -a dir1 dir2`
 
## 文件
- 创建文件 `vim filename` 或者 `touch filename`
- 从头开始显示文件所有内容 `cat filename`
- 从后面开始显示文件所有 `tac filename`
- 逐屏查看 `more filename`
- 显示开头10行 `head filename`
- 指定行数量 `head -n num filename`
- 显示末尾10 ` tail filename`
- 指定行数量 `tail -n num filename`
- 持续监视文件输出 `tail -f filename` 
- 查看文件状态 `stat filename`
- 查看文件中是否包含keyword `grep keyword filename`
- 查看当前目录及其子目录哪个文件包含keyword `grep -R keyword *.`
- 移动文件 `mv filename path`
- 重命名文件 `mv filename newfilename`
- 删除文件 `rm -f filename`
- 删除目录 `rm -rf `

## vim
- q退出编辑
- q！强制退出
- w 保存
- wq 保存退出
- x 保存退出
  


## tar

### 压缩
直接在打包目录的上一级目录进行打包，不支持加绝对路径进行打包
例如你要打包/data/web/下的www目录`cd /data/web`
`tar czvf www.tar www`
而 `tar czvf www.tar /data/web/www`解压后会带上全路径

- `tar cf file.tar file` 低压缩率，速度快
- `tar czf file.tar.gz` 压缩率与速度兼顾
- `tar cjf file.tar.bz2 file` 压缩率高，速度慢
- `tar file.tar file --exclude="*.log"` 排除特定后缀文件或目录

### 解压
解压到当前目录，如果压缩指定目录，-C path
- `tar xf file.tar.gz` tar1.23以上版本自动识别压缩格式
- 低版本则需要指定压缩格式
    - >`tar xf file.tar`
    - >`tar xzf file.tar.gz`
    - >`tar xjf file.tar.bz2`
- 不解压缩，查看压缩文件里包含的文件和目录`tar tf file.tar |more`

## find
- 查找目录包括文件  `find /path -name "keyword"`
- 查找文件 `find /path -name "keyword" -type f`
- 查找60天前修改的文件 `find /path -type f -mtime +60`

## 文件与目录权限
- 共9位，每3位一组，共3组
- 各组依次代表文件所有者、同组用户和其他用户对该文件的权限
- 每一组都是rwx三个符号与"-"符号的组合
  - r 读
  - w 写
  - x 执行
  - "-" 禁止

##  权限掩码umask
用来指定目前用户在新建文件或者目录时候的权限默认值。

- 新建文件 666 - umask，新建文件，如果对应位上为偶数那么最终权限就是这个值，如果为奇数，需要+1
- 新建目录 777 - umask，

### 查看权限掩码命令
- umask 数字形态的权限掩码
- umask -S 符号类型的方式

### 修改权限掩码
- 临时修改默认权限，`umask xxxx`
- 永久修改默认权限，编辑文件。/etc/bashrc （在当前shell环境中生效） 和 /etc/profile (在整个系统中生效)
- 修改完之后，需要重新读取一下 `source /etc/profile` `source /etc/bashrc`
- uid >= 199 的表示普通用户
- uid < 199 表示root

### 更改权限
- chown 改变文件所有权 `chmod [-options] u/g/o/a +/-/= r/w/x [filelist]`
  - u user,文件或目录的拥有者
  - g group 文件或目录的所属群组
  - o other 除了文件或目录拥有者或所属群组之外的其他用户
  - a all 全部用户
  - “+” 加入权限
  - “-” 去掉权限
  - “=” 设定权限
- chgrp 改变用户分组
- chmod 改变文件属性

## 文件操作

### cat
#### 查看文件
- cat -n 查看文件时可以显示行号
- cat file |more 会把文件一部分输出，然后按回车查看下一行，空格查看下一页，按q停止查看

#### 文件合并 
- `cat a.txt > b.txt` 或 `cat a.txt >> b.txt`
- `cat a.txt b.txt > c.txt` a，b文件合并后覆盖到c中
  -  “>” 覆盖方式写入
  -  “>>” 以追加方式写入

#### 创建文件
- cat > file 使用后，linux会让我们添加内容，当添加完内容后，回车另起一行，按ctrl+d结束或者不按回车，按两次ctrl+d
- cat > file << xxx 添加内容，以输入xxx为结束

## grep
命令格式 `grep [option] keyword file`
- -a 不要忽略二进制数据
- -i 忽略大小写

## 重定向信道
- 输入重定向 `cat < file`
- 输出重定向 `cat file > newfile`
- 错误输出重定向 `cat file 2> newfile`
- 输出和错误输出都重定向一个文件 `cat file >newfile 2>&1`
  
## 进程管理
- 查看是否存在某个进程 `ps aux |grep keyword`
- 杀死进程 `pkill keyword` `killall keyword`
- 查看进程号 `pidof keyword`

## Rpm
### 安装
- 安装 `rpm -ivh filename`
- 强行安装 `rpm -ivh --nodeps filename`
- 升级包 `rpm -Uvh filename`
- 卸载 `rpm -e filename`
- 忽略包依赖卸载 `rpm -e --nodeps filename`
### 查询
- 查看是否安装某个包 `rpm -qa |grep -i filename`
- 查看已安装的rpm包安装文件列表 `rpm -ql filename`
- 查看未安装的rpm包的含文件列表 `rpm -qpl filename`
- 查看某个文件由哪个包提供 `rpm -qf filename`

## yum
- 安装`yum -y install filename`
- 卸载`yum remove filename`
- 查看哪个包提供某个文件`yum provides filename`

## 网络
### 远程链接
- ssh登录 ``
- 指定端口登录
- 指定用户名
- 指定认证key文件
- 取消host检查
- 远程执行命令 
- 详细显示连接过程
### scp拷贝
- 指定端口
- 指定认证key文件
- scp目录
- scp限速
- 取消host检查
  
## 网卡相关
- 禁用网卡 `ifdown eth1`
- 开启网卡 `ifup eth1`
- 重启网络，使配置生效 `service network restart`

## 系统性能监控
- top工具  实时显示系统中各个进程的资源占用状况
- vmstat工具
  - 每三秒汇总一次，连续报告5次  `vmstat 3 5`
- iostat工具 
  主要是磁盘IO性能监视
  - 每三秒汇总一次，连续报告5次  `iostat -d -k 3 5`
- dstat 输入dstat进行查看
  - 怀疑cpu存在瓶颈 `sar -u` `sar -q`
  - 怀疑内存存在瓶颈 `sar -B` `sar -r` `sar -W`
  - 怀疑i/o存在瓶颈 `sar -b` `sar -u` `sar -d`
  - 查看历史记录 `sar -f filename`

## 网络监控
### vnstat
- 网卡流量 `vnstat -l`
- -i指定网卡 `vnstat -l -i eth0`

### netstat
- 查看路由表 `netstat -nr`
- 查看tcp监听端口`netstat -tlnp`
- 查看udp监听端口`netstat -ulnp`
- 查看所有链接 `netstat -an`

### ping
- 查看域名解析 `ping domain`
- 指定ping次数 `ping -c num domain`
- 指定ping的出口 `ping -l ip domain`
- 指定发包间隔 `ping -i num domain`

### 其他网络命令
- 指定dns服务器 `dig dns服务器 domain`
- 路由跟踪 `traceroute domain`
- ping+tracert ： mtr  `mtr domain`
- nslookup  查看域名解析是否正常，`nslookup url [dns-server]`
- host 分析域名查询工具，测试域名系统工作是否正常 `host domain`
##  其他
- basename 返回文件名称
- dirname 返回路径字符串的上层目录路径
