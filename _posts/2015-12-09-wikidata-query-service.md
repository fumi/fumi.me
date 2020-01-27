---
author: fumi
comments: true
date: 2015-12-09 08:26:44+00:00
layout: post
link: https://fumi.me/2015/12/09/wikidata-query-service/
slug: wikidata-query-service
title: Wikidata Query Service
wordpress_id: 3269
categories:
- LinkedData
- SPARQL
- Web
tags:
- Linked Data
- SPARQL
- Wikidata
---

これは [SPARQL Advent Calendar 2015](http://qiita.com/advent-calendar/2015/sparql) 9日目の記事です．





以前[Wikidata Linked Dataという記事](http://fumi.me/2014/04/03/wikidata-linked-data/)を書いた通り，Wikidata のデータ提供部分はLinked Dataです．これまでもサードパーティがそのRDFで勝手SPARQLエンドポイントを立てていたりしたのですが，今年9月にWikimediaが公式に[Wikidata Query Service](https://query.wikidata.org)というSPARQLエンドポイントをβ公開しました．今回はこれを使ってみようとおもいます．




サンプル例にアメリカ歴代大統領というのがあったので，試しに歴代の内閣総理大臣を開始年でソートするクエリを書いてみました([SPARQL例へのリンク](http://tinyurl.com/z4q6g5q))．



    
    <code>PREFIX wikibase: <http://wikiba.se/ontology#>
    PREFIX wd: <http://www.wikidata.org/entity/> 
    PREFIX wdt: <http://www.wikidata.org/prop/direct/>
    PREFIX rdfs: <http://www.w3.org/2000/01/rdf-schema#>
    PREFIX p: <http://www.wikidata.org/prop/>
    PREFIX ps: <http://www.wikidata.org/prop/statement/>
    PREFIX psv: <http://www.wikidata.org/prop/statement/value/>
    PREFIX pq: <http://www.wikidata.org/prop/qualifier/>
    PREFIX pqv: <http://www.wikidata.org/prop/qualifier/value/>
    
    SELECT ?primeMinister ?primeMinisterLabel ?startTime
    WHERE {
       ?primeMinister p:P39 ?positionStatement .
       ?positionStatement ps:P39 wd:Q274948 ; 
                          pq:P580 ?startTime .
      
       SERVICE wikibase:label {
          bd:serviceParam wikibase:language "ja,en" .
       }
     }
    ORDER BY ?startTime
    </code>





結果は45件で，データとしてはかなり欠けています．明治・大正時代の人が全然いませんし，近年をみても麻生太郎と鳩山由紀夫が入っていません．皆で日本に関するデータを整備していく必要があります．





Wikidataのデータは多言語化前提になっていて，全てのリソースにIDベースのIRIが振られていて，そのIRIに対して多言語によるラベルを付与するというモデルになっています．そのため，リソースによってラベルがある言語がバラバラになるので，言語指定のフォールバックができる仕組みをSPARQLを拡張して用意しています．上記のクエリの`SERVICE wikibase:label { ... }`の部分がそれです．`bd:serviceParam wikibase:language  "言語名"`の言語名の部分に複数の言語を指定すると，その順番でラベルを使用します．例えば"ja,en"であれば日本語が主で，日本語がない場合は英語を取得します．指定した言語がない場合はリソースのIRIになります．SELECTで指定する変数として，実際にラベルを取得したい変数の最後に"Label"を付けたものを指定することで，自動的にラベルを取得できます．上記例では，?president 変数のラベルとして?presidentLabelを指定しています．




この自動ラベル変換機能は一々言語毎にFILTERをするといった複雑なことをしなくて済むので便利ですが，いくつか制約があります．まず，OPTIONALで使っている変数は現在エラーになるようです(これはバグかもしれません)．また，ラベルの中身に応じてフィルターしたいときのように，クエリ内で変数を参照したいときには使えません．その場合は，SERVICE句の中で直接rdfs:labelでラベル変数を指定すれば良いです．但し，自動変換機能と併用することはできないので，必要なラベルを全て指定する必要があります．




Wikidataまだまだこれからですが，色んなエンティティを結びつけるデータとしてどんどん整理されつつあるので，揃ってくればかなり期待できるサービスだとおもいます．





参考: 






  * [User Manual](https://www.mediawiki.org/wiki/Wikidata_query_service/User_Manual)


  * [ Wikibase/Indexing/SPARQL Query Examples


  * [SPARQL queryservice/queries](Wikidata:SPARQL query service/queries)


