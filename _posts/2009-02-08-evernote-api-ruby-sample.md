---
author: fumi
comments: true
date: 2009-02-08 00:58:32+00:00
layout: post
link: https://fumi.me/2009/02/08/evernote-api-ruby-sample/
slug: evernote-api-ruby-sample
title: Evernote API - Ruby sample
wordpress_id: 660
categories:
- EverNote
- Ruby
tags:
- EverNote
- Programming
- Ruby
- Thrift
- WebAPI
---

Evernote APIのライブラリとサンプルはAPIのページからダウンロード可能です．サンプルはJava，Perl，PHP，Python，Rubyが用意されています．Rubyのサンプルはsample/ruby/EDAMTest.rbです．まず，EDAMTest.rbの13-16行目を，取得したAPI key，secret，開発サーバのユーザ名，パスワードで置き換えます．



    
    <code>
    consumerKey = "your-api-key-here!"
    consumerSecret = "your-api-secret-here!"
    username = "your-username"
    password = "your-password"
    </code>




次に，EDAMTest.rbの先頭にEvernote APIのライブラリのパスを追加します．



    
    <code>
    $:.unshift("../../lib/ruby/")
    </code>




ライブラリにはバグがあるので以下のパッチを当てます．thriftのほうを直すべきだと思いますが，とりあえず動かすために．



    
    <code>
    --- lib/ruby/thrift/struct.rb.orig      2009-02-07 17:07:30.000000000 +0900
    +++ lib/ruby/thrift/struct.rb   2009-02-08 09:40:56.000000000 +0900
    @@ -97,11 +97,11 @@
             end
             iprot.read_struct_end
           end
    -      validate
    +#      validate
         end
    
         def write(oprot)
    -      validate
    +#      validate
           if oprot.respond_to?(:encode_binary)
             # TODO(kevinclark): Clean this so I don't have to access the transport.
             oprot.trans.write oprot.encode_binary(self)
    </code>



    
    <code>
    --- lib/ruby/thrift/transport/httpclient.rb.orig        2009-02-08 09:46:12.000000000 +0900
    +++ lib/ruby/thrift/transport/httpclient.rb     2009-02-08 09:46:53.000000000 +0900
    @@ -19,6 +19,7 @@
         def flush
           http = Net::HTTP.new @url.host, @url.port
           http.use_ssl = @url.scheme == "https"
    +      http.verify_mode = OpenSSL::SSL::VERIFY_NONE
           headers = { 'Content-Type' => 'application/x-thrift' }
           resp, data = http.post(@url.path, @outbuf, headers)
           @inbuf = StringIO.new data
    </code>




後は，残りの必要なライブラリをインストールします．Ubuntu8.10だと以下のように入力します．



    
    <kbd>
    $ sudo aptitude install libreadline-ruby libhttp-access2-ruby
    </kbd>




ここまで設定すれば，ruby EDAMTest.rbと入力することでサンプルプログラムが起動すると思います．
入力した文章を新しいノートとして取り込むという単純なプログラムです．
