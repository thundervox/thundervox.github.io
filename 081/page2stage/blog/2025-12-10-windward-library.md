# 2025年12月10日 - Windward ライブラリ

## デッドコード

Page 2 Stageから参照すらほぼされていないデッドコードの塊なので猫ミーム再来ですよ。なので一旦削除してビルドエラーが出たら拾って書き直し方針でいいでしょう。
とまあ、軽くgrepしてみたが Page 2 Stage から参照されているクラスなど見つからない。もしかして、最終版あたりでは全く使われていない気がするんですけど。どうしたものか。

## 読む？　処す？
全部デッドコードの恐れもあるので後回しにするのが無難かと。コイツを印刷してポールペン片手に解析するのは紙の無駄です。後で役に立つかもしれないからと今必要でもない無駄なコードを読むのもエネルギーがいるんですよ。消耗している場合ではないんですよね。やるなら期限決めて超えたら一旦終了でいいと思います。

## 読む？　そしてメモする。

windward.h からインクルードファイルしている
ヘッダファイルとPage2Stageでの利用状況(暫定)

* thielen.h
* games.h: ✕
* ptr.h: ✕
* datafile.h: ✕
* dlgmsg.h:
* fixpoint.h
* init.h
* rand.h
* threads.h
* _msgs.h
* _error.h
* _help.h
* logging.h: ✕
* _debug.h
* codec.h: ✕

gg.hはダミーファイルのため除外

使われているとしたら汎用マクロや演算子のオーバーライドあたりでしょうか。

### games.h
インデックスカラーパレット関連ですね。CColorでgrepしても見あたらないです。

### codec.h
オーディオコーデック関連ですね。CoDecでgrepする限り、Page 2 Stage での利用状況は無いようです。ほかに圧縮アルゴリズム関連もインクルードしていますが、まったく使われていません。

## Page2Stage専用リポジトリの準備
読みづらいので作ることに。あとで準備ができたら公開予定です。元々のアーカイブには不要なファイルが大量にあるので、そういうものを除外しないと容量食います。

ライセンスは Mozilla Public License 2.0 にしておきます。
なお、 Mozilla Public License 1.1 からのアップグレードは第三者が無許可で行っても合法であり問題ないです→[About MPL 2.0: Revision Process and Changes FAQ — Mozilla](https://www.mozilla.org/en-US/MPL/2.0/Revision-FAQ/)

### ディレクトリ構成
KITScenarist, Scrite などを参考にして、page2stage.rarから変更して現代的な構成(build, data, doc, src, ui) にします。将来的にMFCやめたりユーザインタフェースからコードを分離する必要もありますから。

## 当面の対応
リポジトリには　Windwardフォルダはそのまま持ってこないでダミーファイル(windward.cpp / .h)でも作って様子見ですかね。まだまだ動かせる段階ではないので。こうするとリポジトリ構成もスッキリしますからね。

## 追記: 2025年12月16日
リポジトリ立ち上げてコード検索しまくってますが、使用箇所は全く見当たらないみたいです。なんか、Windwardライブラリの開発経緯はWindwardStudio社内で使われているソフトウェアコードの共通化と移植性(CDIBクラスはWinG, DIB, DirectXの共通ラッパーにしようとしたみたい)の向上のような感じがありますけど、開発中止した感じですね。で、Page2Stageもその流れが来るとは思いきや開発終了となりコードの整理もままならないまま我々を苦しめる結果となっているわけですか。

* ビルドできないコードはオープンソースにする前に現行のシステムでビルドできるようにしてから公開する。
* 使わないコードは添付しない。基本ですね。


## 使われているとこ？
* VisualScript.cpp: IntToCString, LongToCString (strext.cpp), __minmax (thielen.h), verify_minmax (thielen.h), のみ。GetLength (thielen.h) はMFCとメソッド名は同じですが実際は使われていません。

## 2026年1月3日 追記

色々と調査したところ、 Page 2 Stage では
thielen.h, strext.cpp しか使われていません。その中で使われているインラインマクロや関数は、

* __min, __max, __minmax, __roll, verify_minmax
* IntToCString, LongToCString
* CStringInsert, CStringDelete, InsComma
* csPrintf

のみです。この部分をうまく切り貼りしてやれば Windward Library は不要になると思います。

これで Windward 関連のデッドコード削除は終了となります。
