---
author: fumi
comments: false
date: 2010-07-07 11:47:49+00:00
layout: post
link: https://fumi.me/2010/07/07/virtuosoontowiki/
slug: virtuosoontowiki
title: Virtuoso+OntoWiki
wordpress_id: 2951
categories:
- SemanticWeb
- Ubuntu
tags:
- DB
- OntoWiki
- RDF
- SPARQL
- Ubuntu
- Virtuoso
---

Twitterを見れば分かるとおり最近RDF Storeの調査をしているのですが、その過程でOntoWikiを使おうとして色々嵌っているので、ログを残しておきます。現在Ubuntu10.04での動作を確認しています。

### Virtuosoのインストール

[Open Link Virtuoso](http://virtuoso.openlinksw.com/)は複数のデータ形式を統合して扱えるデータベースです。RDF Triple/Quad Storeとしても使え、SPARQLにも対応しています。[Open Source版](http://virtuoso.openlinksw.com/dataspace/dav/wiki/Main/)とClosed Source版があり、Closed版ではClusterやSnapshoなどの追加機能があります。ここではOpen Source版を使います。

まず[Virtuoso Open Source Edition](http://virtuoso.openlinksw.com/dataspace/dav/wiki/Main/)のインストールです。Ubuntuのrepositoryにあるのが6.1.0で、これだと最新のOntoWikiが不具合起こすので、[debian squeeze](http://packages.debian.org/squeeze/virtuoso-opensource
)から最新のソースパッケージ持ってきて再構築しました。


```bash
$ wget http://ftp.de.debian.org/debian/pool/main/v/virtuoso-opensource/virtuoso-opensource_6.1.1+dfsg1-1.dsc
$ wget http://ftp.de.debian.org/debian/pool/main/v/virtuoso-opensource/virtuoso-opensource_6.1.1+dfsg1.orig.tar.gz
$ wget http://ftp.de.debian.org/debian/pool/main/v/virtuoso-opensource/virtuoso-opensource_6.1.1+dfsg1-1.diff.gz
$ dpkg-source -x virtuoso-opensource_6.1.1+dfsg1-1.dsc
$ cd virtuoso-opensource-6.1.1
```

再構築に必要なパッケージをインストールします。

```bash
$ aptitude build-dep virtuoso-opensource
$ aptitude install quilt fakeroot
```

変更点はbuild formatを変えるだけです。changelogとかもそのままでbuildします。

```bash
$ echo "3.0 (quilt)" >debian/source/format
$ debuild -us -uc
```

ライブラリが足りなければ適宜インストールしてください。もし問題がなければ、上のディレクトリに*.debができているのでインストールします。インストール時にデータベースのパスワードを聞かれるので設定します。

```bash
$ dpkg -i ../*.deb
```

次のコマンドで問題なく起動できればインストール完了です。

```bash
$ /etc/init.d/virtuoso start
```

### ODBCの設定 (要確認)

**NOTE: この設定は必要ないかもしれないので要確認**

まずodbcinstをインストールします。

```bash
$ aptitude install odbcinst odbcinst1debian1
```

その後、`/etc/odbcinst.ini,odbc.ini`を以下のように作成します。

```
- /etc/odbcinst.ini
[virtuoso-odbc]
Driver  = /usr/lib/odbc/virtodbc.so

- /etc/odbc.ini
[ODBC Data Sources]
VDS  = Virtuoso

[VDS]
Driver  = virtuoso-odbc
Description  = Virtuoso Open-Source Edition
ServerName  = localhost:1111

[VOS]
Driver  = /usr/lib/odbc/virtodbc.so
Description  = Virtuoso OpenSource Edition
Address = localhost:1111
```

### OntoWiki
[OntoWIki](http://ontowiki.net/)はRDF用の閲覧・編集環境です。CMSと言ったほうがいいかもしれません。

とりあえずphp5とapacheの基本的な設定をしておく必要があります。解説を書いている方がたくさんいるので、やり方はググってください。一点追加で必要なのが、php5-odbcのインストールです。

```bash
$ sudo aptitude install php5-odbc
```

php5とapacheをインストールしたら、[InstallFromMercurial](http://code.google.com/p/ontowiki/wiki/InstallFromMercurial)に書かれている通りに、レポジトリから最新のソースをインストールします。


```bash
$ cd /var/www
$ hg clone https://ontowiki.googlecode.com/hg/ owrep
$ cd owrep/ontowiki/src/libraries
$ ln -s ../../../erfurt/src/Erfurt .
$ ln -s ../../../RDFauthor .

$ wget http://framework.zend.com/releases/ZendFramework-1.9.4/ZendFramework-1.9.4-minimal.tar.gz
$ tar xvzf ZendFramework-1.9.4-minimal.tar.gz
$ mv ZendFramework-1.9.4-minimal/library/Zend .
$ rm -rf ZendFramework-1.9.4-minimal.tar.gz ZendFramework-1.9.4-minimal

$ cd /var/www/owrep/ontowiki/src
$ cp htaccess-dist .htaccess
$ cp config.ini-dist config.ini
```

次に[UsingOntoWikiWithVirtuoso](http://code.google.com/p/ontowiki/wiki/UsingOntoWikiWithVirtuoso)を参考にconfig.iniの設定をします。

```
[private]
store.backend = virtuoso
store.virtuoso.dsn = VOS
store.virtuoso.username = dba
store.virtuoso.password = dba
```

その後OntoWikiに必要なディレクトリ作成します。

```bash
$ mkdir cache log uploads
$ chown www-data:www-data cache log uploads
```

Apacheの設定をします。そのままトップに置くのなら`/etc/apache2/sites-enabled/000-default`のDocumentRootと該当Directoryを変更します。

```
DocumentRoot /var/www/owrep/ontowiki/src
<Directory /var/www/owrep/ontowiki/src>
```

Apacheを再起動した後、http://localhostにアクセスしてください。問題なければOntoWikiが表示されます。ユーザ名 Admin パスワードなしでログインすると管理画面になります。


### Conference Model Demo

FirstStepにConferenceデータのデモの作り方がかかれています。注意する必要があるのは、もしlocalhost以外で動かす場合、Google Maps API Keyの設定が必要です。[API Key取得ページ](http://code.google.com/intl/ja/apis/maps/signup.html)で生成した文字列を`ontowiki/extensions/components/map/component.ini`に設定します。

```    
- ontowiki/extensions/components/map/component.ini
apikey.google = "生成した文字列"
```
