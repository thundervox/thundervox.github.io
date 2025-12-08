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

VisualScript.cpp: 484 〜 516 行目付近
``` cpp
// see if we are demo
	m_sUserName = GetProfileString ( "User", "Name", "" );
	m_sUserPW = GetProfileString ( "User", "Password", "" );
	if ( ( m_sUserName.GetLength ( ) > 0 ) && ( m_sUserPW.GetLength ( ) > 0 ) && 
																		( BuildPassword ( m_sUserName ) == m_sUserPW ) )
		m_mode = std;
	else
		{
		// check for 1 month old
		int expire = myGetProfileInt ( HKEY_CURRENT_USER, "SOFTWARE\\Microsoft\\xCompatibility", "xDOS", -1 );
		CTime t = CTime::GetCurrentTime ( );

		// expire if we are over 6 months old or 1 month of demo
		// bugbug - 2 different dialog boxes
//		CTime tMax ( DEMO_YEAR_END, DEMO_MONTH_END, DEMO_DAY_END, 0, 0, 0 );
//		if ( ( t >= tMax ) || ( ( expire != -1 ) && ( expire < t.GetTime ( ) ) ) )
		if ( ( expire != -1 ) && ( expire < t.GetTime ( ) ) )
			{
			CDlgExpired dlg;
			dlg.DoModal ( );
			return FALSE;
			}

		if ( expire == -1 )
			{
			// set up to expire in a month
			CTime t = CTime::GetCurrentTime ( );
			myWriteProfileInt ( HKEY_CURRENT_USER, "SOFTWARE\\Microsoft\\xCompatibility", 
																				"xDOS", t.GetTime ( ) + 30 * 24 * 60 * 60 );
			}

		// tell them to buy
		CDlgDemo dlg;
		if ( dlg.DoModal ( ) != IDOK )
			return FALSE;
		}
	Log ( "Mode " + IntToCString ( m_mode ) );
```
です。ようするに、password.cpp のダミーを作るかファイルを削除して、各所のコメントアウトや書き換えを行うとパスワードは要求されなくなると思います。

VisualScript.cpp: 92行目付近の書き換え
``` cpp
m_mode = std; // demo → std でデモ版モードの解除
```

VisualScript.cpp: 484〜510行目付近の削除
``` cpp
Log ( "Mode " + IntToCString ( m_mode ) );
```

VisualScript.cpp: デバッグ用コードの削除(保留)
``` cpp
ASSERT ( ( 0 <= m_mode ) && ( m_mode <= 2 ) );
```

VisualScript.cpp: デモ版用コードの修正 - RTF形式での保存制限解除 (保留)

``` cpp
// can't save RTF if demo
if ( pDoc->IsModified ( ) && ( ( pDoc->m_fileType == CVisualScriptDoc::TYP_VS ) ||
	( ( ! pDoc->isDemo ( ) ) && ( ! isDemo ( ) ) ) ) )　// この isDemo 行を修正
pDoc->SaveToFile ();
```
							
もちろん、単純にバイパスするだけであってデモ版モード(m_mode 変数や不要になったメソッドやダイアログなど)のコードは未だ残っています。完全に綺麗になっていませんが、これで  password.cpp ファイルの削除と stdafx.h のプロトタイプ宣言は削除できると思います。

次回は不要箇所の削除に関して調べてみます。

* m_mode
* m_demo
* m_sUserName, m_sUserPW: これはVisualScript.cpp で起動時のユーザ登録以外使われていないので削除
* USER_MODE
* isDemo
* theApp.isDemo: 各所に入る正規ユーザ登録確認判定。これが地味に面倒くさい。
* GetProfileString: レジストリ操作関連(Win32API専用のためマルチプラットフォーム化ではTOML形式などへの対応予定)
* myGetProfileInt
* myWriteProfileInt
* CDlgExpired, CDlgDemo, CDlgRegister: about.cpp / .h にあります。
* CDlgDemoEnd: frame.cpp の 303 行目以外では見当たりません。該当箇所のコメントアウト後に CDlgDemoEnd.cpp / .h は削除できるかもしれません。
* IDS_DEMO_*
* IDD_DEMO
* IDD_EXPIRED

### isDemo / theApp.isDemo
削除対象はかなり多いなあ。そしてかなりいやらしいところに幾重にも記述されているんでクリーンアップするのが面倒なやつ。
デモ版関連のコードを書き換えて綺麗さっぱりにしても、今度はスペルチェッカーの一時廃止、デッドコードだらけの Windward ライブラリの削除、ヘルプファイルシステムの近代化(Winhelpからmkdocsなど)、加えて VisualStudio 2022 でビルドできるようにコードの書き換えやユニットテストやソースコードドキュメントの導入(doxygen)など、ちゃんと現行環境で動くようになるまで時間かかるんよね。再実装作業は大変なのに表向きは変わらない。どおりで誰も手をリライトは出したがらないわけです。これがオープンソース化する前に原作者側でしっかりしバトンを渡せるようMinGWやオープンソースのフレームワーク対応など書き直していたら歴史はかなり違ったかもしれませんね (ビルド要件を揃えるのが厳しいなど壊れたソースコードはメンテできない)。仕方ないので年単位でやっていきますか。

## Windward ライブラリ

Page 2 Stageから参照すらされていないデッドコードの塊なので猫ミーム再来ですよ。なので一旦削除してビルドエラーが出たら拾って書き直し方針でいいでしょう。コイツを印刷してポールペン片手に解析するのは紙の無駄です。後で役に立つかもしれないからと今必要でもない無駄なコードを読むのもエネルギーがいるんですよ。消耗している場合ではないんですよね。

### さらに MFC がらみ。
ビルドログ残っていたので眺めてみる。これはビルドできないね。 ConstructElements と DestructElements は Visual C++ 2003 以降で廃止されているため、KB318734を参考に書き換える必要あり。そりゃあ、誰もしたがらないわけよね。

* [Convert C++ from VisC++ 6 to VS 2008 [modified] | Code Project Forum](https://forum.codeproject.com/topic/400433/convert-c-from-visc-6-to-vs-2008-modified/)
* [ConstructElements and DestructElements are deprecated in Visual C++ .NET and in Visual C++ 2005](https://web.archive.org/web/20111228042454/http://support.microsoft.com/kb/318734)

なんかさ。当時のWindwardStudioはなんかあったっぽい気がするんですけど。そうでなければ、こんな壊れたままのコードを出すのはおかしいんですよね。

## 作戦変更
いちいち注釈書きながらデモ版のコード取り除く方法について解説するのも面倒ですし読んでいる方もあまり面白くはないと思うので、原版と変更後のソースコード上げるか専用のリポジトリでも用意したほうが良さそうですね。

