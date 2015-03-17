本文整个部署过程无需下载及安装使用Cygwin环境， 以下部署过程需要用到的程序及版本

请注意下载对应你系统的版本, 64位系统请保证后文全系使用64位程序, 以免遇到不必要的麻烦

1.JDK&JRE       JAVA运行时及开发包

2.ADT               是Eclipse的一个插件，这一步是为了管理安卓开发库

http://developer.android.com/sdk/index.html

作为新手, 请下载ADT Bundle For Windows, 这个版本已经包含

ADK（安卓开发包）, CDT（Eclipse的C/C++开发插件）及对应的Eclipse, 可以避免第一次部署出现的各种烦心!

3.NDK              只有ADT已经可以运行普通的Andriod程序，但是如果需要编译C/C++程序， 还需要NDK

http://developer.android.com/tools/sdk/ndk/index.html

4. cocos2dx 2.0.4版本

 

准备SDK API

下载好ADT后解压， 有如下目录

eclipse\      <- 开发环境

sdk\           <- Andriod SDK

SDK Manager.exe     <-- Android开发包管理器, 由于Andriod版本较多, 所以此管理器可以方便开发者选择部署目标机器

打开SDK Manager在Android 2.2(API 8)里的 SDK Platform, Google APIs前打勾, 点击右下角的Instal packages

如果感觉下载速度慢, 可以移步这里http://my.oschina.net/heguangdong/blog/17443, 选择Andriod离线下载

这里是下载链接

http://dl-ssl.google.com/android/repository/google_apis-8_r02.zip

http://dl-ssl.google.com/android/repository/android-2.2_r02-windows.zip

https://dl-ssl.google.com/android/repository/usb_driver_r04-windows.zip

把android开头的文件解压到platforms目录下

把goole_apis开头的文件解压到add-ons目录下

把usb_driver_r03-windows.zip解压到usb_driver目录下。

Eclipse导入工程

打开Eclipse

导入Cocos2dx例子工程:

Eclipse中File->New->Other...选择Andriod Project from Existing Code

在Import Projects的Root Directory中导入D:\Develop\RevWar\sdk\cocos2d-2.0-x-2.0.4\samples\HelloCpp\proj.android\

注意, 不要选中 Copy project into workspace, 否则路径编乱很难编译成功

 

导入cocos2dx的java框架

在src目录中new package, 输入org.cocos2dx.lib, 在org.cocos2dx.lib的package中点Import-> FileSystem

选中目录D:\Develop\RevWar\sdk\cocos2d-2.0-x-2.0.4\cocos2dx\platform\android\java\src\org\cocos2dx\lib\, 点选所有java文件

工程Properties->Builder->New->Program

在Main标签中填写

填写NDK编译命令行 D:\Develop\android-ndk-r8e\ndk-build.cmd

点击Browser Workspace选中当前工程,出现${workspace_loc:/HelloCpp}

切换到Environment标签中填写

新建NDK_MODULE_PATH 填写D:\Develop\RevWar\sdk\cocos2d-2.0-x-2.0.4\;D:\Develop\RevWar\sdk\cocos2d-2.0-x-2.0.4\cocos2dx\platform\third_party\android\prebuilt\

修改cocos2dx的Android.mk, diff如下

@@ -153,6 +153,7 @@

LOCAL_WHOLE_STATIC_LIBRARIES += cocos_jpeg_static

LOCAL_WHOLE_STATIC_LIBRARIES += cocos_libxml2_static

LOCAL_WHOLE_STATIC_LIBRARIES += cocos_libtiff_static

+LOCAL_WHOLE_STATIC_LIBRARIES += cocosdenshion_static

# define the macro to compile through support/zip_support/ioapi.c              

LOCAL_CFLAGS := -DUSE_FILE32API

@@ -164,3 +165,4 @@

$(call import-module,libpng)

$(call import-module,libxml2)

$(call import-module,libtiff)

+$(call import-module,CocosDenshion/android)

F&Q

andriod-8问题

修改D:\Develop\RevWar\sdk\cocos2d-2.0-x-2.0.4cocos2dx\platform\android\java\project.properties中的target=android-8改成你需要的版本

resources.ap_ does not exist

assert目录中有资源出问题, 排查即可

例如: cocos2d-2.0-x-2.0.4\samples\TestCpp\proj.android\assets\Images\*.pvr.gz

启动Android模拟器时的Failed to allocate memory: 8问题

调整内存值,请求内存太大导致

api版本过低导致JAVA Symbol未定义问题

setEGLContextClientVersion undefined

api8(andriod 2.2)后的版本, 才支持openGL es 2.0

自己做工程遇到的问题D:\Develop\RevWar\sdk\cocos2d-2.0-x-2.0.4\/cocos2dx/platform/android/jni/JniHelper.h:28:18: fatal error: string: No such file or directory

将cocos2dx例子中的Application.mk拷过来, 修改下内部名称即可

调试请尽量使用真机, 模拟器速度很慢

小米2默认只能管理文件, 无法用adb 连接, 因此需要安装驱动, USB驱动直接在插入电脑后的虚拟盘里找.. 这个太坑了..

保证每次都能部署最新的程序

请执行每次Clean, Build project, Debug.  真机上在需要时, 会弹出安装...

Android启动日志

带有ADT的Eclipse中有一个logcat窗口, 里面有系统及程序本身的日志, 可以做过滤,方便检查问题. 如需自己打日志, 可以使用cocos2dx中的LOGD宏来做, 原型是__android_log_print(ANDROID_LOG_DEBUG,LOG_TAG,__VA_ARGS__)

 

Remark

添加assert后, F5刷新后再编译
NDK build时,默认从工程的jni目录开始

Andriod.mk的import 原则$(call import-module,模块名) 这里的模块名必须与目录名, 模块make file中的名称报纸一致

参考文章

http://www.cnblogs.com/ybgame/archive/2012/06/07/2540693.html

发文时, Andriod Studio已经发布了一段时间, 虽然是测试版, 但将代表未来更方便的Andriod发布工具
