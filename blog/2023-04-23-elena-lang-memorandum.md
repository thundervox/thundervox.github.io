# 2023年4月23日 - 雑記

## つぎの

もはや、マイナーなオブジェクト指向言語の括りでは翻訳したいものが無いので、

 * [bx](http://www.skrenta.com/bx/) - 開発終了
 * [Cobra](http://cobra-language.com/) - ポスト Python になれなかったがほんの数名ほど開発再開を熱望する声がある。
 * [Component Pascal](https://en.wikipedia.org/wiki/Component_Pascal) - ニコラウスの遺産。事実上開発終了。 Squeak や Pharoには勝てなかった。
 * [ECERE SDK](https://www.ecere.org/) - マイナー言語の悪いところ全て兼ね備えた実装というか大した言語仕様でもなく自前ライブラリ直線番長なので Ring で十分。
 * [Eero](https://github.com/eerolanguage) - 開発終了
 * [EO](https://github.com/objectionary/eo) - 今後次第
 * [Fantom](https://fantom-lang.org/) - 今後次第
 * [Falcon](http://www.falconpl.org/) - 開発終了
 * [Nemerle](http://nemerle.org/) - かなりの所まで機能面は攻めたが事実上開発終了。
 * [Gravity](https://github.com/marcobambini/gravity) - 開発は停滞しているものの某所で翻訳している。
 * [Nice](https://nice.sourceforge.net/) - 開発終了
 * [Hush](https://hush.sourceforge.net/) - 開発終了
 * [Qore](http://qore.org/) - マイナー言語だけど意外とツウな仕様で求めている人はいそうな。
 * [TkScript](http://www.tkscript.de/) - clamp, constraint, prepare 以外の特筆点が見当たらない (これらは TkScript でなくても言語仕様を変更せずにユーザサイドで実装可能だと考えられる)。ELENA で十分。
 * [Unicorn](https://sourceforge.net/projects/unicon/) - 今後次第
 * [zkl](http://www.zenkinetic.com/zkl.html) - 良いところまで行ったのに開発終了。
 * この[あたり(dmoz-odp.org)](https://dmoz-odp.org/Computers/Programming/Languages/Object-Oriented/)に掲載されているもの。
 * その他 (後日追記)

などは ELENA のプログラミングマニュアルが出来上がっても付属資料の翻訳はしないと思います。理由は没個性で似たりよったりの言語仕様、翻訳したとしても誰かのためになるかはっきりしません (もちろん、Eiffel や Pharo は別格ですし、Objeck は割と好みです)。使われない無用の長物を増やすことが豊かさや機会を増やすことであるとは考えられないです。そういうのは人間側が手間隙かけるより誰が何を言おうと手抜きでも機械翻訳で十分でしょう（その手抜きで得た成果を手軽に共有できるプラットフォームがないのは課題ですが）。

また、マイナー言語は泥沼です。プログラマとしての本分であるコードを書くことを忘れ、辞めたくてもやめられない事情が出来てしまうこともあります。だったら、そういう処理系を切り貼りしたり、魔改造したり、解析本を書いて出版できるような技能を身に着けたほうが仕事にもなるし喜ばれるかと思います。

##  ELENA 公式サイト

正直、古臭いですし、ドキュメントの統合性や保守性も悪くDRYの法則も守られていないのでイラッとします。ここは定石で [zola](https://github.com/getzola/zola) などのサイトジェネレータを導入したほうがいいと思うのですがね。マイナー言語の開発者はそういった「オレが作った」もの以外への投資 (スターゲイザー、名前を覚えてもらう仕掛けや工夫、そして知名度や開発参加者を増やすなどの流動的・客観的な成果物) は消極的であると思うことがあるため、目に見える成果や効果が実感しづらいものに対してはそれができないだけなんだろうと思います。

### それ以外の問題点: バラバラ

公式情報は検索性に劣ります。

まず、することとしてドキュメントやチュートリアルは Reddit や Wiki などバラバラに置かず、 mkdocs などを用いて elena-lang.github.io の docs 配下に集約してください。加えて API ドキュメントは自動生成で連携できるようしてください (実装のソースコード＝開発資料ではありません)。

言い出しっぺの法則やら待ち人は来ません。多くの場合、文句すら言うのも面倒くさいです。

フォーラムは Github の Discussion 機能を使いましょう。ユーザは面倒なことが嫌いなのに別のサービスに登録なんかしたがりません。

