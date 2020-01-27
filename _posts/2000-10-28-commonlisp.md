---
author: fumi
comments: true
date: 2000-10-28 03:00:01+00:00
layout: post
link: https://fumi.me/2000/10/28/commonlisp/
slug: commonlisp
title: CommonLisp
wordpress_id: 739
categories:
- 未分類
---

今度は研究室にあったCommonLispの本を読んだ。
知識ベース論はGCL(GnuCommonLisp)使ってやるので。
載っている例題、あんまり解けないよう。
![COMP]  kde2コンパイル覚え書き。
kdebase-2.0はinfo_netbsd.cppのコンパイルでこける。
info.cppの中の#include "info_netbsd.cpp"を
#include "info_generic.cpp"にすると一応通る(逃げともいう)。
CPU情報などをここでとっているみたいだけど、まぁ使えなくてもいいか。
kwin/clientsの各種は、Makefileの中で〜.closureを使わないようにすると、
非常に危なげなメッセージがでるけど、一応makeが通る。
kwinのコードだから、動かなかったときはenlightenmentに
すればなんとかなるだろうか。
koffice,kdeutilsはvalues.h,feature.h,gnu/stub.hをLinuxの/usr/includeから
持ってくれば一応make可能。
中身はdefineだけなので大丈夫と決め付ける。
M_PIをなぜか読んでくれないので、math_values.hとかいうのを適当に作った、
includeするのはkchart/enginepie.cc,kchart/kcharEngine_ComputeSize.cc。
とおもったら、feature.hのdefineがいけないみたい。
これのdefineの嵐を編集すれば、上の問題はなくなりそう。
これで、学校行ってみて動かなかったら悲しいなぁ。
TDIARY2.00.00
