---
author: fumi
comments: true
date: 2008-07-29 07:39:38+00:00
layout: post
link: https://fumi.me/2008/07/29/wp-mixipublisher-patch/
slug: wp-mixipublisher-patch
title: wp-mixipublisherのpatch
wordpress_id: 112
categories:
- Mixi
- WordPress
tags:
- Mixi
- WordPress
---

[以前のエントリ](http://fumi.me/2008/07/27/wp-mixipublisher/)で言っていた、[Wp-MixiPublisher](http://factage.com/yu-ji/archives/2006/09/05/wp-mixipublisher-1_0_0rc2/)で[mixi](http://mixi.jp/)に投稿できないバグが取れました。`user_can_edit_post`がdeprecatedだったのが原因のようです。以下のパッチでとりあえずこの[ハッスルサーバー](http://px.a8.net/svt/ejp?a8mat=1C2BMF+8PRGKY+HQW+60OXE)では問題なく投稿できるようです。


```patch
--- wp-mixipublisher.php.backup 2008-07-29 15:05:00.000000000 +0900
+++ wp-mixipublisher.php        2008-07-29 16:15:33.081006700 +0900
@@ -112,7 +112,7 @@
     function publishToMixi($postId) {
         global $wpdb, $user_ID;

-        if(!user_can_edit_post($user_ID, $postId)) {
+        if(!current_user_can('edit_post', $postId)) {
             return $postId;
         }
```

修正後のwp-mixipublisher.phpをzipにして置いておきます。これは二つの変更(1, 2)もすでに適用されています。
[wp-mixipublisher.zip](/images/2008-07-29-wp-mixipublisher-patch/wp-mixipublisher.zip)
