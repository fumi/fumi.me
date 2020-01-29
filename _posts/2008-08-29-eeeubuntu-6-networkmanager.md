---
author: fumi
comments: true
date: 2008-08-29 07:40:38+00:00
layout: post
link: https://fumi.me/2008/08/29/eeeubuntu-6-networkmanager/
slug: eeeubuntu-6-networkmanager
title: eeeUbuntu - (6) NetworkManager
wordpress_id: 215
categories:
- EeePC
- Mobile
- Ubuntu
tags:
- EeePC
- eeeUbuntu
- Emobile EMONE
- NetworkManager
- Ubuntu
---

Ubuntu は Networkの管理にNetworkManagerというのを使っていますが，emobileでppp接続時は，何故かこれがonlineだと認識してくれません。表示を見ても"ネットワーク接続なし"となります。ちゃんと繋がっているのに。で，このNetworkManagerが各アプリケーションに今offlineだよとご丁寧に通知する機能がついているので，FirefoxやPidgin (MSNなどのIM client)，Twitux (Twitter client)などが勝手にofflineモードになってしまいます。本来ならばNetworkManagerがppp接続も監視してくれればいいんですが，今回はNetworkManagerがアプリケーションにoffline通知をしないようにして問題回避しました。

```bash
$ cd /etc/dbus-1/system.d
$ sudo vi NetworkManager.conf
<allow send_interface="org.freedesktop.NetworkManager"/>を全部
<deny send_interface="org.freedesktop.NetworkManager"/>に変更
$ cd ../event.d
$ sudo ./25NetworkManager restart
$ sudo ./26NetworkManagerDispatcher restart
```

これでFirefoxを起動したときに自動的にofflineモードになったりしなくなります。
