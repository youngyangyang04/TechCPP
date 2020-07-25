# OP

## CPU

```
    有几个cpu cpu num                       cat /proc/cpuinfo | grep "physical id" | sort | uniq
    一个cpu里有几个core cpu core num        cat /proc/cpuinfo | grep "cores" | uniq
    逻辑cpu num                             cat /proc/cpuinfo | grep "processor" | wc -l   or  top 然后按 1
    cpu info                                cat /proc/cpuinfo
```

## IO

```
    iostat -x -d 1
    iostat -x 1 3           就显示三条
    iostat -x 1 100         查看io读写状态,sda 为home盘，sdb为disk1，sdc为disk2
    iotop                   看谁在占用IO，tid 为线程id
    sudo iotop -P --only    看具体进程实际正在做io的
```

## Memory

```
    top
    free -g/ free -m
```
## free
![](./media/free-g.png)

* 第1行Mem数据：

total 内存总数: 189
used 已经使用的内存数: 188
free 空闲的内存数: 0
shared 当前已经废弃不用，总是0
buffers Buffer Cache内存数: 3
cached Page Cache内存数: 149

* 第2行-/+ buffers/cache：

-buffers/cache 的内存数：34 (等于第1行的 used - buffers - cached)
+buffers/cache 的内存数: 154 (等于第1行的 free + buffers + cached)
可见-buffers/cache反映的是被程序实实在在吃掉的内存，而+buffers/cache反映的是可以挪用的内存总数。
第三行数据是交换分区SWAP的，也就是我们通常所说的虚拟内存。

## top
* top 中的VIRT,RES,SHR

VIRT ：
1. 进程“需要的”虚拟内存大小，包括进程使用的库、代码、数据，以及malloc、new分配的堆空间和分配的栈空间等；
2. 假如进程新申请10MB的内存，但实际只使用了1MB，那么它会增长10MB，而不是实际的1MB使用量.

RES :
1. 进程当前使用的内存大小，包括使用中的malloc、new分配的堆空间和分配的栈空间，但不包括swap out量；
2. 包含其他进程的共享；
3. 关于库占用内存的情况，它只统计加载的库文件所占内存大小。
4. RES = CODE + DATA

SHR：
1. 除了自身进程的共享内存，也包括其他进程的共享内存；
2. 虽然进程只使用了几个共享库的函数，但它包含了整个共享库的大小；
3. 计算某个进程所占的物理内存大小公式：RES – SHR；

## OS

```
lsb_release -a                  系统版本，操作系统 和 版本
uname -a
uname -r                        内核版本
```

## Disk

```
du -sh filename                 看文件大小
df -H                           查看各个磁盘空间
lsblk -d -o name,rota           ROTA 1 for hard disks, 0 for ssd
du -h --max-depth=1             列出当前目录所有文件夹的大小
```

## Network

```
    ethtool xgbe0                   查看网卡信息，看网卡是百兆还是千兆，xgbe0是网卡的名字，可以通过ifconfig获取到
    curl ip:port                    判断当前ip和端口号是否在监听
    curl -vv                        可以看到发出和接受的报头信息等
    curl -v https                   访问https
    lsof -i:port                    列出在监听的端口号  list open files
    lsof(list open file) -p pid     列出指定进程打开的文件 （真的有用）
    netstat -tunlp | grep port      列出监听的端口号 netstat -tunlp | grep pid       可以看当前进程监听哪些端口
    netstat -nap | grep port        看那些端口被监听
    ping -c 1 www.baidu.com
    telnet www.test.com 8090        看这个域名加端口是否可以访问
    host -i IP                      根据ip 找域名
    netstat | grep 端口号           看哪个IP在访问这个端口号
```

## Linux

