---
author: fumi
comments: true
date: 2009-01-31 03:54:24+00:00
layout: post
link: https://fumi.me/2009/01/31/zsh-completion/
slug: zsh-completion
title: zshの補完機能
wordpress_id: 630
categories:
- Software
tags:
- zsh
---

zshに再挑戦して1ヶ月経ちました．大分慣れてきたのですが，補完機能に関しては不満があります．zshの補完機能は大変お節介で，一文字打つ毎に補完するので，必要なときにTAB (bash)やCtrl-D (tcsh)で補完していたときと比べて鬱陶しく感じるときがあります．




特にscpでリモート作業するときにも，一文字毎にリモートにアクセスして補完しようとするのですが，emobileなどを使っているときは遅くて使えません．また，sshkeyの設定をしていないときには，一文字毎にパスワードを聞かれます．同様の不満はあるようで，zshのメーリングリストに[解決法](http://www.zsh.org/mla/workers/2004/msg00424.html)が書いてありました．以下を.zshrcに書けばscpのときに補完機能が無効になります．




<blockquote>
zstyle ':completion:*:complete:scp:*:files' command command -
</blockquote>
