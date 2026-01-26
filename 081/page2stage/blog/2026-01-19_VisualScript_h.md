# VisualScript.h の解析 Part 01

途中ですが、一旦ここで上げておきます。とまあ、ここからは地味に地道にといった作業が続きます。

自分で読むのと他所様(目の前のあなただけではなく、未来の自分もですよ)に説明するのとでは違うので、面倒だなあと思いつつゆるく進めていきますかね。


## なにをしているのか？

* インクルードガード
* 著作権情報
* インクルードファイルの指定
* バックアップファイルの拡張子定義
* FN_SIGNALOBJECTANDWAIT 型の定義
* _MB_RTL / _WS_RTL 変数の定義
* プロトタイプ宣言


# 全体の傾向と対策

古いソースコードなのでハンガリアン記法やら一見分かりづらい略記は当たり前です。おまけにソースコードのドキュメントもないのですよね。

C/C++は様々な歴史背景や利害関係、後方互換性ゆえにのハイコンテクスト言語なので致し方ないところ。

そういうのをいちいち調べながら細かいところまで読み解きながら説明するのは面倒ですが。

比較的環境を揃えやすいKIT Senaristから始めたほうがほうが良かったか(気づくのが遅い)。

説明にはオリジナル版のソースコード(Page2Stage.rar)を使います。ウチで使っているものだと整合性取れなくてややこしいので。


## インクルードガード用のプリプロセッサ命令 (#if defined 〜 #endif)

*  1, 2 行目 (ヘッダ)
``` cpp
#if !defined(AFX_VISUALSCRIPT_H__F23553B5_E4F8_11D1_A531_00600896C5B2__INCLUDED_)
#define AFX_VISUALSCRIPT_H__F23553B5_E4F8_11D1_A531_00600896C5B2__INCLUDED_
```

* 281 行目 (フッタ)
``` cpp
#endif // !defined(AFX_VISUALSCRIPT_H__F23553B5_E4F8_11D1_A531_00600896C5B2__INCLUDED_)
```

ただのインクルードガードです。ヘッダとフッタに記述しないと効果はありません。感嘆符がつくと否定形となり『〜が定義されていなければ』にな2行目のりdefinedの内容が定義されます (ifndef ディレクティブも同じ意味になります)。ようは、同じヘッダファイルが二度読み込まれると多重定義でエラーとなるため、このような仕組みがよく使われています。

AFX_ファイル名.拡張子__自動生成された十六進数文字列(生成規則不明)__INCLUDED_の内容は Visual C++ 6.0 側で自動生成されたものですので通常は気にしなくて問題ありません。

## 著作権情報

 * 3 〜 10行目
``` cpp

//---------------------------------------------------------------------------
//
//	Copyright (c) 1998 - 2000. Windward Studios, Inc.
//	All Rights Reserved.
//
//---------------------------------------------------------------------------

```

このソースコードの著作権表示です。原則として権利者の許諾がない限り通常は書き換えてはいけません。ただし、今回の場合はオープンソース版のため、現在のプロジェクト保守者(contributor.txt)やライセンス情報(license.txt)の追加あるいは加筆修正は必要になります。なんでオープンソース化する前に書き換えなかったのだ…ろう。


## ファイルの用途

*  11, 13 行目
``` cpp
// VisualScript.h : main header file for the VISUALSCRIPT application
//
```

このコメントは「VisualScript.h は VISUALSCRIPT アプリケーションのメインヘッダファイルである」程度の意味しかありません。VISUALSCRIPT (ビジュアルスクリプト)、あるいは Screen Writer Studio (スクリーンライタースタジオ)はもう使われていないファイルやアプリケーション名なのでリファクタリング対象です。これらすべては WxWidget への移植時に新ブランド名、または単純に Application へ書き換えます。

## インクルードガード

``` cpp
#if _MSC_VER >= 1000
#pragma once
#endif // _MSC_VER >= 1000
```

Microsoft Visual C++ 2005 以降であれはインクルードガード用のディレクティブである #pragma once ディレクティブを定義します。それ以下のバージョンか他社製品のコンパイラならば、1, 2行目のインクルードガードを適用します。どちらのディレクティブも競合しないのでディレクティブの違うインクルードガードが複数あっても問題ありません。


