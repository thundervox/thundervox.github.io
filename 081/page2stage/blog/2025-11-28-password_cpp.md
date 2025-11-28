# 2025年11月28日(金) - password.cpp
シェアウェア版で使われていたパスワード生成器なんですが、オープンソース版では不要なのでコメントアウトできないかなと試行錯誤してみます。

## 探しものはなんですか？
password.cpp にある BuildPasswordが本体です。
コイツを改造してやればパスワード生成器が作れますけど割愛。
生成アルゴリズムは興味がないので読み飛ばし。

この関数を参照しているのは、

stdafx.h: 58行目
``` cpp
CString BuildPassword ( char const * name );
```

VisualScript.cpp: 484行目付近
``` cpp
if ( ( m_sUserName.GetLength ( ) > 0 ) && ( m_sUserPW.GetLength ( ) > 0 ) && 
																		( BuildPassword ( m_sUserName ) == m_sUserPW ) )
```
です。ようするに、password.cppのダミーを作るかファイルを削除して、各所のコメントアウトや書き換えを行うとパスワードは要求されなくなるってことです。
もちろん、デモ版モードのコードは未だ残っていますので完全に綺麗になっていませんが。

現状は stdafx.h のコメントアウトと password.cpp の削除を行うだけにします。
VisualScript.cppのif周りの書き換えなど続きは後ほど。
