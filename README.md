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


## 1.4 版本发布流程

```
1. 拉一份全新的代码（Beetle/build/core/version_defaults.mk，修改BUILD_VERSION := 00.00.01-00）
2. 编译并验证版本（提交build/core/version_defaults.mk）
3. 打tag并推送服务器
./repo forall -c 'pwd;git tag tag_rk3288_hzl_nx7_00.00.01 -m "tag_rk3288_hzl_nx7_00.00.01";git push origin tag_rk3288_hzl_nx7_00.00.01'

4. 生成当前commit节点的tag xml文件：
./repo manifest -o tag_rk3288_hzl_nx7_00.00.01.xml -r

5. 提交tag xml文件：
cp tag_rk3288_hzl_nx7_00.00.01.xml .repo/manifests
cd .repo/manifests
git add tag_rk3288_hzl_nx7_00.00.01.xml
git commit -m 'tag_rk3288_hzl_nx7_00.00.01'
git push origin HEAD:refs/for/AMT-Android-7.1.2

6. 下载代码验证
repo init -u ssh://n000339@gerritnj01.archermind.com:29418/Beetle/manifest -b AMT-Android-7.1.2 -m tag_rk3288_hzl_nx7_00.00.01
repo sync -c
```

## 1.5 拉一个新的分支
```
repo forall -c 'git push origin HEAD:refs/heads/JUKI_Panel' 2>&1 | tee ./log.txt
检查log中有无error，对应单独处理一下

gerrit网站配置branch权限
```

./repo init -u ssh://n000339@gerritnj01.archermind.com:29418/Beetle/manifest -b AMT-Android-7.1.2 JUKI_Panel.xml   

## 1.6编译bootimage   
git clone https://aosp.tuna.tsinghua.edu.cn/kernel/msm    
git branch -r --contains d59db4e    
git checkout -b android-msm-hammerhead-3.4-kitkat-mr2  origin/android-msm-hammerhead-3.4-kitkat-mr2   
cd kernel/msm  
export ARCH=arm64  
export PATH=../../prebuilts/gcc/linux-x86/aarch64/aarch64-linux-android-4.9/bin:$PATH  
export CROSS_COMPILE=aarch64-linux-android-  
make marlin_defconfig  
make  
cp arch/arm64/boot/Image.lz4-dtb ../../device/google/marlin-kernel   
make bootimage   

## 1.7piexl版本  
refs/tags/android-8.1.0_r38    
OPM4.171019.021.P1   

## 1.8  a/b系统刷机   
sudo fastboot flash boot_a out/target/product/sailfish/boot.img    
sudo fastboot flash boot_b out/target/product/sailfish/boot.img   
sudo fastboot flash  system out/target/product/sailfish/system.img   
sudo fastboot flash system_b out/target/product/sailfish/system_other.img  
sudo fastboot erase cache     
sudo fastboot erase userdata  
sudo fastboot reboot   

## 1.9 aar静态库文件反编译重新打包  
1.将aar文件解压    
2.替换或者修改解压之后的文件   
3.jar cvf newAAR.aar  . 使用该命令重新打包整个目录下文件形成新的静态库   

## git ignore   
git config --global core.excludesfile ~/.gitignore    

*.log   

#Android Studio Navigation editor temp files  
.navigation/   

#Android Studio captures folder  
captures/  

#Intellij   
*.iml   
#.idea/workspace.xml  
.idea/  
.idea/libraries  
.idea/caches  
.idea/codeStyles  

#Keystore files   
*.jks   

#External native build folder generated in Android Studio 2.2 and later   
.externalNativeBuild   


## vscode运行python
python -m venv ./xiaozhi   
.\xiaozhi\Scripts\activate   
pip install -r requirements.txt


###.valgrind使用方法
1.环境搭建：
 下载官网最新的代码：
Valgrind: Current Releases
wget https://sourceware.org/pub/valgrind/valgrind-3.23.0.tar.bz2
tar -jxvf valgrind-3.19.0.tar.bz2
编译valgrind：
sudo apt-get install automake
sudo apt-get install autoconf
cd valgrind-3.19.0
./autogen.sh
./configure
make -j4
sudo make install
2.使用：
/usr/local/bin/valgrind --tool=memcheck --leak-check=full --show-leak-kinds=all --log-file=valgrind_report.txt --show-reachable=yes --track-origins=yes --num-callers=30  ./SLRobot
show-reachable 为no的时候不会打印reachable的堆栈。
在程序ctrl+c后会生成报告。
definitely是绝逼的内存泄露。
indirectly也要重点关注。
Invalid read/write of size 存在野指针等问题。
3.修改验证：
 使用系统的system monitor等工具监控进程的内存的使用情况。
4.规划：
在服务器端搭建valgrind环境，在代码merge到代码仓之前进行打包检测，保证代码的安全性。


