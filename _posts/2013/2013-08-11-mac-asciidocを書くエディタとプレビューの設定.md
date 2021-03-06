---
title: '[Mac] Asciidocを書くエディタとプレビューの設定'
author: azu
layout: post
permalink: /2013/0811/res3392/
dsq_thread_id:
  - 1595101427
categories:
  - 雑記
tags:
  - asciidoc
  - Editor
---
# はじめに

[書籍制作でReVIEWを使う実践ワークフロー][1]  
をみて、Oreillyとかで使われてる[AsciiDoc][2]はどうなんだろと思って、

とりあえず書ける環境を作ってみたのでメモ。

## AsciiDoc

[AsciiDoc][2] はMarkdownとかと同じようにテキストベースで書いて、  
HTMLやDocBook(ここからepubとかPDFとか大抵のフォーマット)に変換できるフォーマットのことです。

*   [AsciiDocは技術的な記事やマニュアル、本を書く際に必要なすべての構造的要素をサポートする &#8211; 不悔必省][3]
*   [AsciiDoc その2 &#8211; 不悔必省][4]

Oreilly [Atlas][5] でも、AsciiDocは使われていて、ウェブエディタもあったりします。

AsciiDocのプロセッサーの実装は、本家[AsciiDoc][6] と Rubyで書かれた[Asciidoctor][7]があります。

今回は[Asciidoctor][7]の方を使っていきます。

## エディタ

専用のエディタやサポートしてるエディタがあまり多くない感じだったので、  
Sublime Text2 の [SublimeText/AsciiDoc][8] を使用します。

<img src="http://efcl.info/wp-content/uploads/2013/08/README.asciidoc-2013-08-11-14-56-55.jpg" alt="README asciidoc 2013 08 11 14 56 55" title="README.asciidoc 2013-08-11 14-56-55.jpg" border="0" width="489" height="600" />

シンタックスハイライトとスニペットとキーボードショートカットが入ってる感じです。

## プレビュー

プレビュー用のアプリは特に見つからなかったので、[Marked][9]を使います。

[Marked][9] はMarkdown用のプレビューアプリですが、プロセッサーを任意のものに変更できます。

<img src="http://efcl.info/wp-content/uploads/2013/08/Behavior-2013-08-11-14-59-50.jpg" alt="Behavior 2013 08 11 14 59 50" title="Behavior 2013-08-11 14-59-50.jpg" border="0" width="537" height="402" />

まずは、プロセッサーが必要なので、

> gem install asciidoctor 

[Asciidoctor][7]をインストールしておき、  
`Custom Markdown Processor` にチェックを入れて

    Path: /path/to/asciidoctor
    Args: --backend html5 -
    

と入れておきます。

こうすれば、任意の `asciidoc` ファイルを開けばプレビューできます。

(Markedってプロセッサーの設定切り替えとかないのかな…)

<img src="http://efcl.info/wp-content/uploads/2013/08/README.asciidoc-2013-08-11-15-02-29.jpg" alt="README asciidoc 2013 08 11 15 02 29" title="README.asciidoc 2013-08-11 15-02-29.jpg" border="0" width="600" height="357" />

参考 :

*   [MarkedでreStructuredTextをリアルタイムプレビューする &#8211; F13][10]

## 書き心地

[AsciiDoc][6] の記法自体についてですが、  
Markdownと似てる感じの部分が多く馴染みやすいと思います。

Markdownよりは表現できることは多くて、imgのwidthやaの_blankの属性のサポートやifdefのマクロ等普通に書いてて必要になる部分は大体揃ってる気がします。

記法については公式より、 [AsciiDoc Writer’s Guide | Asciidoctor][11] の方が読みやすいと思います。

[AsciiDoc その2 &#8211; 不悔必省][4]でも書かれていましたが、  
リスト系の記法が充実していて、ネストのサポートやリスト同士の間に改行がある場合につなげる方法等よく出来てると思います。

[Admonition blocks][12] の等の[blocks][13]記法で  
ソースコードやコメント、生のHTML埋め込み等ができるようになってます。

ちょっと面白いなと思ったのはTable記法で、テキストで無理やりテーブルを表現するのではなく、カラムごとにわけてけるのは見た目的に整理しやすくていいなーと思いました。

    [options="header"]
    |===
    |Name |Group |Description
    
    |Firefox
    |Web Browser
    |Mozilla Firefox is an open-source web browser
    
    |Ruby
    |Programming Language
    |A programmer's best friend.
    
    |===
    

=>

<table class="tableblock frame-all grid-all" style="width:100%; ">
  <colgroup> <col style="width:33%;"/> <col style="width:33%;"/> <col style="width:33%;"/> </colgroup> <tr>
    <th class="tableblock halign-left valign-top">
      Name
    </th>
    
    <th class="tableblock halign-left valign-top">
      Group
    </th>
    
    <th class="tableblock halign-left valign-top">
      Description
    </th>
  </tr>
  
  <tr>
    <td class="tableblock halign-left valign-top">
      <p class="tableblock">
        Firefox
      </p>
    </td>
    
    <td class="tableblock halign-left valign-top">
      <p class="tableblock">
        Web Browser
      </p>
    </td>
    
    <td class="tableblock halign-left valign-top">
      <p class="tableblock">
        Mozilla Firefox is an open-source web browser
      </p>
    </td>
  </tr>
  
  <tr>
    <td class="tableblock halign-left valign-top">
      <p class="tableblock">
        Ruby
      </p>
    </td>
    
    <td class="tableblock halign-left valign-top">
      <p class="tableblock">
        Programming Language
      </p>
    </td>
    
    <td class="tableblock halign-left valign-top">
      <p class="tableblock">
        A programmer&#8217;s best friend.
      </p>
    </td>
  </tr>
</table>

軽く触った感じでは、Sphinxほど記法が重くないので良い感じだなーと思いました。

 [1]: http://www.slideshare.net/mhidaka/review-25116838 "書籍制作でReVIEWを使う実践ワークフロー"
 [2]: http://www.methods.co.nz/asciidoc/ "AsciiDoc"
 [3]: http://d.hatena.ne.jp/travelershouse/20130224/1361711279 "AsciiDocは技術的な記事やマニュアル、本を書く際に必要なすべての構造的要素をサポートする - 不悔必省"
 [4]: http://d.hatena.ne.jp/travelershouse/20130311/1363012055 "AsciiDoc その2 - 不悔必省"
 [5]: http://atlas.labs.oreilly.com/ "Atlas"
 [6]: http://www.methods.co.nz/asciidoc/userguide.html "AsciiDoc"
 [7]: http://asciidoctor.org/ "Asciidoctor"
 [8]: https://github.com/SublimeText/AsciiDoc "SublimeText/AsciiDoc"
 [9]: http://markedapp.com/ "Marked"
 [10]: http://blog.f13.jp/post/21638378100/marked-restructuredtext "MarkedでreStructuredTextをリアルタイムプレビューする - F13"
 [11]: http://asciidoctor.org/docs/asciidoc-writers-guide/ "AsciiDoc Writer’s Guide | Asciidoctor"
 [12]: http://asciidoctor.org/docs/asciidoc-writers-guide/#admonition-blocks "Admonition blocks"
 [13]: http://asciidoctor.org/docs/asciidoc-writers-guide/#building-blocks-in-asciidoc "blocks"