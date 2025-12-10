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
* games.h
* ptr.h
* datafile.h
* dlgmsg.h
* fixpoint.h
* init.h
* rand.h
* threads.h
* _msgs.h
* _error.h
* _help.h
* logging.h
* _debug.h
* codec.h

gg.hはダミーファイルのため除外

### codec.h
オーディオコーデック関連ですね。CoDecでgrepする限り、Page 2 Stage での利用状況は無いようです。

## Page2Stage専用リポジトリの準備
読みづらいので作ることに。あとで準備ができたら公開予定です。元々のアーカイブには不要なファイルが大量にあるので、そういうものを除外しないと容量食います。

ライセンスは Mozilla Public License 2.0 にしておきます。
なお、 Mozilla Public License 1.1 からのアップグレードは第三者が無許可で行っても合法であり問題ないです→[About MPL 2.0: Revision Process and Changes FAQ — Mozilla](https://www.mozilla.org/en-US/MPL/2.0/Revision-FAQ/)
