---
author: fumi
comments: true
date: 2008-08-26 04:36:34+00:00
layout: post
link: https://fumi.me/2008/08/26/eeeubuntu-5-emobile-emone/
slug: eeeubuntu-5-emobile-emone
title: eeeUbuntu - (5) emobile (EMONE)
wordpress_id: 209
categories:
- EeePC
- Mobile
- Ubuntu
tags:
- EeePC
- eeeUbuntu
- emobile
- EMONE
- Ubuntu
---

USBもEMONEも繋ぎ方は同じみたいです。右上のNetworkManagerから手動でネットワークを設定するを選びます。ロックの解除→PPP接続で、以下の設定をします。

* 全般
  * 接続の種類: シリアルモデム
  * 電話番号: *99***1#
  * ユーザ名: em
  * パスワード: em
* モデム
  * モデムのポート: /dev/ttyUSB0
  * ダイアルの種類: Tones
* オプション: 全てチェック
  * モデムをインターネットに対するデフォルトルートにする
  * ISPプロバイダが提供するネームサーバを利用する
  * 切断されたり接続に失敗した場合に再試行する


再起動すると、NetworkManagerに新たにダイアルアップ接続という項目が追加されているので、"ppp0 via Modem に接続します" を選択します。そうすると、NetworkManagerのアイコンは何故か接続に問題ありのアイコンのままですが、インターネットに繋がっています。pingなどで確認してみて下さい。
