---
author: fumi
comments: true
date: 2009-02-19 07:30:50+00:00
layout: post
link: https://fumi.me/2009/02/19/debian-lenny/
slug: debian-lenny
title: Debian lenny
wordpress_id: 2151
categories:
- Software
tags:
- amavis
- Debian
- lenny
- mount. debconf
- slapd
---

週末に[Debian Gnu/Linux 5.0 (Lenny)](http://www.debian.org/releases/lenny/)がリリースされました．しばらくどこもアップグレードするつもりはなかったのですが，研究室用サーバの一台が設定ミスにより自動アップグレードしてしまい，更にそれが失敗していたので対処しました．




まず[リリースノート](http://www.debian.org/releases/lenny/releasenotes)の中で、対応するアーキテクチャの文書を読みます．今回は[amd64](http://www.debian.org/releases/lenny/amd64/release-notes/index.ja.html)版を参考にしました．また，直前のアップグレードのログは/var/log/messagesに残っているのでこれも読みます．そうするとmountパッケージのインストールに失敗していることがわかりました．これはnfs mountを使用している場合に発生するので，アップグレード前にnfs mountを全部外すか，または以下のように対処する必要があります．







  1. debconf_english,debconfのダウンロード・インストール([Google Group](http://groups.google.com/group/alt.os.linux.debian/browse_thread/thread/3944b8470cd4ecea))


  2. nfs-commonのインストール ([release note 5.2](http://www.debian.org/releases/lenny/amd64/release-notes/ch-information.ja.html#nfs-common))


  3. mountのインストール




また，slapd.confの設定が古くslapdが起動できていませんでしたので，以下の部分をコメントアウトしました．



    
    /etc/ldap/slapd.conf<code>
    #checkpoint 512 30
    </code>




その他依存関係で失敗しているパッケージがいくつかあったので一旦削除して，lennyにパッケージを揃えた後インストールしなおしました．




アップグレード時に一つ問題があったパッケージがあります．それはamavis-newです．アップグレード時に整合性を保つため，使用ディレクトリを全部chownしようとするのですが，その中に膨大な数のspamファイルがあったために，全然処理が終わりませんでした．spamassassinをamavis経由で使っているサーバは，アップグレード時にamavis-newをホールドしておき，余裕を持ってアップグレードしたほうが良いと思います．