```
    tar -zxvf                       解压
    tar -zcvf  output.tar output/   压缩
    tar -cvf  output.tar output/    打包 不压缩
    tar -tvf test.tar.gz            预览压缩文件夹内容
    ldd                             查看一个 应用需要哪些依赖的动态库
    curl url -o obj                 下载该url的文件，类似wget
    curl -vk  https                 验证https
    vim --version | grep clipboard  看vim是否支持系统剪切板
    ls -lht                         看目录下文件大小以K/M/G 单位
    ll -tr                          看修改顺序
    /usr/libexec/java_home -V       java 路径
    nohup cmd &                     在后台运行cmd命令
    ssh -i id_rsa root@ip     使用私钥登录目标机器
    authorized_keys
    file                            查看文件信息
    strings                         查看bin文件下的字符串
    0 stdin，1 stdout，2 stderr
    2>&1                            将标准错误输出到标准输出中tai
    nohup myprogram > myprogram.out 2> myprogram.err &              将标准输出到特定的文件，err分开，后台起线程运行
    ctrl+A/ctrl+E                   定位到行首行未
    ctrl+U/ctrl+K                   删除到行首/行未
    ctrl+R                          查找历史命令
    ctags --list-languages          看ctags支持哪些语言
    find  ./  -name "*.xml"         递归查找一定要加双引号
    cal -3 / cal -y                 查看前一个月后一个月日历/显示全年的
    su - name                       切换到该用户，同时加载一些列环境配置，例如bash_profile
    sudo su                         切root账户
    rsync -av src/ 172.18.188.106:/Users/sunxiuyang/tmp/ 172.18.188.106为目标机器ip，copy src下的文件到目标机器tmp下
    rsync -av src 172.18.188.106:/Users/sunxiuyang/tmp/  把src这个目录copy过去
    for i in `cat gzns01_all`; do ssh -o StrictHostKeyChecking=no $i "cd /root && sh name_env_setup.sh"; done      root 已经是相互信任的
    ln -s jdk-8u161 jdk             软链
    ll | grep taf                   查看文件
    sort -k3 -n filename            按照（k3）第三个列 的数字(-n) 从小到大排序
    for i in `cat ip.list`;do host $i;done > tmp    按行读取ip.list文件, 并执行 host操作
    for i in `cat gzns01_all`; do scp -o no StrictHostKeyChecking `pwd`/home_env_setup.sh $i:/root/; done
    for i in `cat gzns01_all`; do ssh -o StrictHostKeyChecking=no $i "cd /root && sh home_env_setup.sh"; done
    dig www.baidu.com               dig命令可以执行查询域名相关的任务
    crontab
    rm node.log.* node.log.wf.* -f &    起一个进程删掉
    pstack pid                      打印出pid进程下所有的线程栈信息
    jstack -l pid                   打印java进程的堆栈信息
    for i in `echo -e "name1\n name2\n name3"`; do echo $i" "$RANDOM; done > ./tmp; cat ./tmp | sort -nk2        随机排序名字
    cat /proc/version
    cat /etc/issue
    ll /proc/340/fg | grep socket | wc -l       查看fd数量
    uptime                          看机器启动时间
    /etc/security/limits.conf       把core文件打开
    ulimit -c                       看core文件是否打开
    ulimit -c unlimited             不设置core文件大小
    /var/log/messages               看系统日志
    ls -l /proc/15430/fd/ | wc -l   查看这个进程打开的文件描述符的个数
    cat /proc/sys/fs/file-max       查看系统可打开的最大描述符
    lsof -p 24405                   看这个进程打开的fd
    netstat -antp | grep 24405      看该进程的链接的情况
    /var/log/message                系统启动后的信息和错误日志，是Red Hat Linux中最常用的日志之一
    sysctl -a | grep keepalive      看系统内核是不是那tcp得探活关了
    top -Hp 32554                   查看32554进程的线程情况
    lsblk -d -o name,rota           查看磁盘是否是ssd 或者 HDD， 如果ROTA：0 就是ssd
    curl http://test.com:8302/metrics -o tmp 把这个url的内容输出到文本里
    export TMOUT=0                  不超时

    asan/pmap                       看内存泄漏
    sed                             正则，各种替换
    fdisk -l                        切换root 账号 看机器链接的磁盘数量
    ls /dev                         看机器设备，看有多少块盘
    useradd name                   机器添加 name 用户
    passwd name                    给name 用户添加密码
    cat /dev/null > fe.log          清空文件
    awk -v RS='' -v ORS='\n\n' '/搜索的词/' 文件名字     搜出关键词所在的段落
```

### user_manager

```
    useradd testuser                创建用户testuser
    passwd testuser                 给testuser设置密码
    userdel testuser                删除该用户
```

## git

