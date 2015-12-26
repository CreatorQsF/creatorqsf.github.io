---
layout: default
title: Goのポインタを使ったinitializeで詰まった話(結果:ドキュメント読もう)
---

## 珍しいちょっとしたtips

今宵の月はどうでしょう。こんばんは、[@CreatorQsF](http://f.9en.co/?move=mainSns)です。  
最近Goは来てますね。vimも来てるんですが、どういうわけかなんだかその現状を批判するのが流行りそうな雰囲気。僕はこの先馬鹿にされてもvimを使い続けます。

今日は、あほらしい、一年間ぐらいGoをやってきたとは思えないところでつまづいたので、それを自分への戒めとして、また誰かのために、ここに書きたいと思います。

### 事の発端はこんな感じのコード

<script src="https://gist.github.com/Qs-F/39b5ff8ca3ece7c76958.js"></script>

で、実はこれ動かしてもらえばわかるんですが、panicエラーになるんです。[The Go Playground](http://play.golang.org/p/yQUoy37gwv)

このpanicエラーは配列の未定義の部分にアクセスしようとしたりすると起きるのですが、僕はforとrangeで回しているので、大丈夫と思っていました。要するに配列はこの場合0 indexは存在するはずなんです。で、最初、プログラム内でやっている時はappendしている時に何かあるな、と思っていました。  
ちなみに今はこれただの変数ですが、私がやっていたのは構造体側だったので、varを使ったわけなんです。

ですが、どうやってもpanicエラーが起きるので、仕方なくこのようにコードを変えてみました。

<script src="https://gist.github.com/Qs-F/2cd90ac7911d0c4797ed.js"></script>

動かすとこんな感じです。[http://play.golang.org/p/F3iaFhbMgG](http://play.golang.org/p/F3iaFhbMgG)

これでお分かりいただけるでしょう。appendなどには何の問題もなくて、var initalize事態に問題があると。

でもこっちのコードはうまく動くんですよね…。

[The Go Playground](http://play.golang.org/p/pArS2eRtMz)  
<script src="https://gist.github.com/Qs-F/5f8409722b35e587d00f.js"></script>

またこれも。

[The Go Playground](http://play.golang.org/p/6VVRHILhg5)  
<script src="https://gist.github.com/Qs-F/61306b43b7e0f6431137.js"></script>

なるほど、どうも、pointerの配列の定義は何かあるらしい。とやっとここで気づいて、というか教えてもらって([[SOLVED] Would Anyone explain why is this be error? http://play.golang.org/...](https://plus.google.com/u/0/+FumiTakeuchiQ/posts/Mg8Gp5YMfXh))

> var s *[]int is a pointer to an array while var s []int is the array itself. Golang initializes variables to the 0 value. For the pointer that's nil the concrete array is an empty array.

とあるように、そうなんです。Goのpointerでのinitalizeした後の要素は常にnilに成るらしいのです。

これを知らないって、一体お前はGoで何をしてきたんだよ…って言われそうですが、ここで初めて、前に誰かが書いてたGoらしい書き方を思い出しました。というかいつもは基本それでしか書いてなかったので、気がつかなかったんです…。

[http://play.golang.org/p/JrJpG3HGWu](http://play.golang.org/p/JrJpG3HGWu)  
<script src="https://gist.github.com/Qs-F/8ffd1d26431b6c6cc828.js"></script>

***

**結論:ドキュメント読もう**

以上、Go初心者の詰まったところ、でした。G+のGo+コミュニティは以前もお世話になっていて、すごいありがたいです。Goをやっている方はオススメです!!

おわり
