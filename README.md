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



https://www.xuejiayuan.net/blog/e5bc7cf2e4244e89a97484c9bef69630    

device-common.mk   
KERNEL_DEFCONFIG := /work3/Pulgin/AOSP_8.1/kernel/msm/arch/arm64/configs/marlin_defconfig   
include /work3/Pulgin/AOSP_8.1/kernel/msm/AndroidKernel.mk   
ifeq ($(TARGET_PREBUILT_KERNEL),)  
    LOCAL_KERNEL := /work3/Pulgin/AOSP_8.1/kernel/msm/arch/arm64/boot/Image.lz4-dtb   
else   
LOCAL_KERNEL := $(TARGET_PREBUILT_KERNEL)   
endif   

https://blog.csdn.net/u012417380/article/details/73353670    
export ARCH=arm64   
export PATH=/work3/Pulgin/AOSP_8.1/prebuilts/gcc/linux-x86/aarch64/aarch64-linux-android-4.9/bin:$PATH   
export CROSS_COMPILE=aarch64-linux-android-   
make marlin_defconfig    
make   
