---
author: fumi
comments: false
date: 2010-02-22 15:36:10+00:00
layout: post
link: https://fumi.me/2010/02/23/rdfcontext/
slug: rdfcontext
title: RdfContext
wordpress_id: 2853
categories:
- Programming
- Ruby
- SemanticWeb
- Web
tags:
- Library
- RDF
- RDFa
- Ruby
- SemanticWeb
---

自分用メモとして，言語毎にRDFを扱えるライブラリのまとめをしていきたいと思っています．とりあえずまずはRubyから．RubyはRDFライブラリの対応具合がばらばらで，これといったものがありませんでした．一番人気がある方法がJRuby経由で[Jena](http://jena.sourceforge.net/)を使うことです．私はCライブラリである[Redland](http://librdf.org/)のRubyバインディングをたまに使っていました．しかしここ最近，Pure Rubyなライブラリが出てきているので，調査しています．

まず今回は[RdfContext](http://github.com/gkellogg/rdf_context)です．[Reddy](http://github.com/tommorris/reddy)がベースとなっています．主な機能は以下の通り．


* Parser: RDF/XML, RDFa, N3
* Store: List(Array), Memory, SQLite3
* Serialization: RDF/XML, N-Triples

まだRDFの入出力しか対応しておらず，SPARQLなどの機能はTodoとなっています．また，非ASCII文字は全部unicode escapeされます．Ruby1.9.1で動かなかったので，とりあえず動くようにする[Patchを送った](http://gkellogg.lighthouseapp.com/projects/43717/tickets/1-patches-for-ruby-19)のですが，作者のGreggが今色々と対応中で，近い内にversion0.5を出したいとのことなので，しばらく待とうと思います．

### 使い方

インストールはgemでできます．Ruby 1.8.7なら動くはずです．Ruby1.9以上で使う場合は上記のPatchをインストール後に当てればとりあえず使えます．

```bash
$ gem install rdf_context
```

RDFファイルを読み込んでN-Triplesで出力するコードは以下のようになります．p.parseの2つ目の引数で基点となるURIを与える必要があります．与えなかった場合は適当なbnodeになるようです．

```ruby
#!/usr/bin/ruby
require 'rubygems'
require 'rdf_context'
require 'open-uri'

include RdfContext
p = Parser.new
str = open("http://fumi.me/foaf.rdf").read
g = p.parse(str, "http://fumi.me/foaf.rdf", :type => :rdfxml)

#puts g.to_rdfxml
puts g.to_ntriples
```

また，GraphにTripleを追加いきたいときは，ストレージ先を指定したGraphを先に作れば良いです．引数storeについては，今のところListは動くのですが，まだSQLite3で動かせていません．引数identifierは，NamedGraph用のようです．下記のコードで，二つのRDF/XMLの内容をまとめた一つのRDF/XMLを出力することができます．

```ruby
include RdfContext

## 動かない
#g = Graph.new(:store => SQLite3Store.new(:path => "store.db"), :identifier => URIRef.new("http://fumi.me"))

g = Graph.new(:store => :list_store,
            :identifier => URIRef.new("http://fumi.me"))
g.parse(open("http://fumi.me/foaf.rdf").read,
            "http://fumi.me/foaf.rdf", :type => :rdfxml)
g.parse(open("http://semantictweet.com/fumi1").read,
            "http://semantictweet.com/fumi1", :type => :rdfxml)
puts g.to_rdfxml
```

全体的にまだまだこれからという印象です．
