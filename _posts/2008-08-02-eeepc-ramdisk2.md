---
author: fumi
comments: true
date: 2008-08-02 07:41:47+00:00
layout: post
link: https://fumi.me/2008/08/02/eeepc-ramdisk2/
slug: eeepc-ramdisk2
title: EeePCカスタマイズ - RAMDISK (2)
wordpress_id: 130
categories:
- EeePC
- Hardware
- Mobile
tags:
- EeePC
- ERAM
- Hardware
- Mobile
- Windows
---

[RAMDISK](http://fumi.me/2008/07/27/eeepc-customize/)の続きですが、設定する値は、MAXMEM=1528(MB), ERAM=524288(KB)にしています。EeePC901はGraphics用に8MB使用するようなので、実メモリが2048MBでRAMDISKを512MBにしようとする場合、残りの部分は2048-8-512=1528となります。これをMAXMEMに指定します。そして512MB=524288KBをERAMに設定すればOKです。WindowsXPではZドライブが509MBとして表示されます。
