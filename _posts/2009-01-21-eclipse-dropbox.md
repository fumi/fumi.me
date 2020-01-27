---
author: fumi
comments: true
date: 2009-01-21 12:42:55+00:00
layout: post
link: https://fumi.me/2009/01/21/eclipse-dropbox/
slug: eclipse-dropbox
title: Eclipse + Dropbox はあまりよくない
wordpress_id: 611
categories:
- Software
tags:
- Dropbox
- Elicpse
- Mercurial
- Subversion
---

いつも Eclipse を使おうとして挫折するのですが，また頑張って使ってみています．一つ気付いたのは，大きいディスプレイで使うと快適で，使うきになるということです．




Eclipse の workspace を Dropbox で共有したらどうだろうと思い，試しに Robocode のプロジェクトを作ってみました．結果は，うまく動きません．私のようにWindows, Mac, Ubuntuと異なる環境で併用しようとすると，Windowsで作成したworkspaceはMacやUbuntuではうまく読めません．設定情報を.付きのファイル (.classpathなど)で管理しており，これが問題の一端になっているようです．他にも原因があるかもしれませんが，とりあえず workspace を共有するには向いていません．




同じOSで同じ設定をした状態だとうまくいくのかもしれませんが，素直に各プロジェクト毎に[Subversive](http://www.eclipse.org/subversive/)や [Mercurial Eclipse](http://www.vectrace.com/mercurialeclipse/)などで管理するほうがよさそうです．