## MFC ヘッダファイルのインクルード確認

``` cpp
#ifndef __AFXWIN_H__
	#error include 'stdafx.h' before including this file for PCH
#endif
```

このファイルで使う PCH (コンパイル済みヘッダファイル)  をインクルードする前に stdafx.h (MFCのコアおよび標準コンポーネントである afxwin.h) をインクルードしておかないと、このエラーになります。もちろん、MFCを使わないのであれば不要です。


## インクルードファイルの指定

``` cpp
#include "resource.h"       // main symbols

#include "lists.h"
```

resource.hはWindowsリソースファイルで使われるリソースIDの定義、lists.h は Element 型リストデータ構造の処理用ですかね。今の段階で理解する必要はないです (こういうわからないことを今すぐ無理にわかろうとしないのとも場合によっては大事な戦略)。

## バックアップファイルの拡張子定義

``` cpp
const char savExt [] = ".sws0";	// save as editing
const char bakExt [] = ".sws1";	// previous version
```

文字列定数 (const) ですね。定数名(savExt, bakExt)に角カッコがついているたま char (キャラクター、文字列) 型の集合、つまり転じて文字列の扱いになります。

略記については、

1. sav: Save (保存)
2. bak: Backup (予備)
3. Ext: Extension (拡張子)

意味については、

* savExt: 編集中のファイルのバックアップを保存
* bakExt: 以前のバージョンのファイルのバックアップ

です。

## バグに関するコメント

``` cpp
// windbug - WalkAll* - move to windward, call member func instead of friend
// windbug - CBuf class to give a growing scratch buffer
```

windbugがなにを指すのかは Windows Bug なのか、あるいは Windward Library Bug なのか今となっては不明です。

* WalkAll* - move to windward, call member func instead of friend (Windward ライブラリへ移動、フレンド関連ではなくメンバー関数を呼び出してください)
* CBuf class to give a growing scratch buffer (動的割当バッファは CBuf クラスで実装)

バグトラッカーなんかもTracくらいでロクなものが無かった時代だから、ソースコードコメントに残すしかなかったのかもしれない。この手のコメントは信用ならないのものがある。コメントは最初は事実でも改訂され続け仕様が変わりやがてウソを付く。結局、ソースコードを確認するのが無難だろう。


## FN_SIGNALOBJECTANDWAIT 型の定義

``` cpp
typedef WINBASEAPI DWORD (WINAPI * FN_SIGNALOBJECTANDWAIT) ( HANDLE hS, HANDLE hW, DWORD dwM, BOOL bA );
```

使用箇所の前後関係 (kernel32.dllを呼び出すためにLoadLibraryを使うなど)、SignalObjectAndWait 関数の資料を参照すると意味は理解できるのですけど。なんか FN_ が付いているので、ハンガリアン記法で云う関数ポインタっぽい気もしますが。キャストまわりでこんがらがるので詳しく説明したほうがいいかなと (後で絶対忘れるヤツなので)。

ちょっとややこしいですが、分解すればなんとやら。

* typedef: 型の定義
* WINBASEAPI: __stdcall (winbase.h)
* DWORD: unsigned long (windows.h)
* WINAPI: __stdcall (WinDef.h)
* FN_SIGNALOBJECTANDWAIT: 型名
* HANDLE hS: SignalObjectAndWait - 引数
* HANDLE hW: SignalObjectAndWait - 引数
* DWORD dwM: SignalObjectAndWait - 引数
* BOOL bA: SignalObjectAndWait - 引数

丸括弧は両辺にありますが、左辺はWINAPI型のポインタからDWORD型のアドレス値へキャスト、右辺は引数ってだけのようです。関数ポインタ型ですからね。

方の定義後の使用時は m_fnSignalObjectAndWait 変数を定義してスクリプトの再整形処理の判定用に使われるようです。

意味がわからないときは使われているところに探りを入れるのが基本のようです。

