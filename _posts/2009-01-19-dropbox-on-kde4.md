---
author: fumi
comments: true
date: 2009-01-19 16:19:56+00:00
layout: post
link: https://fumi.me/2009/01/20/dropbox-on-kde4/
slug: dropbox-on-kde4
title: Dropbox on KDE4
wordpress_id: 591
categories:
- Software
- Ubuntu
tags:
- Dropbox
- KDE
- Kubuntu
- Ubuntu
---

[以前触れたとおり](http://fumi.me/2009/01/05/dropbox/)，私は[Dropbox](http://www.getdropbox.com/)をファイル共有に使っています．Linux版のDropboxはnautilusというGNOME用のファイルマネージャのアドオンとして作られているので，どの程度 KDE 上で動くか不安でしたが，今のところ問題なく動いています．




[Ubuntu8.10用のソフトウェア](http://www.getdropbox.com/downloading?os=lnx)をダウンロードしてインストールしようとすると，必要なライブラリも全部インストールしてくれます．または/etc/apt/sources.listに以下を書いてからaptitudeでインストールしても良いです．



    
    <code>
    deb http://linux.getdropbox.com/ubuntu intrepid main
    deb-src http://linux.getdropbox.com/ubuntu intrepid main
    </code>




ターミナルでnautilusを実行すると，Dropboxが右下のタスクバーに表示されますので，クリックするとアカウントの設定ができます．後はファイルの同期を待つだけです．
