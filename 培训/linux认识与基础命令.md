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
- 查看制造商
- 查看cpu
- 查看内存
- 网线链接
- 全双工还是半双工、传输速率
- 网卡驱动版本
- 分区情况
- pci设备
- usb设备
  
## 查看系统
- 当前目录
- 当前时间
- 格式化时间输出
- 发行版
- 查看系统环境变量

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

### grep

##  其他
- basename 返回文件名称
- dirname 返回路径字符串的上层目录路径
