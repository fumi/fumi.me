---
author: fumi
comments: true
date: 2008-08-24 13:52:11+00:00
layout: post
link: https://fumi.me/2008/08/24/eeeubuntu-network/
slug: eeeubuntu-network
title: eeeUbuntu - (3) Network, システムアップグレード
wordpress_id: 197
categories:
- EeePC
- Ubuntu
tags:
- EeePC
- eeeUbuntu
- Ubuntu
---

eeeUbuntu 8/24の最新版だと、前の版で苦労したWEP+ステルスモードでも右上のNetworkManagerから指定することができました。かなり便利になっていますね
インターネットに繋げるようになったら、システムをアップデートします。



    
    <code>
    $ aptitude update
    $ aptitude safe-upgrade
    </code>




私の場合、この後にさらに一度upgradeの通知が来ました。新しいカーネルも入っているので、全部upgradeし終わったら再起動します。そうすると、システムが最新のEEE PCドライバをインストールするかどうかを聞いてくるのでインストールします。これを行わないと、無線LANなどが使えません。
