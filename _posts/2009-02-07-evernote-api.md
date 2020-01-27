---
author: fumi
comments: true
date: 2009-02-07 08:22:08+00:00
layout: post
link: https://fumi.me/2009/02/07/evernote-api/
slug: evernote-api
title: Evernote API
wordpress_id: 647
categories:
- EverNote
- Software
tags:
- EverNote
- Programing
- Thrift
- WebAPI
---

Evernote は去年から開発者向けのAPIを提供しています．Evernote APIは，Facebookが開発した[Thrift](http://incubator.apache.org/thrift/)で書かれています．Thriftは多言語間を接続するためのRPCフレームワークで，現在はApacheのプロジェクトとしてオープンソースとして公開されています．Thriftは現在C++，Java，Python，PHP，Ruby，Erlang，Perl，Haskel，C#，Cocoa，Smalltalk，OCaml用のコードを生成できるようです．Thriftを用いることで，資源管理をC++，並列処理をErlangといったように，得意な分野ごとに言語を分けるといったことが可能になります．Thriftについては，[CyDN - フレームワーク 「 Thrift 」 調査報告](http://cydn.cybozu.co.jp/2007/06/thrift.html)や[Kansai.pm#10 での発表資料 (Thrift について)](http://d.hatena.ne.jp/naoya/20080810/1218372988)が参考になります．




Evernote APIを使うためには，まず初めにAPI Keyの申請を行う必要があります．その際に，どのようなアプリケーションを作りたいかをコメント欄に書きます．私はコマンドラインツールを作りたいという旨を書きました．問題なければ，API keyを送ってくれるはずです．API keyは，開発用のサーバのみで使えます．運用サーバでも有効にするには，開発後に別途申請が必要のようです．開発用サーバは，機能は運用サーバと同等ですが，バックアップされておらず，処理も限定的だそうです．開発サーバを使うためには，別途アカウントを作成する必要があります．複数アカウントを作成することもできます．




以下のリストはAPIの資料です．次のエントリで，Rubyでの開発について書きます．







  * Evernote API Overview


  * Evernote API Reference


  * [Evernote User Forum for Developer](http://forum.evernote.com/phpbb/viewforum.php?f=43)


  * 

