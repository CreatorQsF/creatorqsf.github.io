---
layout: default
title: Evernoteのtemplateを一括で見れるようにしたいなと思い、場所を作りました。
---

## 新しいサービス作りました。隙間時間で1日で仕上げたので、あんま粗探しはしないでくださいw

今宵の月はどうでしょう。こんばんは、[@CreatorQsF](http://f.9en.co/?move=mainSns)です。  
突然ですが、あたらしいサービス作りました。  
[Evernote Template Ploce](https://evernote-ploce.de-liker.com/)

***

### 事の発端

昨日の夜、これ読んで、思ったことがありました。  
[Evernote はもっとテンプレートを配布するべきだと思う！Evernote 公式テンプレート「2016年 Evernote カレンダー」を入手してみました。 | R](http://beadored.com/evernote-2016-calendar-template-distribution/)

「Evernoteのテンプレートってほとんど知られてないし、うまく活用できてない感じがすごいあるなぁ。」と。  
そこで、Evernoteのテンプレート突っ込めるような、ポータル的なサイトあったらなんか良さそう、と思い立ち、Google検索するより何よりも、Goでここ何ヶ月も一生懸命継ぎ足し継ぎ足し改善して作ってきた、「servicehelper」という、小~中規模ならば知識さえあれば6時間ほどで作れるフレームワークではない、機能の寄せ集め、要するにライブラリですかね、みたいなものがローカルリポにありまして、仕事では何やかんやで使うことの多かったAngular(そんなに慣れているわけではない)をこれはもしかしたら正面から取り組むいい機会かもしれない、と思ったので、servicehelperにこの辺もうまく混合させたところへ、angular materialがめでたく1.0になったばかりだったので、これは使わない手はない!!!!と思い立ち、このサービスを作りました。なおデフォルトの色からいじってないのでなんか青いですが気にしないでくださいw  
あと全てのコンテンツがde-likerのADSLサーバーから提供されているので、ロードは遅いです。キャッシュなども設定していないに等しいので、遅いです。

なお、evernote template fileについては特に検閲をしていないので、たまにevernote template fileじゃないものも混ざっていることがあります。これは改善しなくちゃって思ってる。  
あとファイルをアップロードしたあとの動作作りが間に合わなかったので、そのうち作ります。あと検索ね。

なお、実際に6時間で作れたかというと、全くそんなことはなくて、servicehelperのメンテなどもしつつ、最後の方はgoでさえbuildが15秒くらいかかるというかなりおかしいことになっているので、まだまだ改善がいるなぁとはおもっております。でもgoの実行ファイルだけでサービスのdaemon化から全て終わっているのはなかなか便利。やっぱいいわ。

***

### 裏技術

Goでサーバーサイドは書いています。デザインは普段は自分でやるんだけど、Angular Materialを使って見たかったのでAngular Material使ってます。

フロントエンドはAngular jsです。言うまでもないかw  
GoとのやりとりはRest API…にしたかったんだけどなりきれなかった(というか仕様書自体がないし)感じで、base64でエンコードしたデータをpostでroutingしてあるところへ送る感じです。

goroutineは重い処理がなかったのでhttpサーバーのsericehelperの実装のところ以外では書いていません。その代わり、angularの方、クライアント側で結構重い処理が多いです。理由は生データでやりとりするのがめんどくさかったw

そんなこんなで縁があったら使ってやってくださいwww(誰がevernoteのtemplateなんか作るんだろう…。)

[Evernote Template Ploce](https://evernote-ploce.de-liker.com/)

おわり
