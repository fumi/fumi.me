---
author: fumi
comments: true
date: 2008-08-24 13:36:47+00:00
layout: post
link: https://fumi.me/2008/08/24/eeeubuntu-fs/
slug: eeeubuntu-fs
title: eeeUbuntu - (2) ファイルシステム,キャッシュ
wordpress_id: 194
categories:
- EeePC
- Ubuntu
tags:
- EeePC
- eeeUbuntu
- Firefox
- tmpfs
- Ubuntu
---

パフォーマンス向上とSSD書込を減らす努力をします。まず、/var/log,/var/tmp,/tmpはtmpfs (RAMDISK) にしておきます。この用途だと昔のlogは見ないでしょうし。また、他のパーティションを、relatimeからnoatimeに変更して、ファイル読込時間を書き込まないようにします。但し、/homeだけはrelatimeにしたほうが、muttのようにatimeを見るアプリケーションを使う場合には良いようです。最近のカーネルはrelatimeがデフォルトらしいですね。/var/log, /var/tmp,/tmpの中身は、再起動する前に消しておきます。そうしないとディスクに残ったままになりますので。



    
    <code>
    $ sudo vi /etc/fstab
    ....
    UUID=xxxxxxxxxxxxx  / ext2 noatime,errors=remount-ro 0 1
    UUID=xxxxxxxxxxxxx /usr ext2 noatime 0 2
    tmpfs /var/log tmpfs defaults,noatime 0 0
    tmpfs /var/tmp tmpfs defaults,noatime 0 0
    tmpfs /tmp tmpfs defaults,noatime 0 0
    </code>





aptでインストールする際に、ディレクトリがないと文句を言われるので、rc.localのexit 0 の前にmkdir -p /var/log/aptを追加しておきます。




    
    <code>
    $ sudo vi /etc/rc.local
    ....
    mkdir -p /var/log/apt
    exit 0
    </code>





次に、Firefoxのキャッシュを/tmpに書くようにします。一度Firefoxを起動後に、.mozilla/firefox/xxx.defaults/user.jsを作成します。


`
user_pref("browser.cache.disk.parent_directory","/tmp/firefox");
`
