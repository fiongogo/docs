
为什么我用CDT开发jni时，添加的.cpp文件 .h文件在eclipse编辑下总会出现错误信息，但不影响编译和运行。
如下:

是由于没有将jni.h导入的缘故，而这个文件在ndk的目录下面。所以，参照以下步骤：
Project Properties -> C/C++ General -> Path and Symbols
选择include标签，Add -> $Android_NDK_HOME/platforms/android-14/arch-arm/usr/include
且选中All languages.
最后Apply -> OK
http://bbs.csdn.net/topics/380148227

android adt自带eclipse无法设置ndk路径

http://jingyan.baidu.com/article/4d58d5413000a09dd4e9c0fe.html
