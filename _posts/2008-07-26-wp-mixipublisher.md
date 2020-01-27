---
author: fumi
comments: true
date: 2008-07-26 15:30:34+00:00
layout: post
link: https://fumi.me/2008/07/27/wp-mixipublisher/
slug: wp-mixipublisher
title: WordPressからmixiへ投稿
wordpress_id: 80
categories:
- Mixi
- WordPress
tags:
- Mixi
- WordPress
---

[Wp-MixiPublisher 1.0.0 RC2](http://factage.com/yu-ji/archives/2006/09/05/wp-mixipublisher-1_0_0rc2/)というプラグインがあるのを知ったので試していたましたが、うまく投稿できません。mixiのWordPressコミュニティによると、変更版に差し替えて、さらにこの修正を行えばよいらしいですが、、動いていない人も多数います。どうもPHP5だと動き、PHP4だと駄目なようで。確かにここで使っているハッスルサーバーもPHP4。




@ITのPHP5とPHP4の変更点の記事([a](http://www.atmarkit.co.jp/fcoding/articles/php5/01/php501a.html),[b](http://www.atmarkit.co.jp/fcoding/articles/php5/01/php501b.html))を見ましたが、大きな変更点はオブジェクトの代入らしい。そこらへんが間違っているんでしょうか。
