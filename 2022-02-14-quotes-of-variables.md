# 2022年2月14日 - 変数の解説に関する引用
(この記事は Solar eClipse X で公開していた記事の再公開・加筆修正版です)

初学者向けの解説として納得がいかないので各所理系の説明書から引用してみます。

予定 (順次加筆予定)

 * BASIC-256
 * BlitzBASIC
 * ELENA
 * Dartmouth BASIC
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
URL: https://github.com/eantcal/nubasic

```
A variable is a storage location paired with an associated symbolic name called identifier.
Variables allow you to store and change information.
NUBASIC USER'S GUIDE p.33 より引用 (GFDL 1.3)
```

### 粗訳
変数は識別子と呼ばれるシンボル名に関連付けられた記憶領域を組み合わせた〔構成される〕ものである。変数はユーザによる情報の記録と変更ができる。


## 参考文献

 * [まだたとえ話で消耗してるの? - K.Maebashi's はてなブログ](https://kmaebashi.hatenablog.com/entry/20160717/)
 * [変数を箱ではなく付箋で説明してみた（初学者向け） - Qiita](https://qiita.com/yuma-ito-bd/items/c118c637962d34ec51af)

