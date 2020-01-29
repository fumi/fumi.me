---
author: fumi
comments: true
date: 2008-08-02 07:59:54+00:00
layout: post
link: https://fumi.me/2008/08/02/eeepc-sdhc/
slug: eeepc-sdhc
title: EeePCカスタマイズ - SDHCをHDD化
wordpress_id: 133
categories:
- EeePC
- Hardware
- Mobile
tags:
- EeePC
- HDD
- SDHC
---

【Eee PC】SDカードをHDD化手順を参考に行いました。EeePC901では[ASUS Eee PC 質問スレ パート２](http://pc11.2ch.net/test/read.cgi/notepc/1216962402/)に書いてある変更が必要ですのでメモしておきます。

Hitachi Microdrive Filter Driverを入手します。それを解凍後、cfadisk.infの35行目に、以下を追加します。

```
%Microdrive_devdesc% = cfadisk_install,USBSTOR\DiskSingle__Flash__Reader__USB__Device
```    

後は同様にドライバの更新によってcfadisk.infを強制的に読み込ませれば大丈夫です。また、私の場合は、インストールの途中でdisk.sysが見つからないというエラーが出ましたが、C:\Windows\system32を指定すればOKでした。
