---
author: fumi
comments: true
date: 2009-09-27 13:34:11+00:00
layout: post
link: https://fumi.me/2009/09/27/wp-tmkm-amazon/
slug: wp-tmkm-amazon
title: wp-tmkm-amazon
wordpress_id: 2553
categories:
- WordPress
tags:
- Amazon
- WordPress
---

昨日記事を投稿するときにwp-tmkm-amazon pluginが動かなかったのですが，原因は8月からAmazon APIが認証を要求するようになったのに，wp-tmkm-amazonが開発停止となっていて対応できていないからでした．

調べたところ，wp-tmkm-amazonプラグイン配布というページで，別の方が対応したバージョンをダウンロードすることができます．以前のを削除し，これをインストールすればOKです．

また，Amazon APIの認証のために，[Amazon Web Services](http://aws.amazon.com/)でAccess Key IDとSecret Access Keyの対を取得する必要があります．
