---
author: fumi
comments: false
date: 2014-08-08 06:18:54+00:00
layout: post
link: https://fumi.me/2014/08/08/code-point/
slug: code-point
title: Code-Point Open Linked Data - OS Linked Data
wordpress_id: 3148
categories:
- LinkedData
- OpenData
- SPARQL
tags:
- Linked Data
- Open Data
- Open Government
---

[OS Linked Data](http://fumi.me/2014/08/05/50k-gazetteer/)の続きです．今回は[Code-Point Open Linked Data](http://data.ordnancesurvey.co.uk/datasets/code-point-open)について．[Code-Point](http://www.ordnancesurvey.co.uk/business-and-government/products/code-point.html)はイギリスの郵便番号(Postcode)に関するデータですが，基本的な項目を[Code-Point Open](http://www.ordnancesurvey.co.uk/business-and-government/products/code-point-open.html)でオープンデータとして公開しています．詳細なデータを使うには別途メンバーシップ契約が必要です([How to buy](http://www.ordnancesurvey.co.uk/business-and-government/help-and-support/products/how-to-buy.html), 実際の手続きはやったことないので不明)．Code-Point Open Linked DataはCode-Point Openの部分についてLinked Dataにしています．

フォームでは郵便番号文字列の検索ができます．例えば"EC2A"で検索すると，EC2Aを含んだ郵便番号が返ってきます．

{% include image.html url="/images/2014-08-08-code-point/Code-Point_Open_Linked_Data.png" description="EC2Aの検索結果" %}

地名と同様に，郵便番号もURIで識別されます．EC2AのURIは[http://data.ordnancesurvey.co.uk/id/postcodedistrict/EC2A](http://data.ordnancesurvey.co.uk/id/postcodedistrict/EC2A)です．Webブラウザで見ると以下のようになります．


{% include image.html url="/images/2014-08-08-code-point/EC2A.png" description="EC2A" %}

text/turtleを要求すると以下のような結果が返ってきます．

```turtle
% curl -LH 'Accept: text/turtle' http://data.ordnancesurvey.co.uk/id/pozstcodedistrict/EC2A
@prefix rdfs:  <http://www.w3.org/2000/01/rdf-schema#> .
@prefix foaf:  <http://xmlns.com/foaf/0.1/> .
@prefix dct:   <http://purl.org/dc/terms/> .
@prefix rdf:   <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .

<http://data.ordnancesurvey.co.uk/ontology/postcode/PostcodeDistrict>
        rdfs:label  "Postcode District"^^<http://www.w3.org/2001/XMLSchema#string> .

<http://data.ordnancesurvey.co.uk/id/postcodearea/EC>
        rdfs:label  "EC" .

<http://data.ordnancesurvey.co.uk/id/postcodesector/EC2A3>
        rdfs:label  "EC2A 3" .

<http://data.ordnancesurvey.co.uk/doc/postcodedistrict/EC2A>
        a foaf:Document ;
        rdfs:seeAlso <http://sameas.org/rdf?uri=http://data.ordnancesurvey.co.uk/id/postcodedistrict/EC2A> ;
        dct:title    "Description of http://data.ordnancesurvey.co.uk/id/postcodedistrict/EC2A" ;
        foaf:primaryTopic  <http://data.ordnancesurvey.co.uk/id/postcodedistrict/EC2A> .

<http://data.ordnancesurvey.co.uk/id/postcodesector/EC2A1>
        rdfs:label  "EC2A 1" .

<http://data.ordnancesurvey.co.uk/id/postcodesector/EC2A4>
        rdfs:label  "EC2A 4" .

<http://data.ordnancesurvey.co.uk/id/postcodesector/EC2A2>
        rdfs:label  "EC2A 2" .

<http://data.ordnancesurvey.co.uk/id/postcodedistrict/EC2A>
        a <http://data.ordnancesurvey.co.uk/ontology/postcode/PostcodeDistrict> ;
        rdfs:label  "EC2A" ;
        <http://data.ordnancesurvey.co.uk/ontology/spatialrelations/contains>
                <http://data.ordnancesurvey.co.uk/id/postcodesector/EC2A4> , <http://data.ordnancesurvey.co.uk/id/postcodesector/EC2A3> , <http://data.ordnancesurvey.co.uk/id/postcodesector/EC2A2> , <http://data.ordnancesurvey.co.uk/id/postcodesector/EC2A1> ;
        <http://data.ordnancesurvey.co.uk/ontology/spatialrelations/within>
                <http://data.ordnancesurvey.co.uk/id/postcodearea/EC> .
```

ここで面白いのは，イギリスの郵便番号の記法には体系があって，その包含関係がデータとして記述されています．具体的には`http://data.ordnancesurvey.co.uk/ontology/spatialrelations/within`と`http://data.ordnancesurvey.co.uk/ontology/spatialrelations/contains`という二つのプロパティを使ってその関係を記述しています．地域によって桁数等は異なりますが，全体として必ず4階層になるようになっています．以下はOpen Data Instituteの郵便番号である EC2A 4DJ の例です．左の青丸が郵便番号のリソースで，右の茶丸は属するクラスです．図を簡略化するためにURIは省いてあります．


{% include image.html url="/images/2014-08-08-code-point/OS-Linked-Data.png" description="Postcode Model" %}

一番下のPostcodeUnitが実際に使われている郵便番号に相当します．[http://data.ordnancesurvey.co.uk/id/postcodeunit/EC2A4JE](http://data.ordnancesurvey.co.uk/id/postcodeunit/EC2A4JE)を見ると，PostcodeUnitのデータには行政区や統計上の区分との関係が記述されるようになっています．これは別エントリで書きます．

{% include image.html url="/images/2014-08-08-code-point/EC2A_4JE.png" description="EC2A 4JE" %}