```
    git reset HEAD                  如果add了的话，全都取消
    git checkout filename           恢复最新版本
    git commit --amend              改变提交的commit message 或者 对同一个提交进行代码上的修改
    git log -p -2                   最近两次的修改详细记录

    git reset test.cpp              如果add了test.cpp，要取消add
    git log                         查看提交文件的 logid
    git log -p  filename            查看该文件的提交历史， 可以通过关键字
    git reset --hard ${logid}                       回滚该logid的提交（已经commit，没有push）f you don't care about keeping the changes you made
    git reset --soft ${logid}                       use --soft if you want to keep your changes
    git diff --stat --cached origin/master          看commit但没有push的文件
    git log --graph                                 图形化显示
    git branch -d the_local_branch                  删除对应分支


    git brach tmp                                   创建一个branch分支，把当天提交记录都保存起来
    git co 当前branch
    git lg tmp                                      查看tmp这个分支的日志
    git cherry-pick  commitid                       把tmp上某个分支的commit合并到本分支后面
    git cm --amend                                  把change id 改了，要不把changeid也考到这个分支上，改分支提交合入的时候就会出现问题
    git merge feature-show-create-table-partition   当前分支是feature-show-create-table-partition-info，merge一下feature-show-create-table-partition ，响应的提交也会 merge过来
    git merge feature-show-create-table-partition-info --no-ff

    git co develop
    git branch
    git diff develop master
    git pull --rebase
    git branch feature-split-blacklist
    git add fe/src
    git rebase --abort
    git cm
    git branch feature origin/feature               把在本地新建一个feature分支并把远端的分支feature同步下来

    // 分支拉的久远了，和develop上差距比较大，先把把本地备份到 tmp分支
     git rebase develop                             rebase 本地develop的分支，（我当前的分支是tmp）·

     git format-patch -1                            生成对应的patch文件
     git am 0001-Add-delete-range-http-and-rpc-interface.patch

     git branch -d dev                              删除本地分支
     git branch -a                                  显示所有分支
     git push origin --delete dev                   删除远端分支

     git show ce8c290d23ebaf5e1348ff74df5c61a0d8185856  看这个commitid属于哪个分支
     git branch -a --contains 5c64d8be4950b0adc9352de848b1edb915c4ccd4  看远端和本地是否有这个分支


     git clone http://github.com/large-repository --depth 1
     cd large-repository
     git fetch --unshallow
     git fetch是将远程主机的最新内容拉到本地，用户在检查了以后决定是否合并到工作本机分支中。
     git reset --hard origin/hotfix-leader-balance
     git stash
     git stash save "save message"                  执行存储时，添加备注，方便查找，只有git stash 也要可以的，但查找时不方便识别
     git stash pop                                  恢复
     git reset --hard origin/master                 恢复到和远端一致
     git show  commit_id  可以看到每个文件具体的改动内容

```

## Mysql

```
select count(*) from table_name         table记录数量
select * from meta_tablet_1 limit 1;    取一条看一下
SELECT COUNT(*) FROM information_schema.tables WHERE table_schema = 'db_name';      看该库有多少张表
SHOW CREATE TABLE tablename             看创建table的语句
```
## Gdb

```
    gdb lib/name_be ~/core.24563
    bt(backtrace)                 当前堆栈信息
    f(frame)                        n是一个从0开始的整数，是栈中的层编号。比如：frame 0，表示栈顶，frame 1，表示栈的第二层。
```


##  dot

```
dot -Tpng test.dot > output.png
dot -Tsvg test.dot > output.svg
```

## webserver
* nohup python -m SimpleHTTPServer 8000 &  使用python可以快速搭建一个web服务

# Software shortcuts

## Tmux

```
    ctrl + b
    ,                         重命名当前窗口,这样便于识别
    .                         修改当前窗口编号,相当于窗口重新排序
    "                         将当前面板平分为上下两块
    %                         将当前面板平分为左右两块
    x                         关闭当前面板
    数字键                    切换至指定窗口
    &                         关闭当前窗口
    c                         创建新窗口
    w                         通过窗口列表切换窗口
    方向键                   移动光标以选择面板
    [                        "["，此时进入所谓的copy-mode
    set -g terminal-overrides              For tmux version 2.1 and up scroll up , modify on .tmux.conf
    set-option -g mouse on          scroll up
```

## Taglist

```
    u                           更新taglist窗口中的tag
    x                           taglist窗口放大和缩小，方便查看较长的tag
```

## Chrome

```
    ⌘ + t                       Open a new tab, and jump to it
    ⌘ + 9                       Jump to the last tab
    ⌘ + Option + Right arrow    Jump to the next open tab/ Left arrow for previous open tab
    ⌘ + w                       Closes the current tab or pop-up
    Control + Command + F       Full screen
```

# Java compile

```
    javac -cp ".:./third-party/*:./lib/*" Sample.java       complie with jar
    java -cp ".:./third-party/*:./lib/*" Sample             run
```

# Maven

```
    ~/.m2/settings.xml      This is a reference for the user-specific configuration for Maven.
    mvn install             download plugin maven need
    mvn package             compile
    ~/.m2/                  When maven build is executed, Maven automatically downloads all the dependency jars into the local repository.
    mvn package -Dmaven.test.skip=true      skip simple test
    mvn package -Dmaven.javadoc.skip=true   skip doc generator
```

# Ack

```

ack -w wordname         //  Force PATTERN to match only whole words

```
# crontab

```
    crontab –e          // open crontab jobs          0 18 * * * sh /home/name/test/test-feature/replica_hot.sh  这里例子就是每天18点执行这个shell
    crontab –l          // list existing cron jobs

```

# size

## mysql
5.0版本以上 varchar(20)，指的是20字符
bigint  8个字节


# 排除问题的思路

* 查看机器 内存和CPU
* 在看日志

