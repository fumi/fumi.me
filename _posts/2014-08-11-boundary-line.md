---
author: fumi
comments: false
date: 2014-08-11 09:01:30+00:00
layout: post
link: https://fumi.me/2014/08/11/boundary-line/
slug: boundary-line
title: Boundary-Line Linked Data - OS Linked Data
wordpress_id: 3156
categories:
- LinkedData
- OpenData
tags:
- Linked Data
- Open Data
- Open Government
---

以前のOS Linked Dataについての記事．

  * [50K Gazetteer Linked Data](/2014/08/05/50k-gazetteer/)
  * [Code-Point Open Linked Data](/2014/08/08/code-point/)

郵便番号[EC2A 4JE](http://data.ordnancesurvey.co.uk/doc/postcodeunit/EC2A4JE)のデータを見ると，その郵便番号がある行政区画へのリンクがあります．

{% include image.html url="/images/2014-08-11-boundary-line/EC2A_4JE1.png" description="EC2A 4JEの行政区画" %}

[Ward: Haggerston](http://data.ordnancesurvey.co.uk/id/7000000000011110)を見てみると，行政区画についてのデータとその境界線の表示をしてくれます．

{% include image.html url="/images/2014-08-11-boundary-line/Haggerston.png" description="Haggerston" %}

```    
% curl -LH 'Accept: text/turtle' http://data.ordnancesurvey.co.uk/id/7000000000011110
.......
<http://data.ordnancesurvey.co.uk/id/7000000000011110>
        a           <http://data.ordnancesurvey.co.uk/ontology/admingeo/LondonBoroughWard> ;
        rdfs:label  "Haggerston" ;
        <http://data.ordnancesurvey.co.uk/ontology/admingeo/gssCode>
                "E05000239" ;
        <http://data.ordnancesurvey.co.uk/ontology/admingeo/hasAreaCode>
                "LBW" ;
        <http://data.ordnancesurvey.co.uk/ontology/admingeo/hasUnitID>
                "11110" ;
        <http://data.ordnancesurvey.co.uk/ontology/admingeo/inCounty>
                <http://data.ordnancesurvey.co.uk/id/7000000000041441> ;
        <http://data.ordnancesurvey.co.uk/ontology/admingeo/inDistrict>
                <http://data.ordnancesurvey.co.uk/id/7000000000011199> ;
        <http://data.ordnancesurvey.co.uk/ontology/admingeo/inEuropeanRegion>
                <http://data.ordnancesurvey.co.uk/id/7000000000041428> ;
        <http://data.ordnancesurvey.co.uk/ontology/geometry/extent>
                <http://data.ordnancesurvey.co.uk/id/geometry/11110-241> ;
        <http://data.ordnancesurvey.co.uk/ontology/spatialrelations/easting>
                533455.5 ;
        <http://data.ordnancesurvey.co.uk/ontology/spatialrelations/northing>
              "182927"^^<http://www.w3.org/2001/XMLSchema#decimal> ;
        <http://data.ordnancesurvey.co.uk/ontology/spatialrelations/touches>
                <http://data.ordnancesurvey.co.uk/id/7000000000011193> , <http://data.ordnancesurvey.co.uk/id/7000000000041879> , <http://data.ordnancesurvey.co.uk/id/7000000000010856> , <http://data.ordnancesurvey.co.uk/id/7000000000010854> , <http://data.ordnancesurvey.co.uk/id/7000000000010855> , <http://data.ordnancesurvey.co.uk/id/7000000000011112> , <http://data.ordnancesurvey.co.uk/id/7000000000011196> , <http://data.ordnancesurvey.co.uk/id/7000000000011111> ;
        <http://data.ordnancesurvey.co.uk/ontology/spatialrelations/within>
                <http://data.ordnancesurvey.co.uk/id/7000000000011199> ;
        <http://www.georss.org/georss/point>
                "51.529489 -0.07749" ;
        <http://www.w3.org/2002/07/owl#sameAs>
                <http://statistics.data.gov.uk/id/statistical-geography/E05000239> ;
        <http://www.w3.org/2003/01/geo/wgs84_pos#lat>
                51.529489 ;
        <http://www.w3.org/2003/01/geo/wgs84_pos#long>
                -0.07749 ;
        <http://www.w3.org/2004/02/skos/core#prefLabel>
                "Haggerston" .
```

データで使われている語彙のURIが長いので以下のprefixで省略して書きます．

```    
@prefix geometry: <http://data.ordnancesurvey.co.uk/ontology/geometry/>
@prefix spatialrelations: <http://data.ordnancesurvey.co.uk/ontology/spatialrelations/>
@prefix admingeo: <http://data.ordnancesurvey.co.uk/ontology/admingeo/>
```

境界線データはgeometry:extentの<http://data.ordnancesurvey.co.uk/id/geometry/11110-241>に含まれています．GMLが直接埋め込んである形になっています．

```
% curl -LH 'Accept: text/turtle' http://data.ordnancesurvey.co.uk/id/geometry/11110-241
@prefix rdfs:  <http://www.w3.org/2000/01/rdf-schema#> .
@prefix foaf:  <http://xmlns.com/foaf/0.1/> .
@prefix dct:   <http://purl.org/dc/terms/> .
@prefix rdf:   <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .

<http://data.ordnancesurvey.co.uk/id/geometry/11110-241>
        a       <http://data.ordnancesurvey.co.uk/ontology/geometry/AbstractGeometry> ;
        <http://data.ordnancesurvey.co.uk/ontology/geometry/asGML>
                "<gml:Polygon xmlns:gml=\"http://www.opengis.net/gml\" srsName=\"http://www.opengis.net/def/crs/EPSG/0/27700\"><gml:exterior><gml:LinearRing><gml:posList srsDimension=\"2\">533259.9 183282.5 533263 183333.5 533338.9 183342.6 533438.8 183351.7 533469 183358.5 533470.5 183413 533472.6 183487.2 533475.4 183547.4 533479.4 183742 533478.1 183844.1 533479.6 183921.1 533557.9 183928.4 533667 183934.9 533714.4 183937.9 533735.2 183943.8 533719.7 183956 533700.9 183973.5 533684.8 183989 533663.3 184013.4 533693 184012.1 533723.7 184009.8 533736.6 184009.2 533779.7 184006.5 533807.9 184004.5 533827.5 184002.8 533882.3 183999.2 533882.4 184005.2 533930.4 184003.1 533928.4 183932.1 533925.2 183860.9 533928.2 183828.2 533937.5 183695.1 533942.4 183648.7 534044 183636.2 534094.3 183632.5 534105.3 183632.1 534116.1 183631.6 534164.2 183631.8 534223.2 183630.1 534330.8 183632.6 534431.4 183629.5 534479.5 183624.7 534466.7 183600.3 534458.1 183577.8 534454.7 183565.6 534456.6 183526 534463.6 183481.6 534466.6 183466.6 534477.6 183432.5 534486 183413 534496.6 183388.5 534502.3 183372.8 534472.2 183365 534431.7 183352.2 534313.1 183329.2 534303.3 183359.6 534301.1 183364.2 534286.4 183332.5 534269.8 183279.2 534252.2 183229.3 534234.1 183171.7 534225.6 183140.6 534156.8 183129.2 534109.3 183122.7 534019.3 183113.4 533976.4 183111.8 533933.7 183108 533885.2 183101.7 533857.5 183097.1 533837.3 183091.4 533813.9 183086.7 533778.1 183069.1 533768.9 183064 533753.4 183055 533710.8 183028.4 533692.3 183013.8 533683.8 183005.7 533670.1 182990.9 533651.6 182965.8 533633.1 182923.5 533608.1 182854.9 533597.6 182831.7 533587.2 182813.2 533584.2 182808.4 533560.1 182777.7 533539.3 182749.6 533503 182707.2 533478.3 182683.6 533543.8 182668.6 533541.7 182638 533530.1 182597.5 533523.8 182583.7 533523.8 182571 533524 182557.9 533525.4 182539.7 533532.1 182466.3 533543.3 182350.4 533579.8 182355.2 533590.8 182303.7 533595.6 182273.9 533595.3 182262.5 533593.2 182228.3 533590.5 182212.8 533589.1 182204.9 533587.6 182196.7 533578.1 182158.2 533574.1 182138.8 533568.8 182118.9 533567.3 182113.4 533549.2 182097.4 533530.3 182119.1 533501.9 182107.5 533447.5 182086.9 533426 182076.5 533411.9 182041.6 533410.7 182037.9 533320.2 182053.4 533250.9 182075.9 533230.5 182082.5 533215.8 182024.1 533198.6 181978 533184.6 181948.2 533182.4 181945.4 533167.5 181925.3 533146.8 181897.9 533119.2 181869.8 533078.9 181840.5 532946.1 181894.9 532955.7 181928 532965.8 181968.7 532978.1 182037.3 532989.2 182089.3 532993.7 182136 532998.2 182237.5 532999.2 182259.8 533004.7 182293.3 532983.6 182292.4 532941.1 182294.3 532941.6 182350.2 532918.3 182359 532920.4 182368.1 532929.3 182396.8 532944.9 182436.9 532963.7 182460.8 532942.7 182547.9 532938.5 182560.8 532968.5 182570.5 533030.4 182589.1 533033.1 182616.6 533034.4 182629.4 533033.9 182758.8 533098.2 182759.6 533130.9 182761.2 533172.8 182761.8 533179.8 182763.4 533188.1 182763.8 533220.3 182765.5 533225.7 182770.9 533274.9 182774.5 533279.2 182853.1 533280.3 182885 533279.7 182897.7 533277.3 182923.3 533263.6 182979.3 533261.1 182990.3 533259.6 183009.1 533259.8 183032.7 533261.9 183069.2 533260.6 183164.1 533260.9 183204 533259.9 183282.5</gml:posList></gml:LinearRing></gml:exterior></gml:Polygon>"^^rdf:XMLLiteral ;
          <http://data.ordnancesurvey.co.uk/ontology/geometry/hectares> 124.25 .
.......
```

行政区画には隣接関係と包含関係があります．隣接関係は [spatialrelations:touches](http://data.ordnancesurvey.co.uk/ontology/spatialrelations/touches)というプロパティです．包含関係は郵便番号と同様に[spatialrelations:within](http://data.ordnancesurvey.co.uk/ontology/spatialrelations/within), [spatialrelations:contains](http://data.ordnancesurvey.co.uk/ontology/spatialrelations/within)プロパティが使われていますが，[admingeo:county](http://data.ordnancesurvey.co.uk/ontology/admingeo/county), [admingeo:district](http://data.ordnancesurvey.co.uk/ontology/admingeo/district)あるいは[admingeo:inCounty](http://data.ordnancesurvey.co.uk/ontology/admingeo/inCounty), [admingeo:inDistrict](http://data.ordnancesurvey.co.uk/ontology/admingeo/inDistrict)のように直接の上下以外も明示的に個記述されています．


{% include image.html url="/images/2014-08-11-boundary-line/AdministrativeRegion.png" description="Administrative Region" %}
