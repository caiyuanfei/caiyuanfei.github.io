---
title: hexo博客的优化与配置
date: 2016-01-26 16:22:04
tags:
- Hexo
- 技术
---
添加统计代码
========

上周成功用Hexo+Github Pages搭建好博客，但是还有很多功能等待添加的,今天就继续进行优化，首先是添加统计代码，数据统计方面有以下几个:

1. [Google Analytics](http://www.google.com/analytics/web/?hl=zh-CN)
2. [百度统计](http://tongji.baidu.com/web/welcome/login)
3. [不蒜子](http://busuanzi.ibruce.info/)

然后就是站长工具:

1. [CNZZ|站长统计](http://zhanzhang.cnzz.com/)
2. [谷歌站长工具](http://www.google.com/intl/zh-CN/webmasters)
3. [百度站长工具](http://zhanzhang.baidu.com/)
4. [站长之家工具](http://tool.chinaz.com/)
5. [360搜索站长平台](http://zhanzhang.so.com/)

感觉站长工具会比较详细点，所以就采用站长工具，用的是cnzz的，参考了[hexo博客的优化与配置——添加统计代码](http://blog.csdn.net/whjkm/article/details/37884563).

首先在`\theme\yilia\_config.yml`添加一行代码:

    #### Analytics
    cnzz: true
这里我用的是**yilia**主题。

登录[CNZZ](http://zhanzhang.cnzz.com/)中，注册，添加网站，然后会得到代码，选择想要显示的形式，可以只是文字形式，也可以是图表形式，复制给出的代码，然后在`\theme\yilia\layout\_partial`里面创建一个**cnzz.ejs**文件，把刚刚复制的代码添加进去:

    <% if (theme.cnzz){ %> 
    <script type="text/javascript">
        var cnzz_protocol = (("https:" == document.location.protocol) ? " https://" : " http://");
        document.write(unescape("%3Cspan id='cnzz_stat_icon_1257376919'%3E%3C/span%3E%3Cscript src='" + cnzz_protocol + "s11.cnzz.com/z_stat.php%3Fid%3D1257376919' type='text/javascript'%3E%3C/script%3E"));
    </script> 
    <% } %>
主要是替代这段代码中第二行**<script **开始到倒数第二行的**</script>**。

最后在after_footer.ejs（或者footer，或head，可以自己选择需要出现站长统计的位置）的后面添加一行代码即可:

    <%- partial('cnzz') %> 

这样就可以了，然后就执行`hexo generate`,`hexo deploy`发布网站即可。