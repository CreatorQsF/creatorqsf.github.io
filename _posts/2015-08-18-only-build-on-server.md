---
layout: default
title: buildのみServerで行う、について考える
---

## 発端はGoogle+での発言から。

どうも、軽いパソコンはchromebookのみの[@CreatorQsF](http://f.9en.co/?move=mainSns)です。
なかなかにつらいものがあります。(T_T)。  
日常的に1.5kgのMBPRを持ち運ぶのは、高校二年生のいたわるべき身体にはきついのです。(そういいつつ持ち歩いてる)

さてさて、なんでChromebookじゃだめかっていう話なんですが。

いや、勘違いしてほしくないのが、Chromebookがひどいプロダクトとはヒトコトも申しておりません!むしろ私はchromebook推奨委員会の回し者ですから(なんだそれ)、Chromebookをより良いものにしたいっていうのが大きなところなんです。  
しかーし、Chromebookは開発には向かないとよく言われます。理由はあらゆるソフトウェアが動かないから。

そこで私考えました。Server上で作業すればいいじゃないか、要するにsshでやればいいじゃんって。

一見、いい考えのように見えます。しかしながら、わたしのようにvimでgoしか書かない人間にはたしかに十分なように見えました、が、携帯電話ネットワークの遅さのせいで、sshでvimするともう遅延しすぎて書けない。ひどい(SoftBankさーんどうにかしてくださーい)  
PrivServerで行っているので別にServer上で何かすることは全然構わないんですが、いかんせん書けないのは勘弁。そういうわけで、最近はもっぱらMBPRを持ち運ぶ羽目になっているんです。

そこでふとおもいついて書いたこの投稿。

<div class="g-post" data-href="https://plus.google.com/+FumiTakeuchiQ/posts/PcR4DyPq7Ur"></div>

そうです。要するに、ローカルのvimで書いてそれをscpで送り込んでbuildしてその結果を表示するだけならば、何の問題もないんです。すとれすふりーってやつですよ。

で、これについて本格的に考えてみようかなと。

### セキュリティ

sshなのでpipeになるし、vpnなのでまず盗聴はありえないでしょう。それに鍵認証なのでまぁ破られないかな(あぶない

### ストレス

コードはローカルで書くので、agなどがchromebookで動くのかっていう問題はおいておいて、まぁカーソル遅延や予測しながらdeleteしなきゃいけないなんて問題は…おこらないと思います。ただGoogle製品なのにGo製のpecoが動かなそうなのは悔しい。そのまえにHP 11だとgoが動かないwww

### その他諸問題

最初はいけそうだなーと思ったんですけれども、よく考えたらgoはLibrary類が多いので、そのへんどうするか。  
要するに1ファイルならなんでもいいんですが、そんなプロジェクトイマドキほとんどありませんから…git?

って考えてです。もしかして普通にgitとhook使ってdeploy(?っていうのかな)させてそこでbuildさせた結果を流し込めば。って思いました。ってかそれが普通ですね。とおもいきや!!!!!

**HP 11 gitすらうごかないいいいいいいい**

よく考えたら、Chromebook HP 11上でGoとgitが動けば何の問題もないんです。もうそれだけで十分なんです。CPUめ!USB充電のためとはいえなぜスマホ用を使ってしまったのﾀﾞﾀﾞﾀﾞﾀﾞﾀﾞ

### つまり

つまり、わたしはscpとsshだけを駆使したbash function的なものを書かなければならないんです!!!なんと鬼畜な…。というかChromebookすごい。

でもdiffせずに全ファイルを送り込んでたら多分パケット量がなぁ…。でもあってもきろばいとか。

というわけで作ってみるとしたらの仕様。

### 仕様てきなやつ

1. 予め設定したディレクトリにおいてvimのみでコツコツ開発
1. ディレクトリの内容を全部まるごとscpで投げる。なおgo getはServer上で行うこととする(どうせServer上でしかbuildしないので)(:GoImport使えないとか可愛そうとかやめてくださいそもそもbundle類すら使えるかわかんないんです!!!)
1. 投げたら今度sshで入ってディレクトリに移動、そこでgo run(もしくはgo test)してみる
1. その結果をsshなのでどうせ見れるけど見る
1. scpにてServerからcodeを逆に落としてきて(ここがきつそう…ってかできるのかしら)また書き書き、そして…の繰り返し

…書いてて思ったけど、これボツだな…。

なお、Ubuntuいれろよ発言はやめてください。Chromebookのセキュリティそのままに、そしてChrome OSのままできるだけ使いたいんです。

これがだめだと、SoftBankのネットワークから乗り換えるか、やっぱりMacBookを結局は買うことになってしまうのか(それだとHP 11をかった意味が無い!)、悩ましいところであります。

(それと私はネットワーク系やサーバー系エンジニアとかそういうんじゃないんで怖い顔してご意見やめてください…。でもなんか良い手法とかあったら教えて下さい!)

さて、今日は立場がなかったHP 11ちゃんですが、明日辺りChromebook HP 11の再レビュー行っていきます。これがどうして私のそんなにお気に入りマシンなのか…正直自分でも不思議ですがw、これはいいものです。勘違いしないでください。ChromebookとChromeOSは本当にいい製品です。僕がその枠を超えた使い方をしようとしてるのが問題なだけであり、なのでDeveloperにおすすめできないのも知ってますし、僕はそれを承知でかっています。でもやっぱり…軽くて良いマシンは使いたいじゃないんですか!MBPR持ち運ぶの疲れたんですよ。

おわり

<script type="text/javascript" src="https://apis.google.com/js/plusone.js"></script>
