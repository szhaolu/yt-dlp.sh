# 关于Youtube-dl的在Ubuntu18.04及以上版本的安装使用与错误修正说明！
 
Youtube-dl个人感觉是一款不错的Youtube视频下载工具与FFMPEG配合可以在主机上很轻松的下载Youtube上的任意可视视频。
关于Youtube-dl的教程网上多的很。基本上都只说明了安装步骤。却没有说明使用是报错问题的解决与修正。
这次本文连同安装与错误解决方案一同说明。  
Youtube-dl基本支持三种系统。Centos 、Ubuntu、Windows。个人感觉Ubuntu 安装时比较容易看懂。使用是在压制视频时比其他两个系统都要显得略好一些。
本文就用Ubuntu 18.04 为例。从安装到使用及报错等解决方法。**【虽然步骤比较多，也比较繁琐，但是用起来你就会发现它比其他两个系统的程序要好的多。】**
## 在安装Youtube-dl前必须先安装FFMPEG
安装FFMPEG有两装方法！
* 第一种比较简单。**【初来乍到的小白适用，系统版本要≥Ubuntu18.04。】**  
`1、sudo apt-get update -y // 更新apt-get程序。`  
`2、sudo apt-get install ffmpeg -y // 直接安装FFMPEG程序。`  
这样安装出来的FFMPEG在使用中没有压缩影片时画质会有损伤。版本也不是最新的。**所以这个方式我个人不太建议使用。**  
* 第二种方式比较繁琐，**个人比较推荐使用。**  
  * 先要安装yasm程序和libsdl1.2-dev程序。  
`1、sudo apt-get update -y // 更新apt-get程序。`  
`2、sudo apt-get install yasm // 安装yasm程序。`  
`3、sudo apt-get install libsdl1.2-dev --fix-missing // 安装libsdl1.2-dev程序。`  
   * 接下来要安装SDL程序。  
