#相关软件下载

来源：http://leechenhwa.blog.163.com/blog/static/301782762014514104427162/

MinGW-builds 已加入 MinGW-W64  

MinGW-builds 
Dual-target(32 & 64-bit) MinGW compilers for 32 and 64-bit windows

http://sourceforge.net/projects/mingwbuilds/

MinGW-builds本身的下载资源也不错的，备忘如次。以Windows系统中安装为准，其他系统参考摸索。 
1）MinGW 
http://sourceforge.net/projects/mingwbuilds/files/host-windows/releases/ 
只更新到4.8.1，分32位和64位，分开下载。 
还要注意区分线程和异常处理方式的选择。

2）msys 等工具包 
http://sourceforge.net/projects/mingwbuilds/files/external-binary-packages/ 
最近的为msys+7za+wget+svn+git+mercurial+cvs-rev13.7z 
因此需要安装7-zip工具（http://7-zip.org/）

3）Qt 
http://sourceforge.net/projects/mingwbuilds/files/external-binary-packages/Qt-Builds/ 
最近的为x64-Qt-5.2.1+QtCreator-3.0.1-(gcc-4.8.2-seh).7z和x32-Qt-5.2.1+QtCreator-3.0.1-(gcc-4.8.2-dwarf).7z 
注意gcc的版本。特别注意的是这里的64位版本，Qt项目网站本身只提供32位版本的下载。 
（http://download.qt-project.org/official_releases/qt/5.3/5.3.0/qt-opensource-windows-x86-mingw482_opengl-5.3.0.exe）


------------- 
新领域的MinGW-builds

32位 
http://sourceforge.net/projects/mingw-w64/files/Toolchains%20targetting%20Win32/Personal%20Builds/mingw-builds/

64位 
http://sourceforge.net/projects/mingw-w64/files/Toolchains%20targetting%20Win64/Personal%20Builds/mingw-builds/

------------ 
Windows 7中添加MinGW路径 
1)在系统环境变量中新建MINGW指向解压缩的mingw文件夹（bin的上一级）; 
2)在path变量中追加;%MINGW%\bin 
3)升级MinGW版本时，只需要修改MINGW变量，指向新文件夹即可。

Windows 7中添加msys路径 
1)在系统环境变量中新建MSYS指向解压缩的mingw文件夹（bin的上一级）; 
2)在path变量中追加;%MSYS%\bin 
3)升级msys版本时，只需要修改MSYS变量，指向新文件夹即可。
