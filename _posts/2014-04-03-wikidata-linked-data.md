---
author: fumi
comments: false
date: 2014-04-03 02:53:57+00:00
layout: post
link: https://fumi.me/2014/04/03/wikidata-linked-data/
slug: wikidata-linked-data
title: Wikidata Linked Data
wordpress_id: 3132
categories:
- LinkedData
tags:
- DBpedia
- LinkedData
- Wikidata
- Wikimedia
- Wikipedia
---

[Wikidata](http://www.wikidata.org/)は[Wikimedia](http://www.wikimedia.org/)のプロジェクトの一つで，人間と機械が同じように参照・編集可能なフリーな知識ベースです．誰もが簡単に構造化データを作れます．WikidataはすでにWikipediaの言語間リンク等に利用されています．

技術的に見ると，WikidataはLinked Dataを基盤としています．まず，[http://ja.wikipedia.org/wiki/森薫](http://ja.wikipedia.org/wiki/森薫)のWikidataページは[http://www.wikidata.org/wiki/Q433255](http://www.wikidata.org/wiki/Q433255)になります．DBpediaと異なり，一つのアイテム毎にユニークなid (Qの後のXXXXX)があり，それに多言語のラベルが付くようになっています．WikipediaとWikidataの対応関係を知るためにはリゾルバがあります．リゾルバのURI設計は`http://www.wikidata.org/wiki/Special:ItemByTitle/{site}/{title}`です．森薫の例だと，[http://www.wikidata.org/wiki/Special:ItemByTitle/jawiki/森薫](https://www.wikidata.org/wiki/Special:ItemByTitle/jawiki/森薫)となります．


一方で，アイテム自体を識別するためのURIはhttp://www.wikidata.org/entity/Q{id}となっています．Q433255を識別するためのURIは[http://www.wikidata.org/entity/Q433255](http://www.wikidata.org/entity/Q433255)です．Linked DataとしてのURI設計は以下の通りになります．connegはhttp,https両方受け付けるみたい．

* Item URI: http://www.wikidata.org/entity/Q{id}
* データURI: http://www.wikidata.org/wiki/Special:EntityData/Q{id}
* HTMLページ URI: http://www.wikidata.org/wiki/Q{id}
* JSON URI: http://www.wikidata.org/wiki/Special:EntityData/Q{id}.json
* Turtle URI: http://www.wikidata.org/wiki/Special:EntityData/Q{id}.ttl
* RDF/XML URI: http://www.wikidata.org/wiki/Special:EntityData/Q{id}.rdf
* N-Triples URI: http://www.wikidata.org/wiki/Special:EntityData/Q{id}.nt


```turtle
$ curl -LH 'Accept: text/turtle' http://www.wikidata.org/entity/Q433255
@prefix data: <http://www.wikidata.org/wiki/Special:EntityData/> .
@prefix schema: <http://schema.org/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
@prefix entity: <http://www.wikidata.org/entity/> .
@prefix cc: <http://creativecommons.org/ns#> .
@prefix wikibase: <http://www.wikidata.org/ontology#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix skos: <http://www.w3.org/2004/02/skos/core#> .

data:Q433255
  schema:version 103373967 ;
  schema:dateModified "2014-01-19T13:20:45Z"^^xsd:dateTime ;
  a schema:Dataset ;
  schema:about entity:Q433255 ;
  cc:license <http://creativecommons.org/publicdomain/zero/1.0/> .

entity:Q433255
  a wikibase:Item ;
  rdfs:label "森薰"@zh-hans, "森薰"@zh-hant, "森薰"@zh-hk, "森薰"@zh-cn, "森薰"@zh-sg, "森薰"@zh-tw, "Kaoru Mori"@de, "森薫"@ja, "Kaoru Mori"@fr, "Мори, Каору"@ru, "모리 카오루"@ko, "Kaoru Mori"@en, "Kaoru Mori"@sv, "Kaoru Mori"@nl, "Kaoru Mori"@es, "Kaoru Mori"@pl, "森薰,"@zh ;
  skos:prefLabel "森薰"@zh-hans, "森薰"@zh-hant, "森薰"@zh-hk, "森薰"@zh-cn, "森薰"@zh-sg, "森薰"@zh-tw, "Kaoru Mori"@de, "森薫"@ja, "Kaoru Mori"@fr, "Мори, Каору"@ru, "모리 카오루"@ko, "Kaoru Mori"@en, "Kaoru Mori"@sv, "Kaoru Mori"@nl, "Kaoru Mori"@es, "Kaoru Mori"@pl, "森薰,"@zh ;
  schema:name "森薰"@zh-hans, "森薰"@zh-hant, "森薰"@zh-hk, "森薰"@zh-cn, "森薰"@zh-sg, "森薰"@zh-tw, "Kaoru Mori"@de, "森薫"@ja, "Kaoru Mori"@fr, "Мори, Каору"@ru, "모리 카오루"@ko, "Kaoru Mori"@en, "Kaoru Mori"@sv, "Kaoru Mori"@nl, "Kaoru Mori"@es, "Kaoru Mori"@pl, "森薰,"@zh ;
  schema:description "japanische Manga-Zeichnerin"@de, "japońska mangaka"@pl ;
  skos:altLabel "森薫"@zh, "Mori Kaoru"@de, "森薫"@de, "県文緒"@ja, "森薫"@fr, "Mori Kaoru"@fr, "Fumio Agata"@fr, "Agata Fumio"@fr, "県文緒"@fr, "Мори Каору"@ru, "Каору Мори"@ru, "모리 가오루"@ko, "Mori"@sv .

<http://zh.wikipedia.org/wiki/%E6%A3%AE%E8%96%B0>
  a schema:Article ;
  schema:about entity:Q433255 ;
  schema:inLanguage "zh" .
....
```

### 参考
  * [Wikidata/Notes/URI scheme](http://meta.wikimedia.org/wiki/Wikidata/Notes/URI_scheme)
  * [Wikidata/Notes/Data model primer](http://meta.wikimedia.org/wiki/Wikidata/Notes/Data_model_primer)
  * [Wikidata/Data model](http://meta.wikimedia.org/wiki/Wikidata/Data_model)
  * [Wikidata/Development/RDF](http://meta.wikimedia.org/wiki/Wikidata/Development/RDF)
  * [Wikidata/Notes/DBpedia and Wikidata](http://meta.wikimedia.org/wiki/Wikidata/Essays/DBpedia_and_Wikidata)
