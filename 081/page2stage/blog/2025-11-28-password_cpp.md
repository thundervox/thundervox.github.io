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

VisualScript.cpp: 484行目付近
``` cpp
m_mode = std;
Log ( "Mode " + IntToCString ( m_mode ) );
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

### theApp.isDemo
削除対象はかなり多いなあ。そしてかなりいやらしいところに幾重にも記述されているんでクリーンアップするのが面倒なやつ。
デモ版関連のコードを書き換えて綺麗さっぱりにしても、今度はスペルチェッカーを一時的に削除する必要があってちゃんとビルドできるようなるまで時間かかるんよね。どおりで誰も手をリライトは出したがらないわけです。仕方ないので年単位でやっていきますか。