前往[SDL的官网](http://www.libsdl.org)在里面找到Download目录栏，复制最新版本的SDL（这里我用SDL version 2.0.10为例。）  
`1、sudo apt-get wget -y // 安装下载工具若系统中已有可以忽略此行。`  
本人建议是在安装FFMPEG前先建立一个文件夹，只是个人习惯看着界面整洁一些罢了。  
`1、mkdir /home/ffmpeg // 在/home目录下新建一个ffmpeg目录。如果你嫌弃繁琐可以忽略。`  
`2、cd /home/ffmpeg // 进入ffmpeg目录。`  
下面正式下载安装SDL程序。【这里要说一下程序时常更新换代，下载的连接自己去官网查阅。】  
`1、sudo wget http://www.libsdl.org/release/SDL2-2.0.10.tar.gz // 下载SDL程序。`  
`2、tar -xvf SDL2-2.0.10.tar.gz // 解压安装包。`  
`3、cd SDL2-2.0.10 // SDL程序目录。`  
`4、./configure // 执行脚本。`  
`5、make && make install // 安装解析程序文件。（这里安装需要时间，请耐心等待。不要中断！）`  
`6、cd .. // 返回上一级目录。`  
然后同理下载安装 FFMPEG 程序 【这里要一样程序时常更新换代，下载的连接自己去官网查阅。】  
前往[FFMPEG 的官网](https://www.ffmpeg.org/download.html)在里面找到最新版本的FFMPEG（这里我用 FFMPEG-4.2.1.tar.bz2 为例。）  
`1、sudo wget https://ffmpeg.org/releases/ffmpeg-4.2.1.tar.bz2 // 下载 ffmpeg程序。`  
`2、tar -xvf ffmpeg-4.2.1.tar.bz2 // 解压 ffmpeg程序。`  
`3、cd ffmpeg-4.2.1 // 进入 ffmpeg目录。`  
`4、./configure // 执行脚本。`  
`5、make && make install // 安装解析程序文件。这里说一下常规的VPS主机大约也需要10分钟左右才能安装完成。请耐心等待。`  
`6、ffmpeg -version // 检查ffmpeg版本。（嫌繁琐可以忽略这一条。）`  
## 弄好了上面的一切，下面就可以安装Youtube-dl了。  
  前往[Youtube-dl的官网](https://yt-dl.org) 下载最新版本的程序，当然你也可以自己手动下载在这个里面[Github库](https://github.com/ytdl-org/youtube-dl)相关命令参数也可以参考这里。  
  当然本库也有备份的程序。在本库的Apps目录中 [youtube-dl](https://raw.githubusercontent.com/szhaolu/Ubuntu/master/Youtube-dl/apps/youtube-dl)如果你从这里下载安装后需要-U参数进行升级。**若无法下载请扶梯**  
`1、curl -L https://yt-dl.org/latest/youtube-dl -o /usr/bin/youtube-dl // 下载与安装Youtube-dl。`  
`2、sudo chmod 755 /usr/bin/youtube-dl // 给程序文件赋予权限。`  
弄到这里安装的部分就结束了，但是你还是无法使用用youtube-dl 运行命令后一定会如下下错误代码。  
` // /usr/bin/env: ‘python’: No such file or directory。`  
简单解释一下这个问题，是由于开发人员使用的是Windows程序进行的编译，导致了编码不匹配所致。国内很多网站都有相关解释。但就是没有针对性的解决方法。  
我也是在一家国外的叫做[askubuntu](https://askubuntu.com/questions/1037666/youtube-dl-python-not-found-18-04)论坛上看见后才彻底解决此项问题的。**（时而直通时而扶梯扶墙。）**  
`1、sudo apt remove youtube-dl //解除 Youtube-dl与系统的关联。`  
`2、sudo apt install python3-pip -y // 安装 python3-pip 这里不知道为什么，明明系统中有却还要在装一遍。不然就不行。`  
`3、pip3 install --user youtube-dl // 在pip中重新安装挂载youtube-dl。`  
`4、sudo ln -s /usr/bin/python3 /usr/local/bin/python // 进行系统python的关联。`  
弄到这里基本上Youtube-dl就能正常使用了。  
这里我们用一个视频作为例子。【注意你的主机能登陆Youtube这是重点。出不去，无法访问其他一切都是白搭。】  
【考虑到视频著作权问题视频文件后缀以XXXXXX代替。】  
* 首先建议单独为Youtube建立一个目录（个人习惯不弄也是可以的。）  
`1、youtube-dl -F https://www.youtube.com/watch?v=XXXXXX // 这里一定是要大写-F展开视频目录。`  
目录如下显示：（以下呈现的是图片文件若不显示，请扶梯看效果。在文件在本目录下的img文件夹中。）  
![](https://raw.githubusercontent.com/szhaolu/Ubuntu/master/Youtube-dl/img/youtube-dl_F.jpg)  
这里展开后有媒体流、音频流与视频流分离的各种文件，也有压缩整合好的现成的媒体格式下载这里要注意区分。  
有avc与video 组合呈现的就是可以不用FFMPEG编译下载就能看听的。画质一般不高，上面有分辨率显示。要仔细看  
【在这里不推荐，本人一直是下载高清组合媒体视频用FFMPEG直接编译后在下载。】操作如下。  
`1、youtube-dl -f 248+251 https://www.youtube.com/watch?v=XXXXXX //这里一定是要-f` **还要注意的是一定要遵循视频在前音频在后的原则。**  
结果呈现如下：（以下呈现的是图片文件若不显示，请扶梯看效果。在文件在本目录下的img文件夹中。）  
![](https://raw.githubusercontent.com/szhaolu/Ubuntu/master/Youtube-dl/img/youtube-dl_ok.jpg)  
这样视频连同下载加编译全部完成。ls 之后你就能看见视频文件了。主机上直接用播放器播放即可。如果是远端VPS回传下载即可。当时这个是webm的网页媒体流。  
## 下面有个特殊情况报错！  
`python File "/usr/bin/pip", line 11, in <module> sys.exit(main()) File "/usr/lib/python3.4/site-packages/pip/__init__.py", line 215, in main locale.setlocale(locale.LC_ALL, '') File "/u`  
先按照上面的步骤测试一下是否能完全成功有无报错，若一切正常下面的不用做了。  
* 问题是python与python-pip出问题了。  
到目前为止只发现个别VPS主机的Ubuntu 18.04系统。出现过这个问题！这一类问题一般是在Windows的python会有出现，Ubuntu的主机我也是只是在Stallion这样VPS运营商那里遇到过。  
解决方法如下：  
`1、python --version // 检查python 版本与是否安装。`  
`2、pip --version // 检查python 版本与是否安装。（大部分都是pip没有安装完全。）`  
`3、sudo  apt-get install python-pip -y // 安装 python-pip。`  
`4、unset LC_ALL`  
`5、pip install virtualenv // 在pip 安装 virtualenv。`  
`6、export LC_ALL=C  // 这里是重点`  
这样要说一下如果不能显示中文可能是因为你的VPS是裸机导致没有中文字库。这里可以参看一下Ubuntu 18.04中文字库的安装方法。[仅供参考](https://github.com/szhaolu/Ubuntu/blob/master/Language/%E5%9C%A8Ubuntu18.04%E5%AE%89%E8%A3%85%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87%E5%92%8C%E7%B9%81%E4%BD%93%E4%B8%AD%E6%96%87.md)中文包方法。  
弄完以后Youtube-dl就能正常使用了。  
## 关于下载文件时的403错误的修正。  
当我们通过Youtube-dl下载视频时使用 -F可以正常打开文件目录。但是使用-f时出现以下错误：  
`“ERROR: unable to download video data: HTTP Error 403: Forbidden”`时。无法下载正确的视频。  
目前无法确定错误的发生原因。一般出现在视频发布者在视频工具调节选项中加入了视频注释内容和订阅选项。导致了视频在同一程序下只能被浏览一次。  
尝试性解决方法如下（这里不能保证全部有效。）：  
* 1、可以先升级Youtube-dl “使用命令：`youtube-dl -U`来升级。Youtube-dl到最新版本。  
* 2、使用Youtube-dl中的清除缓存的工具来清空刚刚因 “-F”而访问的目录文件。使用命令：`youtube-dl --rm-cache-dir`少等一会儿后。再次直接使用 “-f 视频文件ID+音频文件ID 视频网址”方式。这里不要再次打开文件目录。避免不必要的错误。  
