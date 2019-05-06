centos7自带python2，由于执行yum需要python2，所以即使安装了python3也不能删除python2
1.安装依赖包
yum -y groupinstall "Development tools"


yum -y install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel

2.下载自己需要的python版本，例如python3.7.1,下载要花费一段时间，要耐心等待
wget https://www.python.org/ftp/python/3.7.1/Python-3.7.1rc1.tar.xz

3.新建一个文件夹存放python3
mkdir /usr/local/python3 

4.把安装包移动到该新建文件夹下，解压安装包，安装python3,依次执行以下命令，花费时间较长，耐心等待
mv Python-3.7.1rc1.tar.xz /usr/local/python3
tar -xvJf  Python-3.7.1rc1.tar.xz
cd Python-3.7.1rc1
./configure --prefix=/usr/local/python3
make  
make install

若出现错误：ModuleNotFoundError: No module named '_ctypes' make: *** [install] Error 1

3.7版本需要一个新的包libffi-devel，安装此包之后再次进行编译安装即可。

yum install libffi-devel -y
make install
若在安装前移除了/usr/bin下python的文件链接依赖，此时yum无法正常使用，需要自己下载相关软件包安装，为节省读者时间，放上链接

wget http://mirror.centos.org/centos/7/os/x86_64/Packages/libffi-devel-3.0.13-18.el7.x86_64.rpm
rpm -ivh libffi-devel-3.0.13-18.el7.x86_64.rpm
安装完成后重新进行make install，结束后再次配置相关文件的软连接即可。
 


5.创建软连接
ln -s /usr/local/python3/bin/python3 /usr/bin/python3
ln -s /usr/local/python3/bin/pip3 /usr/bin/pip3
这里要注意，否则会造成无法调用(如PHP调用python脚本需要用到绝对路径)

其中公司用的软连接：/usr/bin/python3 -V、/usr/local/python3/bin/python3 -V

个人用的软连接：/usr/bin/python3 -V、/usr/local/python3/bin/python3 -V、/usr/local/bin/python3 -V
6.此时python3已经装好，在命令行中输入python3测试


7.修改yum配置文件，python2与python3共存
vi /usr/bin/yum

把#! /usr/bin/python修改为#! /usr/bin/python2（配置文件第一行）
同理
vi /usr/libexec/urlgrabber-ext-down

把文件里面的#! /usr/bin/python 也修改为#! /usr/bin/python2
此时完成python3安装，且实现与python2共存,保持yum命令可用
--------------------- 
作者：滑冰选手斯蒂芬 
来源：CSDN 
原文：https://blog.csdn.net/weixin_40096730/article/details/83029915 
版权声明：本文为博主原创文章，转载请附上博文链接！
