---
layout: default
title: Goの凄さを語る。
---

## なぜ「ソレに適した言語選択をするべきだ」という私が、1言語にこだわりgoが優れていると言うのか。

どうも、[@CreatorQsF](http://f.9en.co/?move=mainSns)です。

突然ですが!、このブログは、Goで書かれています。(以前のバージョンはPHPです)

PHPからGoへ、一体何があったのか、今日は思うままに喋らさせていただこうと思っております!!!!!

### Goの凄さ

私の考えるGoの良い所はこれ。

- vimサポートが手厚い過ぎて泣ける
- いままで無駄だなと思った手順 / 嫌だなと思った仕様 / 迷う構文の書き方が殆ど無い
- くっそはやい
- はやいのにモダン
- Cのようにすごいやつを書ける
- パワフルすぎる
- `go fmt`が神の領域に達してる。ある程度の規模であればチーム作業するときにコーディング規約がいらない
- GoのGUIやgo.mobileもあり、まだ完全ではないが、各種Platform対応のアプリケーションができる
- もうすでにコンパイル自体はめっちゃ簡単にほぼすべてのPlatform向けにコンパイルすることが(それもひとつのOS上で、1コマンドで)行うことが可能
- オブジェクト指向であり、オブジェクト指向でない
- 厳格な型
- 標準パッケージ(?)でももうすごいのに(net/httpとか何者)、`go get`がさらに便利にしていてもうなんだかわからない

ざっとこんなところでしょうか。

例外処理のない言語が私は大好きで(でもその言語で搭載されていて推奨されているなら使います。それが言語に合わせた歴史を考える書き方だと思っています)、Goはまずそこが良い。

そして、errorがすごい。すごすぎる。便利。便利。

functionが返り値を2つもてるのもいいよねぇ。

あと、変数の定義が、`var hoge type`のように、`変数 型`の順で定義できるのが素晴らしい。

そしてgoroutineとchannelがもう泣ける。泣けるぐらい便利。最初の頃は違う意味で泣いてたけど。

というわけで、よく考えてみたらgoのすべてがすごいので、書ききれないというか、**Goすごい**でまとめられちゃうので、書く意味が無いかな、みたいなw

あと私はインデントはハードタブがいいんじゃないかなぁとすごく思っていて。その理由としては書く人が好きに幅設定できるじゃないですか。これからは、**仕様書にあった書き方をするんじゃなくて、書く人にコンパイル側とかfmtみたいなやつとかが合わせる？言うなれば、書く人に仕様書が合わせる**ことが、私はとても大事に、そしていい方法に成るんじゃないかなと、思うんです。

だって、みんな自分の理想の書き方があるわけで、それを統一するためだけに、書き手がそれを崩して合わせるのは納得出来ないです。生産性落としてないですかね。

……そんなこと実際の業務では言ってられないですけどね^^;

だからこそ、Goのように標準でformatツールがついてくるのは、これからのモダンな言語には欠かせないんじゃないかなぁと。IDEもオススメ出来ません。その環境で常に書くっていう保証ありません。IDEはあくまで**コーディングを助けるツールであり、コーディングにマストなものになってしまっては私は本末転倒だと思います。**

そんな感じでしょうか?何が言いたいかというと、私にとって、

**Go最高**

ということでした。みなさんGoへいらっしゃい!!!