---
title: FirebugでJSON形式を見易くフォーマットするuserChrome.js
author: azu
layout: post
permalink: /2009/1115/res1463/
aktt_notify_twitter:
  - no
SBM_count:
  - '00006<>1355436785<>4<>0<>1<>1<>0'
dsq_thread_id:
  - 300802430
categories:
  - userChome.js
tags:
  - Firebug
  - JSON
  - userChrome.js
---
FirebugでDOMをtoSource()したときに生成されるJSON形式のようなものがかなり見えづらいので、それを読みやすくコンソールに表示するuserChrome.jsを作成した。   
あくまで、**見易く表示**させることを目的としてたので、整形したものを使うという用途には向いてないかもしれません。

<!--more-->

こっからダウンロード

*   [<span>Firebug JSON formatting.uc.js</span>][1]

例えばニコニコ動画のマイリストでmy.currentItemes[0].toSource() をやると下のようなものが表示されます。   
整形されていないしUTF-8などが混ざっていて読みづらいです。

<pre class="brush:javascript;">({item_type:0, item_id:"1237006406", description:"", item_data:{video_id:"sm6429247", title:"u3010u521Du97F3u30DFu30AFu3011Blunder girlu3010u30AAu30EAu30B8u30CAu30EBu66F2u3011", thumbnail_url:"http://tn-skr4.smilevideo.jp/smile?i=6429247", first_retrieve:1237006407, update_time:1245142420, view_counter:"1469", mylist_counter:"58", num_res:"38", group_type:"default", length_seconds:"112", deleted:"0", last_res_body:"u3053u306Eu4EBAu306Fu30D4u30B3u30D4u30B3u97F3u306E u51FAu3060u3057u304Cu661Fu9593u98DBu884Cu306Bu8074 sm7203573u306Bu3066u4F7Fu7528u3055. ", watch_id:"sm6429247"}, watch:0, create_time:1237007514, update_time:1254596442})
</pre>

そこでこのuserChrome.jsを使って整形して表示させると、コンソールに次のような結果が返ってきます。

<pre class="brush:javascript;">(object){
	item_type (number): 0
	item_id (string): 1237006406
	description (string):
	item_data (object){
		video_id (string): sm6429247
		title (string): 【初音ミク】Blunder girl【オリジナル曲】
		thumbnail_url (string): http://tn-skr4.smilevideo.jp/smile?i=6429247
		first_retrieve (number): 1237006407
		update_time (number): 1245142420
		view_counter (string): 1469
		mylist_counter (string): 58
		num_res (string): 38
		group_type (string): default
		length_seconds (string): 112
		deleted (string): 0
		last_res_body (string): この人はピコピコ音の 出だしが星間飛行に聴 sm7203573にて使用さ.
		watch_id (string): sm6429247
	}
	watch (number): 0
	create_time (number): 1237007514
	update_time (number): 1254596442
}

</pre>

整形後は何が何の要素なのかがわかりやすく表示されています。  
さきほど、整形したものを再利用しにくいと書いたのは、その要素がstringであるなどの情報も含んでいるためです。

### 使い方

<br class="spacer_" /><figure id="attachment_1470" style="width: 300px;" class="wp-caption alignnone">

[<img class="size-medium wp-image-1470" title="2009-11-14 22-48-43" src="http://efcl.info/wp-content/uploads/2009/11/2009-11-14-22-48-43-300x55.png" alt="使い方の流れ" width="300" height="55" />][2]<figcaption class="wp-caption-text">使い方の流れ</figcaption></figure> 
<br class="spacer_" />

1.  FirebugのコマンドラインにJSON形式のものだけを入力する(コマンドラインに入力されているものをそのまま使います)
2.  右下のJSONボタンを押す
3.  コンソールに結果が表示される。

整形するのに[JSONDecoder.js][3]を使用させてもらっています。

**JSONを見やすく展開してFirebugとかで表示 &#8211; JSONDecoder.js [ゼロと無限の間に]**
:   [http://0-oo.net/sbox/javascript/json-decoder][4]

**gist: 234552 &#8211; GitHub**
:   [http://gist.github.com/234552][5]

<br class="spacer_" />

 [1]: http://gist.github.com/raw/234552/643b98a1f96d3a77efae5627c662bd406d77ea5b/Firebug%20JSON%20formatting.uc.js
 [2]: http://efcl.info/wp-content/uploads/2009/11/2009-11-14-22-48-43.png
 [3]: http://0-oo.net/sbox/javascript/json-decoder
 [4]: http://0-oo.net/sbox/javascript/json-decoder "JSONを見やすく展開してFirebugとかで表示 - JSONDecoder.js [ゼロと無限の間に]"
 [5]: http://gist.github.com/234552 "gist: 234552 - GitHub"