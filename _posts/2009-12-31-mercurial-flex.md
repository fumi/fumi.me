---
author: fumi
comments: false
date: 2009-12-31 03:28:17+00:00
layout: post
link: https://fumi.me/2009/12/31/mercurial-flex/
slug: mercurial-flex
title: Using Mercurial with Adobe Flex Builder
wordpress_id: 2787
categories:
- Flex
- Mercurial
tags:
- Mercurial Flex Eclipse
---

[![Mercurial設定](http://fumi.me/wp-content/uploads/2009/12/3eb755440bbeda6c454f2b85ca15fb78-300x224.png)](http://fumi.me/wp-content/uploads/2009/12/3eb755440bbeda6c454f2b85ca15fb78.png)最近Flex Builderを使っているのですが，最初から対応しているバージョン管理システムがCVSしかないなくて困っていました．Flex BuilderはEclipseがベースなのでEclipse用のプラグインが動くはずだと思い，いじっていたら動いたようなので書いておきます．




まず[Mercurial Eclipseのサイト](http://www.vectrace.com/mercurialeclipse/)を見るとSoftware updateを使えと書かれていますが，Flex BuilderはSoftware updateのメニューが消してありますので使えません．そこで直接jarファイルを[Plugins](http://www.vectrace.com/eclipse-update/plugins/)のページからダウンロードします．ダウンロードしたjarをFlex Builderのpluginsディレクトリ(Macなら"アプリケーション"→"Adobe Flex Builder 3"→plugins)に置いた後，Flex Builderを起動します．




[![ショートカット - 新規](http://fumi.me/wp-content/uploads/2009/12/deecf7c652877465f0b9a1adf3b43579-290x300.png)](http://fumi.me/wp-content/uploads/2009/12/deecf7c652877465f0b9a1adf3b43579.png)
起動後にMercurialの設定について聞かれますので，hgやgpgの場所などの設定をします．私の場合はfinkでMercurialを入れてあるので，それぞれ/sw/bin/hg,/sw/bin/gpgとしました．後は"パースペクティブの設定"→"新規","ビューの表示"でMecurialにチェックを入れれば設定完了です．




Mercurialで管理するためには，管理下に置きたいプロジェクトを右クリック→"チーム"→"プロジェクトの共用"→"Mercurial"で設定した後に，"チーム"→"Commit"で管理したいファイルをコミットすれば良いです．
