---
author: fumi
comments: true
date: 2008-07-29 11:07:11+00:00
layout: post
link: https://fumi.me/2008/07/29/eeepc-evernote/
slug: eeepc-evernote
title: EeePCのSSD性能とEverNote
wordpress_id: 117
categories:
- EeePC
- EverNote
tags:
- EeePC
- EverNote
- SD
- SSD
---

メモツールはWiki→[Changelog memo](http://0xcc.net/unimag/1/)→howmと渡り歩いて、数か月前から[EverNote](http://evernote.com)を使っています。全部以前のメモを変換して取り込んであるのでかなりの量のメモがあります。




EeePCで困ったのが、EverNoteの動作が遅いということです。英文打つのは問題ないのですが、日本語の変換や確定の際に非常に時間がかかり、使い物になりません。何が悪いのかと考えてみると、EverNoteはちょっと変化があるだけでwriteするので、Diskの書込性能の問題なのではないかと思い、HDBenchでテストしました。以下結果。



<table summary="HDBench" >

<tr >DriveReadWriteRReadRWrite</tr>

<tbody >
<tr >
<td >C (SSD4GB)
</td>
<td >25296
</td>
<td >5345
</td>
<td >21913
<td >2367
</td></tr>
<tr >
<td >D (SSD8GB)
</td>
<td >25793
</td>
<td >5903
</td>
<td >22831
</td>
<td >3289
</td></tr>
<tr >
<td >F (SD16GB)
</td>
<td >18354
</td>
<td >12649
</td>
<td >17018
</td>
<td >3590
</td></tr>
</tbody>
</table>



明らかにC、DのSSDは書込が遅いです。それに対し、追加で挿してあるSDカードの書込性能は倍くらいになります。ランダムアクセスの書込みは変わらないようですが。というわけで、[EverNote](http://evernote.com)をFドライブに置くようにしたところ、日本語変換時も許容できる速度になりました。書込速度が必要なデータはSDカード上に置いたほうが良いようです。
