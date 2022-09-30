# 2022年2月14日 - 変数の解説に関する引用
(この記事は Solar eClipse X で公開していた記事の再公開・加筆修正版です)

巷に流布されている初学者向けの解説として「ハコとワイシャツとワタシ」ってのが絶対納得がいかないので各所理系の説明書から引用してみます。

予定 (順次加筆予定)

 * RCBasic
 * BASIC-256
 * BlitzBASIC
 * Dartmouth BASIC
 * ELENA
 * nuBASIC
 * など。

## FORTRAN
黎明期の取扱説明書 (IBM704 用) はあるようです。入手できたら調べてみます。

URL: https://www.ibm.com/ibm/history/ibm100/us/en/icons/fortran/breakthroughs/

## Dartmouth BASIC (1964)
[ダートマス BASIC](https://www.dartmouth.edu/basicfifty/basic.html)の初版説明書において、変数は、

```
LET 変数 = 数式
```

の説明しかありません。そんなわけで、少なくとも 1964 年の時点では、変数をハコに例えるような事実は確認できません (TrueBASIC は除く)。

また、イコールを等号と頑なに決めつける異常な初学者もいなかったようです (筆者はプログラミングを始めてこのかた、そんな人に出会ったことがありません。そんなことを言い出したのは15世紀から生きている怪異か異世界人でしょうか？)。

## nuBASIC 1.48
URL: [https://github.com/eantcal/nubasic](https://github.com/eantcal/nubasic)

```
A variable is a storage location paired with an associated symbolic name called identifier.
Variables allow you to store and change information.
```
NUBASIC USER'S GUIDE p.33 より引用 (GFDL 1.3)

### 粗訳
```
変数は識別子と呼ばれるシンボル名に関連付けられた記憶領域を組み合わせた〔構成される〕ものである。
変数はユーザによる情報の記録と変更ができる。
```


## RCBasic
URL: [https://www.rcbasic.com/](https://www.rcbasic.com/)

```
To store "Bob" (or whatever you call yourself) we use something called a variable.
You might have seen variables used in math class in school.
A variable is just a symbol that holds data.
By symbol I don't mean a logo or anything.
```
RCBasic v3.17 Manual より引用 (Zlib ライセンス)

### 粗訳
```
"Bob" (あるいは自分自身の名前) を保持するには変数を使います。
学校の数学授業で変数が使われているのを見かけたことがあると思います。
変数はデータを保持するためのシンボル (表象、記号) です。
シンボルには、ロゴ (合言葉) や何らかの意味があるわけではありません。
```


## BASIC-256
```
In computer program a variable is "a quantity or function that may assume any given value or set of values."
To describe it another way, we can think of a variable as name for a reserved location in the computer's temporary memory. 
We may store, change, and retrieve values from this location as our program runs by using the variable name.
```
[So You Want to Learn to Program – BASIC-256 (Third Edition) - Chapter 3 – Variables](https://syw2l.org/) より引用 (Creative Commons Attribution-Noncommercial-Share Alike 3.0 United States)

### 粗訳
```
計算機プログラムにおいて、変数とは「値の指定や値の設定をするための数量や機能である」と考えられます。
違う言いかたをすると、計算機の一時作業用メモリ内で予約済みの記憶領域に名前を与えたものが変数であると考えられます。
変数名を使うことでプログラムの実行中に該当領域で値の保存、変更、そして取得が可能になります。
```


## まとめ

### シゲルボックス
「箱」や「おなじない (シギル)」なんて書いてある本だいたい悪書。
そもそもメモリは連続した領域なので箱ではない。なんというかメモリセルを本箱に喩えた時点で劣化コピーが生じて箱になったのかもしれまあ線。

メモリはキャッシュレジスタでよく使われる熱転写ロール紙を仮想化したものに近い。

 * メモリは使えば使うほど減る (解放しなければ空き領域は戻らない)。
 * 印刷時、限られた範囲で印刷して用紙を切る (先頭アドレス、データ、ナル終端文字)。
 * 解放すれば空き用紙量は部分的に回復する。ただし、空き用紙をつぎはぎして使用中のロール紙に接続するため断片化が発生する。
 * ロール紙とは異なりメモリはランダムアクセスができる。

ちょっと違う。これもダメな解説ですね。実際に説明するとしたらメモリシミュレータ、マスキングテープやカラー紙テープを使ったほうがわかりやすいかもしれない。

本職のプログラマであっても自作言語を組むまで変数についてよくわかってないで使いこなしている人はいますから、下手に恐れなくていいです。


### 初心者にとってわからないと思うこと

 * 変数、代入、宣言など数学用語からの借用語による混乱 → プログラムと数学は別物です。同音異義語であると考えたほうが楽です。
 * どこに変数が記録されるのかわからない (ブラックボックス化) → メモリで予約された一時作業用域です。どこか暗くてジメジメした洞窟に保存されるわけではありません。
 * イコールは値を割り当てたり比較するためのものではなく答えでしょ？ → 数学からの概念の借用にすぎません。混同しないでください。
 * あたらしい用語が現れた！  痛恨の一撃！ 〇〇は挫折した…… → 言語読解能力の問題。SNS ばかりではなく、ちゃんとした読書をしましょう。
 * わからん×9999 → 実際に検証用コードを書いて 9999 回試行錯誤してください。そうすれば概念や機能、用法は理解できるでしょう (つまり、他人が何とかしてくれると勘違いした上での練度不足)。


## 参考文献

 * [まだたとえ話で消耗してるの? - K.Maebashi's はてなブログ](https://kmaebashi.hatenablog.com/entry/20160717/)
 * [変数を箱ではなく付箋で説明してみた（初学者向け） - Qiita](https://qiita.com/yuma-ito-bd/items/c118c637962d34ec51af)
 * [ヒープとスタック｜学校では教えてくれないこと｜［技術コラム集］組込みの門｜ユークエスト](https://uquest.tktk.co.jp/embedded/learning/lecture16.html)
 * [プログラムがメモリをどう使うか理解する(1) - rita (Zenn)](https://zenn.dev/rita0222/articles/e6ff75245d79b5)
 * [プログラムがメモリをどう使うか理解する(2) - rita (Zenn)](https://zenn.dev/rita0222/articles/beda4311d9a6bf)
 * [プログラムがメモリをどう使うか理解する(3) - rita (Zenn)](https://zenn.dev/rita0222/articles/f59b79bab45a2a)
 * [プログラムがメモリをどう使うか理解する(4) - rita (Zenn)](https://zenn.dev/rita0222/articles/1f37a5bf910282)
