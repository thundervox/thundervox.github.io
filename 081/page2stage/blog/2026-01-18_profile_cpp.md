# 令和8年1月18日 - profile.cpp

## 用途
レジストリ操作関連ですね。ほかにもあるようですが。
シェアウェア関連のコードを削ると以下を除き不要になるようです。

* myRegisterFileTypes: ファイル拡張子の登録
* DeleteProfileFolder: スタイルやリスト関連のレジストリ登録削除
* myWriteProfileString: レジストリエントリーの書き込み

オープンソース版ではmyGetProfileInt, myGetProfileString, myWriteProfileInt は使われなくなる予定です。

## レジストリ操作で使われるデータやメンバ変数は？

VisualScript.h などに記載されています。

