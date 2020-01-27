---
author: fumi
comments: true
date: 2009-02-21 09:20:44+00:00
layout: post
link: https://fumi.me/2009/02/21/beautiful-code/
slug: beautiful-code
title: Beautiful Code ビューティフルコード
wordpress_id: 2172
categories:
- Book
- Programming
tags:
- Book
- Programming
- Review
---

## Beautiful Code

著名なプログラマー達が，自分が今まで出会った中で"美しい"と思っているコードについて述べている本．人によって"美しい"の定義が異なるので，アルゴリズム，テスト，アーキテクチャ，並列処理など，内容が多岐にわたります．




自分が考える美しいコードとは，簡潔で，短く，容易に可読なコードです．本書でも，多くの方々が同様の意見を述べていましたので，抜粋してみました．




<blockquote>

> 
> ロブは，さまざまな選択肢の中から，非常に小さいが，重要であり，うまく定義された，拡張可能な一群の機能を選択したという点で賞賛されるべきです．
> 
> 

> 
> ロブの実装それ自体も，コンパクトでエレガントで，効率的で，実用性があるという点で美しいプログラムの最上の例です．(p.3 Brian Kernighan)
> 
> 
</blockquote>




<blockquote>

> 
> コードを削ることで機能を追加しなさい．(p.40 Jon Bentley)
> 
> 
</blockquote>




<blockquote>

> 
> 美しいコードは，理解が容易でなければいけません．開発者の言語知識をひけらかすために書かれたようなコードは，私は大嫌いですし，あるコードが実際に何をやっているのかを理解するために25行以上コードを読み進む必要があるべきではありません． (p.277 by Adam Kolawa)
> 
> 
</blockquote>




<blockquote>

> 
> 要約すると美しいコードとは，短くて，明確で，質素で，現実を考えて書かれている物だと，私は信じています．(p.282 by Adam Kolawa)
> 
> 
</blockquote>




<blockquote>

> 
> 私はコードをリファクタリングして追加した行数より削除した行数の方が多いとき，いつも得意な気分になります．(p.306 by Diomidis Spinellis)
> 
> 
</blockquote>




<blockquote>

> 
> Pythonを開発していて，最初はいろいろ最適化するのがよいと思ったけれども，結局は比較的素朴な実装の方が好ましい，と気づく場合がありました．要するに物事はシンプルに保っておくことが得な場合が多いのです．(p.310 Andrew Kuchling)
> 
> 
</blockquote>




<blockquote>

> 
> 並列プログラムは非決定的に実行されるため，テストは困難であり，バグはほとんど再現できません．ですから私にとっては，美しいプログラムとは，単に明らかな間違いがないという物ではなく，明らかに間違いがないと一目でわかるような単純でエレガントなプログラムのことを言います(この表現はC.A.R.ホーアによるものです)．(p.405 Simon Peyton Jones)
> 
> 
</blockquote>




<blockquote>

> 
> プログラムの美しさを構成する要素の一つは「簡潔さ」です．Paul Grahamもエッセイで「簡潔さは力なり」と語っています．ですから簡潔に記述できることはプログラミング言語にとって絶対の善なのです． (p.504 by まつもとゆきひろ)
> 
> 
</blockquote>




それぞれ実際に言及している分野はばらばらなのですが，それでもほとんど同じことを言っていると思います．




取り上げられていたアルゴリズムで美しいと思うのはニ分探索 (binary search) です．しかし，これだけ単純で古いアルゴリズムでも，最近まで実装にバグがあったというのには驚きます．"[Extra, Extra - Read All About It: Nearly All Binary Searches and Mergesorts are Broken](http://googleresearch.blogspot.com/2006/06/extra-extra-read-all-about-it-nearly.html) - Google Research Blog"にその詳細が載っています．




    
    <code>
    1:     public static int binarySearch(int[] a, int key) {
    2:         int low = 0;
    3:         int high = a.length - 1;
    4:
    5:         while (low <= high) {
    6:             int mid = (low + high) / 2;
    7:             int midVal = a[mid];
    8:
    9:             if (midVal < key)
    10:                 low = mid + 1
    11:             else if (midVal > key)
    12:                 high = mid - 1;
    13:             else
    14:                 return mid; // key found
    15:         }
    16:         return -(low + 1);  // key not found.
    17:     }
    </code>




上記のコード(元ブログから引用)の6行目 `int mid = (low + high) / 2;`でlow+highが231-1より大きくなるとき，符号が反転してmidがマイナスになります．そのため7行目の配列アクセスで失敗します．これを回避するためには`int mid = (low + high) >>> 1`とすれば良いです．>>>は右シフト演算で符号を落とします．または明示的にunsignedで実装する必要があります．




その他にも，MapReduceなど，色々載っています．通して読むよりは，興味がある章を拾い読みするのが良いかなと思います．





[tmkm-amazon]4873113636[/tmkm-amazon]