関連: [Windows データ型 (BaseTsd.h) - Win32 apps | Microsoft Learn](https://learn.microsoft.com/ja-jp/windows/win32/winprog/windows-data-types)

## WM_ 定数

``` cpp
const int WM_MAX_CHILD = WM_USER + 2;
const int WM_INVALIDATE_REFORMAT = WM_USER + 3;
const int WM_REDRAW_REFORMAT = WM_USER + 4;
```

WM は Window Message の略語のような。調べてみると、カスタムダイアログで使うユーザーメッセージとのことです。WM_USERは推奨されておらずWM_APPを使えとのことです。

## _MB_RTL / _WS_RTL 変数の定義
``` cpp
// used for hebrew/arabic
extern UINT _MB_RTL;
extern UINT _WS_RTL;
```

ヘブライ語、アラビア語で使う変数です。範囲は MB_RTLREADINGなどの定数により変わります。

extern は外部公開シンボル、UINT は unsigned int です。

## プロトタイプ宣言

### DeleteProfileFolder 関数

レジストリ操作用の関数です。コードの実体は profile.cpp にあります。profile.hがないので、このヘッダファイルに定義されています。少々、定義場所としては不自然ですね。レジストリ操作用なら専用ファイル作って放り込みたいところです。

``` cpp
void DeleteProfileFolder ( LPCTSTR lpszSection, LPCTSTR lpszEntry );
```

* Delete (デリート): 削除
* Profile (プロファイル): 各種情報
* Folder (フォルダ)

* LPCTSTR: Long pointer to Const TCHAR String.
* lpszSection: セクション
* lpszEntry
 
* STR: String
* lpsz: **l**ong **p**ointer to **s**tring with **z**ero terminated (文字列型)

Windows API 特有のハンガリアン記法による命名規則です。いまではこの命名規則はほとんど使われてませんが、レガシーソフトウェアのマイグレーションでは見かけます。

もちろん、こういうのに耐性がない人は心が折れるかも知れれませんが、早見表は探すとありますので手元に置いておくと良いでしょう。

ちなみに、Windowsレジストリは使わなくなりBoostなど他の方法で実装しなおしますので、この関数も廃止になる予定です。レジストリの洗い出しは後程機会があれば。

#### WindowsレジストリAPI (winreg.h)

 * RegOpenKeyEx
 * RegCreateKeyEx
 * RegSetValueKeyEx
 * RegQueryValueEx
 * RegDeleteKey
 * RegCloseKey

いずれも使われているのは profile.cpp, about.cpp, about.h くらいです。

### win.ini を使う Windows API 関数

Windows 3.1 との互換性のために残されているものなので非推奨扱い。

 * GetProfileInt
 * GetProfileString
 * WriteProfileInt
 * WriteProfileString

現代の環境ではレジストリにマッピングされるようなので、レジストリとの差違は気にしなくていいかもしれない。

### クラス

``` cpp
class CDlgIntro;
class CStyle;
class CVisualScriptDoc;
class SE_Exception;
```

* C: Class
* Doc: Document
* Dlg: Dialog
* Intro: Introduction
* SE: Structur Exception
* Exception: 例外処理

CDlgIntro (DlgIntro.cpp, DlgIntro.h) は IDD_INTRO (VisualScript.rc) ダイアログを表示して使用方法に関する簡単な入門を案内します。

CStyleはドキュメントのスタイル(Style: 体裁、書式)に関する処理を行います。

CVisualScriptDocはドキュメントの処理全般を行います。

SE_Exception は Microsoft Visual C++ で使われている例外処理機構です。ほかのコンパイラでは使えませんし、すでにレガシーな方法なので C++標準例外機構や RAII など書き換えたほうが良いでしょう。

### その他関数

proppage.cpp, getdir.cpp, viewspell.cpp, sendmail.cpp

``` cpp
// stuff to move to windward.h
void GetDirectory ( HWND hPar, char const * sTitle, CString & sDir, BOOL bSetDir );
void GetValue ( CString const & str, int & val );
void SetValue ( CString & str, int val );
unsigned int atoh ( char const * str );
BOOL MyIsAlpha ( BYTE ch );
BOOL MyIsUpper ( BYTE ch );
BOOL MyIsLower ( BYTE ch );
BYTE MyToLower ( BYTE ch );
BYTE MyToUpper ( BYTE ch );
BOOL MyIsWordStart ( BYTE ch );
BOOL MyIsWordBody ( BYTE ch );
BOOL MyIsWordEnd ( BYTE ch );
void SendMail ( char const * to, char const * subj, char const * msg, char const * file );
```

* Get: 取得
* Set: 設定、定義
* Directory: ディレクトリ、フォルダ、階層構造のデータ表現
* Value: 値
* atoh: **A**SCII **t**o **H**exadecimal (ASCII文字から十六進数へ変換)
* My: 私家版、私の、独自の、私製の
* Is: 〜は (条件判定)
* To: 〜へ (データの変換)
* Upper: 半角英字大文字
* Lower: 半角英字小文字
* Word: 単語
* Start: 行頭、始点
* Body: 行中、本体
* End: 行末、終点
* Send: 送信、送る
* Mail: 手紙、郵便、電子メール

## CVisualScriptApp クラス

``` cpp
/ CVisualScriptApp:
// See VisualScript.cpp for the implementation of this class
//

class CVisualScriptApp : public CWinApp
{
```

アプリケーション本体となる CVisualScriptApp クラスのメンバ関数や変数のプロトタイプ宣言です。

See VisualScript.cpp for the implementation of this class は「このクラスのインプリメンテーション(コード本体、実装)はVisualScript.cppを参照せよ」程度の意味しかありません。

## フレンド関数のプロトタイプ宣言

``` cpp
friend void CatchSE ( SE_Exception e );
friend CDlgIntro;
```

* friend: C++ におけるオブジェクトのアクセス権限指定の変更子でありカプセル化の破壊や依存関係の複雑化など弊害により現代では推奨されていない。
* CatchSE: Catch a Structured Exception (構造例外の検出)
* CDlgIntro: 前述

## PreTranslateMessage のプロトタイプ宣言

``` cpp
public:

	virtual BOOL PreTranslateMessage(MSG* pMsg);
```

* public:C++ におけるオブジェクトのアクセス権限指定変更でありクラス外部に公開される。
* virtual: 仮想関数
* Pre: 事前に、前もって、準備処理、先行
* Translate: 変換、翻訳
* Message: 命令、情報、メッセージ、電文
* MSG*: メッセージ型のポインタ
* p: ポインタ
* Msg: Message の略記
* PreTranslateMessage: MFC の CWndクラスで使われているメソッド(PreTranslateAppMessageとは別物)
* virtual: 仮想関数

VisualScript.cpp 側にある実装はスプラッシュスクリーンで使われているだけめのメソッドのようです。CGがなんの略語(Class Generatorかな？)は現段階では不明です。

``` cpp
BOOL CVisualScriptApp::PreTranslateMessage(MSG* pMsg)
{
	// CG: The following lines were added by the Splash Screen component.
	if (CSplashWnd::PreTranslateAppMessage(pMsg))
		return TRUE;

	return CWinApp::PreTranslateMessage(pMsg);
}
```

## コンストラクタとデストラクタのプロトタイプ宣言

``` cpp
CVisualScriptApp ( );
	~CVisualScriptApp ( );
```

プロトタイプ宣言です。チルダがついてない方はコンストラクタ(初期化などの準備)、ある方はデストラクタ(片付け)

## メソッドのプロトタイプ宣言

``` cpp
void		GetStyle ( int ind, CStyle & pStyle ) const;
	void		GetDefaultStyle ( CStyle & pStyle ) const { GetStyle ( m_defaultStyle, pStyle ); }
	void		GetProfileData ( const char * section, const char * entry, void * def, void * data, int len );
	void		WriteProfileData ( const char * section, const char * entry, void * data, int len );
	void		GetDCSize ( CDC * pDC );
```

* Get: 〜を得る、取得する
* int: **Int**eger
* ind: **Ind**ex
* p: **P**ointer
* C: **C**lass, MF**C**, **C**haracter
* Default: 初期値、既定値、デフォルト
* def: **def**ault, **def**ine
* entry: エントリー項目、要素
* section: セクション
* size: 大きさ
* data: データ
* profile: プロファイル、ユーザー固有のソフトウェア設定情報
* len: Length
* void: 無形型
* m_: **m**ember of (例: 〜クラスのメンバー変数)
* Style: 体裁、スタイル
* const: **Const**ant
* DC: **D**evice **C**ontext

``` cpp
					// width only
	int			PixelsToCols ( int pix ) const { return ( pix * 10 ) / m_charWid; }
	int			ColsToHund ( int cols ) const { return ( cols * 10 ); }
	int			PixelsToColHund ( int pix ) const { return ( pix * 100 ) / m_charWid; }
	int			HundToCols ( int hun ) const { return hun / 10; }
	int			ColsToPixels ( int cols ) const { return ( cols * m_charWid ) / 10; }
	int			ColHundToPixels ( int hun ) const { return ( hun * m_charWid ) / 100; }
```
   
* Pixels, pix: ピクセル
* To: 〜から〜へ
* Cols: Column
* Hund, hun: **Hund**redths (小数点)
* Wid: **Wid**th, **Wi**n**d**ow
* 10, 100: マジックナンバー

文字幅の単位変換専用ワンライナー関数です。
恐らく、ピクセル ⇔ DPI(小数点)の相互変換だと思われます。なるほど、どのような歴史背景があるか理解していないとわからん(1980年代以前のコンピューターに関する知識がないと深堀りできない)。

``` cpp
					// printer
	int			ColHundToDevice ( int hun ) const { return ( hun * m_devWid ) / 100; }
	int			DeviceToColHund ( int pix ) const { return ( pix * 100 ) / m_devWid; }

					// pixels/inch
	int			_GetDevHt ( ) const { return m_devHt; }
	int			_GetCharHt ( ) const { return m_charHt; }
```

* Printer: プリンター、印刷機
* Col (Column): カラム
* To: 〜から〜へ変換
* Device, dev: デバイス、装置
* pixel, pix: ピクセル
* hun: hundredths
* 100: マジックナンバー (なぜそうなるかは保留)
* Char (Character): 文字
* Ht (Height): 高さ
* Wid (Width): 幅
* return: 返値

一般に接頭辞にアンダーバーが付いているのは低水準処理に使われる関数です。プログラマが直接呼び出すようなことはしません。

``` cpp
int			GetCharSet ( ) const { return m_charSet; }
	int			GetCodePage ( ) const { return m_codePage; }
	int			GetFontWeight ( BOOL isBold, BOOL isPrint ) const;
```

* CharSet: 文字コードセット (ShiftJIS, UTF-8 など)
* CodePage: コードページ (932など)
* FontWeight: フォントウェイト (書体の太さ)

``` cpp
	CString	MakeFileName ( CString name, char const * ext );
	void		WalkAllViews ( FN_WALK_VIEWS func, void * data );
	void		WalkAllDocs ( FN_WALK_DOCS func, void * data );
```

* Make: 作成、生成
* File: ファイル
* Name: 名、名前
* Walk: 走査、歩く
* All: すべて
* Views: ビュー、表示、表示領域
* Docs: ドキュメント
* ext: 拡張子
* data: データ
* func: 関数
* FN_WALK_VIEWS: 関数ポインタ (stdafx.h)
* FN_WALK_DOCS: 関数ポインタ (stdafx.h)

``` cpp
	void		SetStatusBar ( UINT id );
	void		SetStatusBar ( char const * str );
	void		FixDir ( CString & defDir, BOOL incSlash );
	CString	GetLang ( BOOL localLang );
	CString	IntToLangID ( int id );
	CString	GetDefFont ( ) const { return m_defFont; }
```

* Set: 設定
* Get: 取得
* StatusBar: ステータスバー
* Fix: 固定、修正
* Dir (Directory): ディレクトリ
* inc (Include): インクルード、含める
* Slash: スラッシュ記号
* Lang (Language): 言語
* local: ローカル、ロケール
* Int (Integer): 整数
* ID, id (Identifier): 識別子
* Def (Default, Define): デフォルト、定義
* str (string): 文字列
* Font: フォント、書体

SetStatusBarは二種類ありますけど、これはポリモーフィック(多態性)という仕組みで渡された引数で関数の動作を変える仕組みです。

``` cpp
	void		Log ( char const * str );
	CString	GetSystemSpecs ( );

	void		SetPrinterDefaults ( CVisualScriptDoc * pDoc, short orient = 0 );
	BOOL		isDemo ( ) const { return m_mode == demo; }
	BOOL		isRTL ( ) const { return m_bRTL; }
	BOOL		isRTLInput ( ) const { return m_bRTLInput; }
	void		_SetRTLInput ( BOOL val ) { m_bRTLInput = val; }
```

* Log: 動作状態などの記録して後で不具合などを検証できるようにするための機能
* System: システム
* Spec (Specification): スペック、性能、機器構成、仕様
* orient: 方向 (この場合は印刷用紙の縦横向き)
* RTL (Right To Left): 戦前の日本語など右から左へ読み書きする言語のこと。
* Demo: デモ版、試用版、体験版、評価版
* Input: 入力
* Mode: モード、状態、方式、形態
* b : Bool 型
* short: short int 型

## 仮想関数とメッセージマップなど

``` cpp
// Overrides
	// ClassWizard generated virtual function overrides
	//{{AFX_VIRTUAL(CVisualScriptApp)
	public:
	virtual BOOL InitInstance();
	virtual int Run();
	virtual int ExitInstance();
	//}}AFX_VIRTUAL
		```
	
* ClassWizard: クラスウィザード
* Instance: インスタンス
* Init (Initial): 初期化
* Exit: 終了、開放
* override: オーバーライド
* over: 超える、上に
* ride: 乗る、乗せる、覆う
	
仮想関数のオーバライド (上書き) ですね。
		
	``` cpp	
// Implementation
	void		ReadIniSettings ();
	void		RereadIniSettings ( BOOL doDict );

	//{{AFX_MSG(CVisualScriptApp)
	afx_msg void OnAppAbout();
	afx_msg void OnFileSaveall();
	afx_msg void OnUpdateFileSaveall(CCmdUI* pCmdUI);
	afx_msg void OnFilePrintSetup();
	afx_msg void OnFileOpen();
	afx_msg void OnWindowCloseall();
	afx_msg void OnHelpFaq();
	afx_msg void OnHelpUpdates();
	afx_msg void OnHelpWww();
	afx_msg void OnHelpTechSupt();
	afx_msg void OnHelpNews();
	afx_msg void OnUpdateDispStyle(CCmdUI* pCmdUI);
	afx_msg void OnFileNewScreenplay();
	afx_msg void OnFileNewSitcomFilm();
	afx_msg void OnFileNewSitcomTape();
	afx_msg void OnFileNewStage();
	afx_msg void OnUpdateFileNewScreenplay(CCmdUI* pCmdUI);
	afx_msg void OnUpdateFileNewSitcomFilm(CCmdUI* pCmdUI);
	afx_msg void OnUpdateFileNewSitcomTape(CCmdUI* pCmdUI);
	afx_msg void OnUpdateFileNewStage(CCmdUI* pCmdUI);
	afx_msg void OnUpdateFilePrint(CCmdUI* pCmdUI);
	//}}AFX_MSG
	DECLARE_MESSAGE_MAP()
```

* afx_msg: メッセージマップであることを意味する
* On: イベント発行時に呼び出される関数を表す接頭辞
* App(-lication): アプリケーション
* About: ソフトウェアに関する基本情報
* FAQ: よくある質疑応答
* Cmd (Command): コマンド、命令
* WWW: ウェブ
* Tech(-nical): テクニカル、技術
* Supt(Support): サポート、相談や問い合わせ
* News: 最新情報、ニュース
* Disp(-lay): 表示
* Re-: 再び、再度
* Style: スタイル、体裁
* Screenplay: 脚本
* Sitcom: コメディ、喜劇、漫才
* Film: 映画、番組
* Tape: 音声のみの媒体、ラジオ番組やオーディオドラマ
* Stage: 舞台
* Declare: 宣言
* Message: メッセージ
* Map: マップ、地図、割り当て、対応表、対応関係
* File: ファイル
* New: 新規
* Save: 保存
* Open: 開く
* Close:閉じる
* All: すべて
* Update: 更新
* Print: 印刷
* Setup: セットアップ、設定
* Help: ヘルプ
* Window: ウィンドウ

ウィンドウの大きさが変更されたりメニューから選択されたなどイベント発生時に呼び出されるコールバック関数ですね。

まだまだ続きますが、システム設定関連の変数は長文のため次回解説します。
