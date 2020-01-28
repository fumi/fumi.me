---
author: fumi
comments: false
date: 2012-05-12 09:18:53+00:00
layout: post
link: https://fumi.me/2012/05/12/microdata/
slug: microdata
title: Microdata&Schema.org @ニコニコ学会βシンポジウム研究マッドネス
wordpress_id: 3029
categories:
- LinkedData
- Microdata
- Web
tags:
- Microdata
- SPARQL
- ニコニコ学会
---

先日2012年4月28-29日にニコニコ超会議にてニコニコ学会βが開催されました．ニコニコ学会βの中で野生の研究者に発表してもらう研究マッドネスというセッションがあり，その研究を公募するサイトを担当しました．ただ作るだけでは面白くなかったので，裏でMicrodataとSchema.orgのテストをすることにしました (参考: [当時のGoogle+](https://plus.google.com/111432057975328893801/posts/R2mHmfvEN5A))．

例えば，メカの部で賞を取った電子楽器ウダーのページのソース抜粋は以下のようになっています．





```html
<div class='entry' id='work' itemid='http://nicores.herokuapp.com/entry/10#work' itemscope='itemscope' itemtype='http://schema.org/CreativeWork'>
  (...snip...)
  <h2><span class='hashtag'>#マッドネス10</span>「<span class='title' itemprop='name'>電子楽器ウダー</span>」</h2>
  <h3><span class='author' id='person' itemid='http://nicores.herokuapp.com/entry/10#person' itemprop='author' itemscope='itemscope' itemtype='http://schema.org/Person'>発表者:<a href='http://twitter.com/uda807'><span itemprop='name'>宇田道信</span></a></span> (<span itemprop="genre">メカ</span>の部希望)</h3>
  <div class='video'><script type="text/javascript" src="http://ext.nicovideo.jp/thumb_watch/sm14918619?w=490&h;=307" itemprop="url"></script></div>
  <p class='description' itemprop='description'>ウダーは個人で開発している電子楽器です。電子楽器ではありますが、操作は非常にシンプルです。　
  (...snip...)  
```    

これをMicrodata等からRDFを抽出する[RDF Distiller](http://rdf.greggkellogg.net/distiller)に掛けると以下のキャプチャのようになります．

{% include image.html url="/images/2012-05-12-microdata/b6a7d7de297f3e6684141e18c21f9023-1024x648.png" description="result of RDF Distiller" %}

また，[Google Rich Snippets Testing Tool](http://www.google.com/webmasters/tools/richsnippets)に通すとこんな感じ．

{% include image.html url="/images/2012-05-12-microdata/8b5c47232ab78cf39d327f53d8ca8f51.png" description="the result of Rich Snippets Testing Tool" %}

今見なおすと動画のurlが取れていないみたいですが，Microdataの仕様を読むとscript要素は対象外なんですね．当時は取れていたきがするけど．

更に，これらのデータをRDF Distillerを通して，データクラウドサービスである[Dydra](http://dydra.com)に取り込みました．公開レポジトリは[fumi/nicores](http://dydra.com/fumi/nicores)です．色々クエリが書けて便利．
