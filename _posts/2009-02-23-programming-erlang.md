---
author: fumi
comments: true
date: 2009-02-23 10:01:41+00:00
layout: post
link: https://fumi.me/2009/02/23/programming-erlang/
slug: programming-erlang
title: プログラミング Erlang
wordpress_id: 2181
categories:
- Book
- Programming
tags:
- Book
- Erlang
- Programming
- Review
---

## プログラミング Erlang







Erlangの作者 Joe Armstrongが書いた本の翻訳本を読みました．マルチコアなプロセッサや分散環境が手軽に使える時代なので，平行指向かつ分散指向なプログラミング言語である Erlangは気になっていました．ロックによる状態共有のプログラミングは皆が正しく行うには難しいので，プログラミング言語としてサポートするのは正しいと思うのです．今すぐ使うわけではないので，簡単な逐次実行から並列処理のサンプルを試しただけですが，新しい言語を学ぶのは楽しいですね．文法部分にPrologの影響を受けた関数型言語という感じです．




束縛した変数が不変で，かつプロセス間メッセージパッシングで処理を行うモデルなので，状態の共有はほとんどありません．そのため，安全に平行処理ができるというのがウリです．サーバーを書くには向いていると思います．文字列はただの数字の配列という扱いなので，文字列処理には向いていなさそうです．[Erlang Tips](http://www.mikage.to/erlang/)を見ると正規表現ライブラリもあるようですが，試してはいません．





[tmkm-amazon]4274067149[/tmkm-amazon]
