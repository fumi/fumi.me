---
author: fumi
comments: true
date: 2009-02-10 01:45:37+00:00
layout: post
link: https://fumi.me/2009/02/10/tdiary-to-wordpress/
slug: tdiary-to-wordpress
title: tDiaryからWordPressに移行
wordpress_id: 672
categories:
- WordPress
tags:
- HNS
- Perl
- tDiary
- WordPress
---

HNS: Hyper NIKKI Systemと[tDiary](http://www.tdiary.org/)で昔日記を書いていたのですが，ある時点で全公開はどうなのかなと思うようになったので，[mixi](http://mixi.jp/)の中に閉じて書いていました．しかし，最近またオープンにしたほうが良いと思えるようになってきたので，過去日記の一部を公開しようかと考えています．

HNSからtDiaryには既にデータ移行してあるので，tDiaryからWordPressに移行する方法を探していました．どうやら，多くの人が，tDiary からMovable Typeへの移行にあるスクリプトによってtDiaryからMovableType形式に変換することで，WordPressに取り込んでいるようでした．

私はtDiaryでWiki記法を使っていたため，変換用スクリプトにいくつか修正を加えました．またいくつか不具合も修正しました．修正点は以下の通りです．

* \* のリスト形式を<ul><li>で置換
* [[|]]をリンクに変換
* EUC-JP/UTF-8の問題解決 (tDiaryをWordPressに移行する(1))
* 日付が全部1970年1月になる問題を修正
* 最初から公開するようになっているのを，下書き状態で保存するように変更

変換に使用したスクリプトとパッチを以下に置いておきます．

* スクリプト: [t2m.pl.txt](/images/2009-02-10-tdiary-to-wordpress/t2m.pl.txt)
* [オリジナルに対するパッチ](/images/2009-02-10-tdiary-to-wordpress/t2mpl.diff)


### 参考URL
* tDiary からMovable Typeへの移行
* tDiaryをWordPressに移行する(1)
