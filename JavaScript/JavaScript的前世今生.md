# JavaScript的前世今生

***

## 前言

最近一段时间，一直在研读react的源码，越深入，越发现自身基础知识的薄弱，因此最近打算重新回顾一遍JS的基础，旨在查漏补缺，厚积薄发。第一篇文章主要想讲讲JS的发展历史，了解JS的本质、历史以及局限性。

## Mosaic

Mosaic浏览器是由美国伊利诺大学的NCSA组织在1993年发表的第一个可以显示图片的浏览器，在当时一度引起轰动，可以说很大程度推动了互联网的发展。

![img](https://upload-images.jianshu.io/upload_images/8793674-9c6b08cf9693b0af.jpg)

## Netscape

1994年Mosaic研发的核心成员马克·安德森（Marc Andreessen）和几何图形发生器的发明人吉姆·克拉克（Jim.H.Clark）共同创立了Mosaic Communication Corporation。而Mosaic 公司成立后，由于伊利诺伊大学拥有 Mosaic 的商标权，且伊利诺伊大学已将技术转 让给 Spy Glass 公司，开发团队必须彻底重新撰写浏览器程式码，且浏览器名称更改为Netscape Navigator。

在二人领导下，公司合力进行超越以往浏览器的新一代浏览器的研发，试图打破Mosaic的垄断并取得业界的领导地位。所以对新浏览器名为 Netscape Navigator，即“导航者”。而它的对内称呼为Mozilla，意为Mosaic杀手，也是之后创造火狐浏览器的公司的名字。

1995 年，JavaScript随着􏱧网景􏱨公司􏱩发布􏱪的 Netscape Navigator 2.0 问世􏱪，它最初命名􏱫􏱬􏱭为 LiveScript，它􏰩自􏰘今的 Mozilla 􏱨􏱩的 CTO——Brendan Eich 之􏱯手，􏱏其产生􏰒源于网景􏱨􏱩发布的 Netscape Navigator 􏱰􏱱􏱲􏱳需要一种脚本语言来协助浏览器进行一些简单的动态操作。而在当时网景公司和Sun公司达成联盟，出于利用Java 这个因特网时髦词汇达到推广目的，就在 Netscape Navigator 2.0 即将正式发布前，Netscape 将其更名为 JavaScript。

![img](https://gss0.bdstatic.com/94o3dSag_xI4khGkpoWK1HF6hhy/baike/c0%3Dbaike116%2C5%2C5%2C116%2C38/sign=e9c573b4bd3533fae1bb9b7cc9ba967a/b812c8fcc3cec3fd0c1e5dcfda88d43f8794276c.jpg)

如果不是公司的决策，Brendan Eich绝不可能把Java作为Javascript设计的原型。作为设计者，他一点也不喜欢自己的这个作品：

> "与其说我爱Javascript，不如说我恨它。它是C语言和Self语言一夜情的产物。十八世纪英国文学家约翰逊博士说得好：'它的优秀之处并非原创，它的原创之处并不优秀。' (the part that is good is not original, and the part that is original is not good.)"

1996年  Netscape Navigator 3.0问市，此版本有分为“Standard Edition”和“Gold Edition”两个版本，后者具备邮件软件和所见即所得的网页编辑程式，此时网景的占有率达到70%的高峰。

同时Netscape Navigator 迎来一个强大对手来自微软开发的Internet Explorer，展开后世称为浏览器大战的占有率争夺战。

## Microsoft

从 1995 年Netscape Navigator 2.0 发布以来，市场上的网页浏览器标准都以 Netscape 主导，直到1996年8月13日，微软IE3发布。而IE 3.0 搭载了一个 JavaScript 的克隆版，叫做 JScript（这样命名是为了避免与 Netscape 潜在的许可纠纷）。微软进军浏览器市场，双方激烈竞争就此展开，在此之前微软曾经尝试收购Netscape公司，遭到了拒绝。到了1997年IE4的市场占有率已经达到了15%，Netscape（69%），而我们都知道到了1999年两者的情况得到了翻转，微软占据了绝大部分浏览器市场，原因无外乎两个一是彼时微软已经占据了绝大部分pc的操作系统市场，而作为亲儿子的IE自然的到了大力推广，二是Netscape是一家浏览器企业，为了收益，Netscape Navigator 是收费的，而IE是免费的，因此在IE技术赶上的时候就是Netscape Navigator 消亡的时候。而后面带着V8引擎而来的Chrome席卷浏览器市场又是后面的故事了。

![img](https://gss0.bdstatic.com/-4o3dSag_xI4khGkpoWK1HF6hhy/baike/c0%3Dbaike92%2C5%2C5%2C92%2C30/sign=8787c637a68b87d6444fa34d6661435d/7dd98d1001e9390115a4f9387cec54e736d19615.jpg)



## ECMA

在微软进入后，有 3 种不同的 JavaScript 版本同时存在：Netscape Navigator 3.0 中的 JavaScript、IE 中的 JScript 以及 CEnvi 中的 ScriptEase。作为开发者同一段逻辑的代码，要分别写三遍，这无疑极大的降低了开发效率。随着业界担心的增加，这个语言的标准化显然已经势在必行。

1997 年，JavaScript 1.1 作为一个草案提交给欧洲计算机制造商协会（ECMA）。第 39 技术委员会（TC39）被委派来“标准化一个通用、跨平台、中立于厂商的脚本语言的语法和语义”(http://www.ecma-international.org/memento/TC39.htm)。由来自 Netscape、Sun、微软、Borland 和其他一些对脚本编程感兴趣的公司的程序员组成的 TC39 锤炼出了 ECMA-262，该标准定义了名为 ECMAScript 的全新脚本语言。

1999年12月，ECMAScript 3.0版发布，是对ECMAScript标准第一次真正的修改。从各方面综合来看，第3版标志着ECMAScript成为了一门真正的编程语言。也成为JavaScript的通行标准，得到了广泛支持。

2007年10月ECMAScript 4.0版草案发布对3.0版做了大幅升级，预计次年8月发布正式版本。草案发布后，由于4.0版的目标过于激进，各方对于是否通过这个标准，发生了严重分歧。以Yahoo、Microsoft、Google为首的大公司，反对JavaScript的大幅升级，主张小幅改动；以JavaScript创造者Brendan Eich为首的Mozilla公司，则坚持当前的草案。2008年7月ECMAScript 4.0发布前被废弃由于对于下一个版本应该包括哪些功能，各方分歧太大，争论过于激进，ECMA开会决定，中止ECMAScript 4.0的开发（即废除了这个版本）。

2015年ECMAScript 6正式发布，并且更名为“ECMAScript 2015”。它吸收了之前ES4，ES5的内容，ECMAScript 2015的发布代表JS迎来了新时代，它是是JavaScript语言的下一代标准，提供了许多新的语法和编程特性以提高ECMAScript的开发效率并优化ECMAScript的开发体验。

之后的每年都会推出一些新特性，最近的一版是ECMA2019又带来了新的八个功能，有时间会新开一篇文章介绍一下，ES6之后每个版本的一些新功能。

 																																									