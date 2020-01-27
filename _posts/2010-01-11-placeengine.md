---
author: fumi
comments: false
date: 2010-01-11 14:55:55+00:00
layout: post
link: https://fumi.me/2010/01/11/placeengine/
slug: placeengine
title: PlaceEngineをActionScriptから使用
wordpress_id: 2818
categories:
- Flex
- Programming
tags:
- ActionScript
- Flex
- PlaceEngine
- Programming
---

"[新しい扉 PlaceEngine ActionScript API公開](http://v12engine.blog116.fc2.com/blog-entry-12.html)"という記事で，ActionScript用のAPIソースが公開されていたので，それをベースに[PlaceEngine](http://www.placeengine.com/)をActionScriptから使ってみました．とりあえず，PlaceEngineのローカルDBを用いて緯度経度を取得することはできるようです．




まず，PlaceEngineを[サイトからダウンロード](http://www.placeengine.com/)してインストールします．起動後に，環境設定→ローカルDB→アップデートをします．WifiをOnにした状態で"現在地を取得"を押すと，登録されている位置が取得できるはずです．取得できない場合は[PlaceEngine.com Map](http://www.placeengine.com/map)から追加してください．




ActionScriptからローカルDBを使うには以下のようにします．






  1. [PlaceEngine連携サイト用アプリケーションキー取得ページ](http://www.placeengine.com/appk)で以下の情報を入力してアプリケーションキーを生成
  
  
    * 認証コード: 表示されているcaptureを入力

  
    * URL: app:/アプリケーション名.swf (helloというアプリならapp:/hello.swf)

  
    * サービス名: アプリケーション名

  



  2. PlaceEngineAPI.asをプロジェクトの適切な場所に置く．デフォルトパッケージ名はPlaceEngineAPIになっているので適宜変える．

  3. PlaceEngineAPIに以下を追加
  
    
    
    		public function getLocationFromLocal():void{
    			printMsg("WiFi情報取得中...");
    			//タイムスタンプとして現在時刻を取得
    			timeStamp = new Date();
    	
    			//URL文字列を作成
    			var URL:String = "http://localhost:5448/locdb?t=";
    				URL += timeStamp.milliseconds + "&appk;=";
    				URL += appk;
    			trace("URL: " + URL);
    			var request:URLRequest = new URLRequest(URL);
    			var loader:URLLoader = new URLLoader();
    			
    			//イベントハンドラをセット
    			setListeners(loader, "Server");
    			
    			//実際にリクエストを発行
    			sendRequest(loader, request);
    		}
    





  4. プログラム側からはgetLocationの代わりにgetLocationFromLocalを使う




以上の手順で動くことは確認しました．苦労したのは，正しいアプリケーションキーの取得方法がなかなかわからなかったことです．




getLocation がうまく動かないためWebAPIから直接取得できないのですが，原因はcrossdomain.xmlにあるようです．どうやらcrossdomain.xmlの内容が古いらしく，以下のエラーを吐きます．サーバ側で対応してもらえるように，後で連絡する予定です．




<blockquote>

> 
> Warning: Domain www.placeengine.com does not specify a meta-policy.  Applying default meta-policy 'master-only'.  This configuration is deprecated.  See http://www.adobe.com/go/strict_policy_files to fix this problem.
> 
> 

> 
> Error: Ignoring policy file at http://www.placeengine.com/api/crossdomain.xml due to meta-policy 'master-only'.
> 
> 
</blockquote>
