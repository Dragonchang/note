CTS：
https://source.android.google.cn/compatibility/cts/downloads?hl=zh-cn   

翻墙：   
https://xiapac.com/305167995/8114187.pac   
设置-网络    
   自动   
   使用chrome   
在线dump汇编：   
   https://onlinedisassembler.com/odaweb/  
   
android svg图片转换工具：   
   http://inloop.github.io/svg2android/   
   
代理下载android源代码：   
   https://github.com/foxleezh/AOSP/issues/1    
   
网页查看代码工具：   
   https://github.com/oracle/opengrok  
linux代码：   
   https://elixir.bootlin.com/linux/latest/source   
   
linux apt 镜像地址 /etc/apt/sources.list：　　　  
~~~ shell
deb-src http://archive.ubuntu.com/ubuntu xenial main restricted #Added by software-properties
deb http://mirrors.aliyun.com/ubuntu/ xenial main restricted
deb-src http://mirrors.aliyun.com/ubuntu/ xenial main restricted multiverse universe #Added by software-properties
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-updates main restricted multiverse universe #Added by software-properties
deb http://mirrors.aliyun.com/ubuntu/ xenial universe
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates universe
deb http://mirrors.aliyun.com/ubuntu/ xenial multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-updates multiverse
deb http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-backports main restricted universe multiverse #Added by software-properties
deb http://archive.canonical.com/ubuntu xenial partner
deb-src http://archive.canonical.com/ubuntu xenial partner
deb http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted
deb-src http://mirrors.aliyun.com/ubuntu/ xenial-security main restricted multiverse universe #Added by software-properties
deb http://mirrors.aliyun.com/ubuntu/ xenial-security universe
deb http://mirrors.aliyun.com/ubuntu/ xenial-security multiverse

~~~~
   
   https://android-review.googlesource.com/c/platform/cts/+/951278

建立git仓库能够进行git clone   
服务端：   
git remote add origin ssh://archermind@10.13.14.7:/work/p_unity/AOSP_8.1/packages/apps/XRService   
git push origin master    
客户端：  
git clone ssh://archermind@10.13.14.7:/work/p_unity/AOSP_8.1/packages/apps/XRService   
git push ssh://archermind@10.13.14.7:/work/p_unity/AOSP_8.1/packages/apps/XRService 

//可以通过部分命令查找全部命令
"\e[A": history-search-backward
"\e[B": history-search-forward
~/.inputrc
