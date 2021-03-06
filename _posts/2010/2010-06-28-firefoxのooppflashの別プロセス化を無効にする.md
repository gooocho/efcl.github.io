---
title: FirefoxのOOPP(Flashの別プロセス化)を無効にする
author: azu
layout: post
permalink: /2010/0628/res1811/
SBM_count:
  - '00009<>1355436678<>9<>0<>0<>0<>0'
dsq_thread_id:
  - 300873434
categories:
  - Firefox
tags:
  - Firefox
  - flash
  - ソフトウェア
  - プラグイン
  - 設定
---
公式にFirefox3.6.4がリリースされ、その中の大きな変更としてサードパーティ製プラグインを別プロセス化するOOPPという機能が盛り込まれデフォルトで有効になっています。  
3.6.4ではサードパーティ製プラグインのクラッシュ判定が応答しなくなって10秒となっていたのが3.6.6では判定時間を 45 秒に延長されています。(判定時間はdom.ipc.plugins.timeoutSecsで設定できます)

*   [次世代ブラウザ Firefox – Firefox 3.6.4 リリースノート][1]
*   [次世代ブラウザ Firefox – Firefox 3.6.6 リリースノート][2]

プロセスを分離することで、Flashがクラッシュしてもブラウザ全体を巻き込んで落ちなくなることが期待できますが、プロセスを分離したことで少し問題も発生したりします。  
OOPPはWindows と Linuxで導入されましたが、環境によっては逆に不安定になったりすることや、今までFirefoxのプロセスをホックして動作していたソフトウェアが正しく動作しなくなることがあります。  
具体的に言えば、Windowsでの**音量ミキサ**(プロセスごとに音量を設定する)や**myspeed**(ブラウザ上のFlashの再生速度を変更する)などのソフトウェアはプロセスが分離されたことで上手く動かなくなったりします。  
(音量ミキサの場合は&#8221;Plugin Container for Firefox&#8221;というプロセスの音量を設定することでなんとかなるかも)

### OOPPの無効化

ロケーションバーに[about:config][3]と入力して、*dom.ipc.plugins.enabled*と入力するとOOPPの有効無効の有無を決める設定が出てきます。  
[<img class="alignnone size-medium wp-image-1812" title="ss-2010-06-28-1" src="http://efcl.info/wp-content/uploads/2010/06/ss-2010-06-28-1-300x119.png" alt="" width="300" height="119" />][4]

出てくる項目で、*dom.ipc.plugins.enabled* はOOPP全体の有無でfalseにすれば無効となります。  
*dom.ipc.plugins.enabled.npswf32.dll* はFlashのプロセスを分離するかを決めることができ、入っているプラグインごとにそれぞれ決めることができます。  
プラグイン同士で[連携][5]していたりすることがあるらしいので、全てをtrue(有効)かfalse(無効)のどちらかにした方がいい気がします。  
falseにすると今まで同じようにプロセスは一緒になるので(音量ミキサやmyspeedも動作する)、OOPPが安定したりソフトウェアが対応するまでは無効化するのもありかと思います。

**MozillaZine.jp :: トピックを表示 &#8211; 【ヒント】Firefox 3.6.4 と OOPP について**
:   [http://forums.mozillazine.jp/viewtopic.php?t=10328&sid=4b9e3ceea6409b2f1e02c4db6fef54c6][6]

 [1]: http://mozilla.jp/firefox/3.6.4/releasenotes/
 [2]: http://mozilla.jp/firefox/3.6.6/releasenotes/
 [3]: http://wiki.mozilla.gr.jp/wiki.cgi?page=aboutconfig
 [4]: http://efcl.info/wp-content/uploads/2010/06/ss-2010-06-28-1.png
 [5]: http://forums.mozillazine.jp/viewtopic.php?t=10306&sid=454af6926a56fcd38a4aff7558479b4e
 [6]: http://forums.mozillazine.jp/viewtopic.php?t=10328&sid=4b9e3ceea6409b2f1e02c4db6fef54c6 "MozillaZine.jp :: トピックを表示 - 【ヒント】Firefox 3.6.4 と OOPP について"