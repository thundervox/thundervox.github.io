# 2025年12月22日
MFC 6.0 からのマイグレーションで問題となる ConstructElements/DestructElements なんだけど、
Geminiに聞き直したら現行の Visual C+++なら勝手に内部処理されるから何も問題がなければ該当部分を削除すればいいだけってことらしい(あるいはコンストラクタやデストラクタに移動する)。んなわかるかッ。

それが本当なら大昔のWinSCPのソースコード読まなくて済むんでいいけど。いまのところ未確認ということで。

## 修正対象
* windward/music.cpp
* scene.h
* lists.h
* lists.cpp
* element.h
* music.h
* document.h
* para_doc.cpp
* element.cpp
* edit_doc.cpp
* page_doc.cpp

AFXAPIでgrepすると出てきます。

SerializeElementsは廃止されていませんので消さないように。

