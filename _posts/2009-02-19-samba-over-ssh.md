---
author: fumi
comments: true
date: 2009-02-19 07:32:18+00:00
layout: post
link: https://fumi.me/2009/02/19/samba-over-ssh/
slug: samba-over-ssh
title: Samba over SSH
wordpress_id: 2158
categories:
- Software
tags:
- Samba
- SSH
- Windows
---

Unix的小ネタも時々書いていこうと思います．

Sambaによるファイル共有は，Windowsクライアントが多い環境ではよく行われていると思うのですが，セキュリティ上接続が許可されているネットワークは限定されています．もし外部からも扱いたい場合は，VPNではなくても，SSH Portforwardingで手軽にできます．しかし，Windowsクライアントは既に139番ポートを使っているので，そのままでは転送できません．そこでループバックデバイスを使い，そのポートとサーバ側のポートを繋ぐことで使えるようになります．Windowsには標準でMicrosoft Loopback Adapterというループバックデバイスがありますので，以下の手順で設定をします．

* ハードウェアの追加でMicrosoft Loopback Adapterを追加
* Microsoft Loopback AdapterにIP: 169.254.xxx.1, Netmask: 255.255.0.0を設定
* PortForwarderやPuTTYなどで169.254.xxx.1の139番ポートを転送するように設定

詳細は以下のページが参考になります．

* SSH のポート転送を用いて Samba にアクセスする
* [Samba over SSH](http://blog.asial.co.jp/208)
