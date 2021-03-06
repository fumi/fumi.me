---
author: fumi
comments: false
date: 2010-01-31 12:09:12+00:00
layout: post
link: https://fumi.me/2010/01/31/sharkspace/
slug: sharkspace
title: SharkSpaceに移転
wordpress_id: 2830
categories:
- WordPress
tags:
- Hosting
- SharkSpace
- WordPress
---

当サイトをSharkSpaceというホスティングサービスに移転完了しました．

さくらインターネットのスタンダードを今まで使っていましたが，色々問題がありました．まず，重かったです．特に管理画面が重く，いつまで待っても編集できないということが良くあったため，更新するのが億劫になっていました．また，自分がさくらを使い始めたときにはMySQL4.0.xしかなかったのですが，WordPress2.9からMySQL4.0をサポートしなくなったので，アップグレードできずにいました．現在さくらでもMySQL5.0.xが使えるのですが，どちらにしろ移行作業をしないといけないので，移転先を探していました．私が望んでいた要件は以下の通りです．

1. ssh
2. WordPressの速度
3. MySQL5
4. 容量 (Disk･転送)
5. 価格

1. のsshがなかなか厳しい条件です．何故か未だにsshを提供しない，または条件付きのホスティングサービスが多いのです．sshでアクセスするのは基本だと思うのですが，この条件でかなり選択肢が減ります．国内で且つ低価格でsshを提供するのはさくらかxrea系列くらいです．また，4. Disk容量については，さくらスタンダードの3GBでは足りなかったのと，月の転送量が10GBを越えてきたので，それを余裕を持って上回るものを探す必要がありました．

この条件で探すと国内では割高なので，海外のホスティングサービスを中心に探していました．その中で，安定した評判を得ていたのはBlueHost系列 ([BlueHost](http://www.bluehost.com/), [HostMonster](http://www.hostmonster.com/), [FastDomain](http://hosting.fastdomain.com/))でした．値段も6-7USD/monthからと，そこそこです．sshを使うには，アカウント作成後にPhoto ID (パスポートなど)を登録する必要があるというのが面倒ですが，それ以外は良さそうでした．

試しにHostMonsterとかを使ってみようかと思っていたところで，SharkSpaceという，聞いたことのないホスティングサービスを推薦しているサイトを見つけました([海外サーバーコレがイチばん!](http://kore1server.com/))．読んでみるとなかなか良さそうなことが書いてあるので，海外のホスティングサービスフォーラムとかも見てみたところ，確かに地味に評判が良さそうでした．個人的にはsshがPhoto IDなしでいけそうだというところと，値段が安いことに惹かれて，使ってみることにしました．

値段は，真ん中のHammerheadコースの2年契約だと7.95USD/月(190.80USD/2年)なんですが，50%offクーポン(クーポンコード: **50offlife**)があるので，3.975USD/月(95.4USD/2年)になります．今1USD=90JPYなので，大体360円/月です．これは安い．これでDisk容量が20GB，データ転送が500GBあります．PHPもモジュールで動きます．さくらのようにCGIモードではありません．

契約してわかったことですが，残念ながらsshを使うにはやはりPhoto IDが必要でした．仕方がないのでiPhoneでIDを写真に撮って，手続きしました．5分程ほどでsshアクセスできるようにしてくれたので，応対は良いですね．

今のところ，不満点はPhoto IDだけで，それ以外はかなり快適に使っています．まだcronで動かしているスクリプトがあるのでしばらくさくらも使いますが，少しずつ移していこうと思っています．

以下は参考サイトです．実際のMySQLの移転作業については別途まとめます．

* [海外サーバーコレがイチばん!](http://kore1server.com/)
* [レンタルサーバはSharkSpaceに決めました](http://waviaei.com/2009/12/21/i-am-going-to-use-sharkspace/)
