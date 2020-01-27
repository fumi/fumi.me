---
author: fumi
comments: true
date: 2009-01-21 11:52:48+00:00
layout: post
link: https://fumi.me/2009/01/21/evernote-on-ubuntu/
slug: evernote-on-ubuntu
title: Evernote on Ubuntu
wordpress_id: 598
categories:
- Software
- Ubuntu
tags:
- EverNote
- Software
- Ubuntu
- Wine
---

[![evernote-ubuntu](http://fumi.me/wp-content/uploads/2009/01/evernote-ubuntu-300x241.png)](http://fumi.me/wp-content/uploads/2009/01/evernote-ubuntu.png)[WineHQのEvernoteの項目](http://appdb.winehq.org/objectManager.php?sClass=application&iId=2566)にはある程度動くと書かれているので，前から試してみたいと思っていましたので，今回やってみました．結論から言うと，日本語表示・入力共に可能ですが，速度が実用的ではないです．今動かしているマシンはCore 2 Duo E8500+4GB memoryですが，動作がもっさりしています．




まず，最新のWineをインストールします．WineHQにはUbuntu8.10用のapt lineが用意されていますので，/etc/apt/sources.listに以下の行を追加します．



    
    <kbd>
    deb http://wine.budgetdedicated.com/apt intrepid main 
    </kbd>




次に，aptのための公開鍵を取得し，Synaptic Package Managerの認証/AuthenticationからImportします．その後にwineをインストールすればOKです．wineのバージョンは1.1.13~winehq0~ubuntu~8.10-0ubuntu1でした．




この状態で[Evernote](http://evernote.com)のWindows用インストーラをダウンロードし，ダウンロードしたディレクトリで$ wine Everenoteとコマンド打つと，インストールが始まります．特別な要求がなければデフォルト設定で大丈夫です．インストール終了後，$ wine "C:\Program Files\Evernote\Evernote3\Evernote"と入力することで起動できます．




しかしこの状態では日本語が表示できません．そこで[WineLocale](http://cinnamonpirate.com/hobbies/software/winelocale/)をインストールします．詳しい説明は[HOWTO: CJK in Wine (Chinese, Japanese & Korean) - Ubuntu Forums](http://ubuntuforums.org/showthread.php?t=383628)に書かれていますが，既に日本語環境が設定されている場合はwinelocaleの設定だけ行えば使えます．まず，[winelocale](http://www.cinnamonpirate.com/software/winelocale/)よりwineloc-0.41.tar.gzを取得し，インストールします．



    
    <kbd>
    $ wget http://www.cinnamonpirate.com/pub/software/sh/wineloc-0.41.tar.gz
    $ tar xvzf wineloc-0.41.tar.gz
    $ cd wineloc-0.41
    $ ./install
    </kbd>




デフォルトの設定でEvernoteをインストールした場合，その実行ファイルはHOMEディレクトリの.wineの中にインストールされているはずです．そのため，以下のようなコマンドを入力することで，日本語表示可能なEvernoteが起動できます．/home/userの部分を環境に合わせて変更してください．/p>

    
    <kbd>
    $ wineloc -l ja_JP -f common
        /home/user/.wine/drive_c/Program Files/Evernote/Evernote3/Evernote.exe
    </kbd>




日本語入力に関しては，SCIMを使っている限りでは何も設定なしで使えました．これはXIMなどの場合は問題になるかもしれません




また，winelocの作者が最近[Google Code](http://code.google.com/p/winelocale/)にソースを移して開発を再開しているのですが，何故か日本語の設定が削られていたので動きませんでした．問題がわかればコミットしようと思います．
