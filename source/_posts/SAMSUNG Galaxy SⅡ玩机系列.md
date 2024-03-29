---
title: SAMSUNG Galaxy SⅡ玩机系列
tags:
  - 随笔
categories:
  - 个人
  - 原创
date: 2018-09-20 12:44:57
mathjax: true
---
# 前言
一次偶然的机会，翻出来了这部古董机。仔细研究了一下，发现这部当年的旗舰机并没有先前想的那样不堪。遂将我研究后的经验写下。

# 手机来源
作为家里第一部智能机，印象深刻。奠定了我对安卓机整体的初步认知。在此之前，我曾用过一段时间的HTC Desire S。感觉还不错，玩跑跑卡丁车，植物大战僵尸，水果忍者等早期游戏，体验都很棒。而且那部机刷了MIUI4，用起来相当的顺手。算是我最早接触的安卓机。也是因此，我产生了对MIUI的信仰。
言归正传，让我们来一起看看这部当年的三星机皇。出厂版本是Android 2.3。但实际到手时应该已经是Android 4.0.3。~~(我记得我没有升级过系统)~~,操作系统是TouchWiz，期间有过软件更新的提醒。但当时的我不知道是干啥子的，就没去更新系统。
在当年那就是**屏幕大，性能强。厚度薄。**
买的时候应该是13年，用了1年左右，因为发热严重，续航尿崩，就提前结束了它的使用。后来，我妈换新机，这部手机就归我了。但我也受不了这部机子的高热，时刻感觉会爆炸。~~(如同Note7一般)~~随后买了红米1S，弃用之。
直到今年(2017)，因为种种原因，不得不再次启用它做备用机。但如今的我，已经有相当好的使用~~(调教)~~经验。只要不是硬件硬伤，有相应的第三方软件支持，我就能带这部机重回流畅省电。

# 原因分析
## 为什么会如此的高耗电，续航崩？
首先很容易猜测到是CPU的问题。
所以，我打开了CPU-Z，能很明显的看到两个cpu的频率居高不下。这不可能啊，我啥软件都没开啊！打开后台应用进程，好像也没什么问题，最后想到开发者模式似乎可以看各个应用的占用率。
于是乎打开开发者模式中的显示CPU使用情况，就很容易发现360安全卫士一直占据第一的位置。当时，我从未想过360会这么耗CPU。
## 干掉360
刚开始的时候，想到可以直接在360中退出，但依旧会有进程残留在后台。最后直接在系统设置应用中将360后台服务结束了。
可能是我关了360自动启动的服务，重启后360就再也没有唤醒过了。
当然，你可能会问，为什么不直接卸载掉360呢？因为当年智障的我，开启了防卸载功能。360注册了设备管理器，然后我又忘记了解除防卸载的密码。我印象中记得这个功能对系统重置也是很有效的，总之挺强大的。
最后只有双清的办法，且慢，我还有很多应用没有备份完。主要还是因为我担心双清会把我内部存储的数据销毁，事实上，就算是双清也会引起问题。(后面会提到)

# 尝试刷机
刷机首要条件，是要有刷机包。突然发现i9100至今还有第三方官方维护系统更新。wow！不愧是三星旗舰机。因为一直找不到三星官方固件下载站点，所以在网上胡乱找了一些刷机包。但还好，这些刷机包都挺小的，300M左右，比起主流机型动辄1G+好太多。
因为是这部机初次刷机，所以应当循序渐进慢慢来，先刷官方包升级到最新版，在以安卓版本为顺序刷第三方包来玩。

# 基于官方4.1.2
官方Touchwiz只维护到4.1.2，这是一个十分尴尬的版本号。目前大部分软件最新版最低支持Android KitKat 4.4。更有少部分冷门软件或国外软件要求Android lollipop 5.0。所以，要有较好的软件体验，需要想办法升级安卓版本。但为了防止机子变砖，不敢过早的刷非官方版本的ROM包。
## 刷机遇阻
想要卡刷，首先要有好用的卡刷工具即RECOVERY，第三方rec我首先想到twrp，去官网查询，发现有相应的版本支持。但是只提供了img镜像，可以使用更低版本的twrp刷入，或者线刷，但是我没有电脑，不能线刷。我在网上也找不到低版本的twrp卡刷包。
所以只好用官方rec进行刷机了。除了这个基于官方的修改包，我还下载了MIUI包和cm11等其他包，防止某个包因刷机失败而进不了系统。
开始卡刷，双清之后重新开机，发现主屏幕一直崩溃，我当时想有可能是我卸载了一些系统软件导致系统的不稳定，又或者是360的锅。总之，如果没有可用的包刷入系统，这部手机就真成砖了。
重新回到rec，一个个刷机包试，试到最后一个MIUI包的时候终于成功刷入了。其他的包都因为没有官方签名，而过不了验证。既然如此那就先体验一下MIUI吧！MIUI体验请看下一章。
MIUI用了一段时间就又开始做死，想用回官方包。这时我重启发现官方rec替换成CWM了。而CWM是不会进行签名验证，所以成功上了官改的车。
## 使用体验
最新的官改包没有三星自家以及Google自家的云服务，只有最基础的系统软件。大概一页纸的自带app，用Kingroot搞定内置推广，发现好多了。续航不差，流畅度也不差，很稳定。还有一些偏原生的好用的功能。没有之前的WiFi开关bug。我认为可以长久的使用。
如果安卓版本再高一点我可能就会长期使用这个ROM了，奈何版本太低，很多软件用不了。所以踏上了Android4.4追寻之路

# MIUI V5
MIUI官网对这部机型有两位开发者提供的ROM包，均已停更。版本死在MIUI V5。但两个底层安卓版本不同，一个是4.4，一个是4.1.2。
## Android 4.4版本MIUI
意外的通过官方rec刷入的MIUI。当时只下了这一版本。因为它是最新的。
## 使用体验
卡的不能自理，系统流畅性还行，但是动画时间长。旧版MIUI基本都是靠动画时间来给人一种流畅的感觉。同样也会有大面积的发热现象。

# CM11
经过我的多方寻找，找到了鼎鼎大名的CM刷机包，这款刷机包，用了之后顿时舒服多了。我的Android版本终于上了4.4，不会遇到连知乎都装不了的问题了。

## 使用体验
如同前面所说，飞一般的流畅，而且还能开启ART模式。但是，随便使用现在最新款的应用，都容易造成CPU高频，继而带来高发热和耗电。因此，只要注意使用旧版的软件，就好了。

# 总结
这次重新研究这部手机，使我对三星有了大的改观。真实的感受到了三星强大的硬件实力。也感受到国产流氓软件对三星的毒害。事实证明不是三星硬件实力不行，而是国产软件太流氓。如果三星的价格能再亲民一点，界面能在好看易用，我可能就会选择三星了！