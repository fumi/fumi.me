---
author: fumi
comments: false
date: 2010-03-22 08:33:12+00:00
layout: post
link: https://fumi.me/2010/03/22/placeengine-2/
slug: placeengine-2
title: PlaceEngine in ActionScript その後
wordpress_id: 2872
categories:
- Flex
tags:
- ActionScript
- Flex
- PlaceEngine
---

以前[PlaceEngineをActionScriptからうまく使えない](http://fumi.me/2010/01/11/placeengine/)と書いたのですが，その後クウジット社の人とやりとりして，最終的に動くのを確認しました．問題は2点あったようです．1点はサーバ側の問題だったようで，修正したという連絡がありました．もう1つはcrossdomain.xmlの場所が異なっていたようです．以下のようにPlaceEngineAPI.asを直せば良いです．



    
    <code>
           //サーバアクセスに先立って、crossdomain.xmlの場所を指定
    -     Security.loadPolicyFile("http://www.placeengine.com/api/crossdomain.xml");
    +    Security.loadPolicyFile("http://www.placeengine.com/crossdomain.xml");
    </code>




この修正後，ActionScriptからも住所を取得できるのを確認できました．クウジット社の方々にはこの場を借りてお礼申し上げます．
