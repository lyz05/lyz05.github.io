---
title: 【NOIP】10.29总结 B组
tags:
  - 总结
categories:
  - 信息学
  - 原创
date: 2015-10-29 17:05:00
mathjax: true
---
<strong>概述
--
今天这套题并不太难，时间分配还算比较合理。第一题花费的时间有点多。
第四题，一开始想的太复杂了。打程序前一定要确定算法的可行性，及算法的复杂度。想好再打，不然会白白浪费很多调试时间。
<strong>T1:质数 
--
第一题比较简单，先筛选处理出$\sqrt{n}$的素数，然后枚举素数。注意一下边界，记得测试小数据，和大数据就行了。

<strong>T2:平方数游戏 
--
这题打完40分暴力后就去做后面的题，因为过多的专注于第二问的回答。没仔细观察第一问的回答，是有循环节的。当我昨晚后面的题时，回过头已经没时间了，当时也不知道有这样的规律。下次对于额外数据还是多关注一下。
<strong>T3:树上路径
--
先画一副复杂一点的树，观察一下发现每个节点只需要维护三个值就好了。
考试时不大确定其正确性。
<strong>T3:抓知了 
--
首先给定一个序列，就是要我们求最长不下降子序列。dfs动态维护F数组即可。
考试时以为既要满足最长不下降子序列,还要求它们的和。
理解错题意，下次要注意。