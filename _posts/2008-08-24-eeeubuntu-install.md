---
author: fumi
comments: true
date: 2008-08-24 13:24:40+00:00
layout: post
link: https://fumi.me/2008/08/24/eeeubuntu-install/
slug: eeeubuntu-install
title: eeeUbuntu - (1) インストール
wordpress_id: 190
categories:
- EeePC
- Ubuntu
tags:
- EeePC
- eeeUbuntu
- Ubuntu
---

しばらくSDHCにライブCDの部屋のeeeUbuntuをインストールして試用していました。ステルスモードのWEPにつなぐのにちょっと手間取りましたが、それ以外は、SDHCにインストールしているときにサスペンドから復帰できない問題くらいです。EMONE経由でemobileにダイアルアップして普通に使えます。よって、XP消してSSDにeeeUbuntu入れることにしました。SSDに入れればサスペンドもできるようなので。




基本的には、eeeUbuntu 8.04が良くできているので、CD作成して日本語でインストールすればOKです。ジャーナリングファイルシステムだとSSDすり減らしそうなので、ext2に変更しました。パーティションは`/sda (4G,SLC) → /, /sdb (8G,MLC) → /usr`としました。うまくいけば、SDHCを/homeにするかもしれません。swapはなしです。





インストール終了後に再起動すると、EeePC機種選択が表示されるので"Eee PC 901"を選択します。私はASCII配列じゃないとプログラミングなどの効率が悪いので、キーボードの設定を変更します。キーボードレイアウト→キーボードの形式→"Generic 105-key (Intl) PC", レイアウト・オプション→Ctrlキーの位置→"CapsLockをもう一つのCtrlにする", レイアウト追加→USAを設定すると、ASCII配列で、パイプ記号やバックスラッシュも入力できます。Generic 104だとこのキーが無入力になります。




この内容は続きます。
