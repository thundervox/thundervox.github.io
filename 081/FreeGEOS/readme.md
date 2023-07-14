# PC/GEOS

* 公式リポジトリ: https://github.com/bluewaysw/pcgeos
* Wikipedia: https://ja.wikipedia.org/wiki/GEOS_(%E3%82%AA%E3%83%9A%E3%83%AC%E3%83%BC%E3%83%86%E3%82%A3%E3%83%B3%E3%82%B0%E3%82%B7%E3%82%B9%E3%83%86%E3%83%A0)

* ライセンス: Apache 2.0 [英語](https://www.apache.org/licenses/LICENSE-2.0) / [日本語](https://licenses.opensource.jp/Apache-2.0/Apache-2.0.html)
* 作業対象: [2023年03月27日 開発版](https://github.com/bluewaysw/pcgeos/tree/9672d033f192a4fd5103103bf385cc8cd58c48b7)

作業検討中(2023年09月〜2024年以降)

## なん？
かつてブラザーやキャノン製の英文ワープロ専用機、[HP OmniGo 100/120](https://mobileascii.jp/elem/000/001/409/1409113/)、ノキアの携帯電話などに採用されていた 16-bit [オペレーティングシステム](http://toastytech.com/guis/bbe.html)ですね...(Windows Me 以前と似たようなDOS に GUI OS と各種アプリケーションやオフィス・スゥイートが乗っている構造)。現在、その大部分は Apache ライセンス下でオープンソース化されています (元々の製品版である Breadbox Ensemble 4.13 からオープンソース化でライセンス問題となるモジュール除去したものだそうです)。

なお、Commondore 64 や Mega64 版もありますが、このプロジェクトでは扱いません (環境を用意するのが割と手間です。またワープロ専用機から外した8-bit CPU でワンボードPC作る予定がないのもありますが、単純に興味のあるかたが遊び尽くしたらいいだけです)。

[DOSbian](https://github.com/appnjoy/dosbian) と、この PC/GEOS のローカライズなどすれば当時の技術で日本語ワープロ専用機の復刻(＋レロトフィットキット)やらレトロコンピューティングは可能かと思います……。その先は
FDD や ISA カードつけた
り、 FreeDOS32/64, T-Kernel や Minix3 上で動くようにするとか X68000Z に移植したり、謎パーの再現などそれなりかつ、かなり長くに遊べるのでは？ 飲酒、喫煙、ギャンブルより安くて家族に迷惑がかからず仕事にも繋がりやすい？いい趣味ですね。

とまあ、その技術資料なんかを翻訳するかもしれません。この OS は C や x86 アセンブリ、R-BASIC 使わないと遊べないので (ハッカー気取りのOS作りたい学生の心を無慈悲に粉砕骨折させる気はありませんが)。そういう情報弱者が減りガチ勢が増えれば少しは生きやすくなるでしょう。たぶん。

## あるよね？

Vircon32 ですね。
そちらも並行して続けるでしょう。
キーボード使えないとこ、音源部に不満があって PCM 専用(そこはSIDだろ)ということなんですが。

## 翻訳支援について

この活動を通じてデジタル富国強兵になるとは考えていません。とはいえ、仮に無償で続けて欲しいなら相応の対価と社会に対する発展への参加を求めます。そうはならないことくらいわかってます。ある程度進んだら寄付を求めますけどね。目標額まで集まらなければ活動は断念するということです。

## 関連情報

* [blueway.Softworks (公式サイト)](https://blog.bluewaysw.de/)
* [Marcus Gröber's Homepage](http://mgroeber.de/)
* [GEOS-InfoBase / Startseite](https://www.geos-infobase.de/)
* [How PC/GEOS found a 5th life as an open source DOS shell | TechRepublic](https://www.techrepublic.com/article/how-pcgeos-found-a-5th-life-as-an-open-source-dos-shell/)
