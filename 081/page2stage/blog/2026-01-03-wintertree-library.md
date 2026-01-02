# 2026年1月3日 - Wintertree ライブラリ関連

これさえ済めばデッドコードの削除は峠を超えたことになる。

## どこでなにを削除する

スペルチェッカーとシソーラスエンジンを使っているソースコードを見つけてデッドコードを削る。

該当ファイルは、
* about.cpp
* DlgThes.h
* StdAfx.h
* view.h
* view.cpp
* viewchar.cpp
* viewspell.cpp
* SpellCheck.h
* SpellCheck.cpp
* options.h
* options.cpp
* ssce.h
* Thesdb.h
* VisualScript.cpp
* VisualScript.rc


## Wintertree API

* 接頭辞 SSCE_, ThesDB_ などで始まります。S16などもあり。


### 関連資料

 *
 * 

## 将来の予定

* デッドコード削除後にリライトをして無事にビルドできるようになってからスペルチェッカーの再実装
* スペルチェッカーエンジンはHunspellなど
* シソーラス(類義語、同義語)はOpenThesaurusやWordNetベースで再実装


