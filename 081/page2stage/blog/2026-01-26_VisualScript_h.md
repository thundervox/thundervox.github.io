# 令和8年1月26日

## オプション関連の変数

用途はコメントに書いてあるので英語が読めない読もうとしない初心者さん、通信容量無制限が使えない方、宗教上の理由でAIチャットやバイブコーディング環境が使えない零細限界プログラマ向けに逐一説明しなくてもいい気がしますが⋯⋯。そういう人はこんなところ読んでませんし、そもそもウェブ検索には引っかからないほどこのプロジェクトのディレクトリ階層は深めですからね。

``` cpp
public:
	// data set in options
	BOOL			m_autosaveOn;						// do autosave
	int				m_secIdleSave;					// save if N seconds idle
	int				m_minForceSave;					// force save every N minutes
	BOOL			m_backupOn;							// create backup file when saving
	CString		m_backupDir;						// directory to put backup in (can be ".\")
```

 * do: 〜をする
 * if: 〜もし〜ならば
 * On: 機能の有効化、オンにする、電源を入れる
 * when: 〜である時、であるならば、の場合
 * auto: 自動
 * save: 保存
 * force: 強制的に、自動で
 * every: 〜おきに、〜ごとに、〜経過するたびに、〜後に
 * N: Number (数値) の略記
 * sec (seconds): 秒
 * minutes: 分
 * idle: アイドル、無操作待機状態、見てるだけ
	
``` cpp
	BOOL			m_selWord;							// select entire word with mouse
	BOOL			m_over;									// start in overwrite mode
	BOOL			m_repSel;								// typing replaces selection
	int				m_startDoc;							// start w/ nada, new doc, last doc
	CString		m_scriptDir;						// default directory for scripts
```

* sel (select, -ion): 選択
* entire: 全体、全部
* word: 単語
* with: 〜で
* mouse: マウス
* over: 超える、上に
* overwrite: 上書き
* start: 開始
* typing: 打鍵
* w/ : with の省略形
* nada (r): 何もしない
* new: 新規
* last: 最後
* doc (document): ドキュメント
* rep (replace): 置換
* script: スクリプト、脚本

``` cpp
	BOOL			m_autoSpell;						// spell check as type
	BOOL			m_suggestSpell;					// suggest corrections
	BOOL			m_spellIgnoreUC;				// ignore all uppercase words
	BOOL			m_spellIgnoreNum;				// ignore words with numbers
	BOOL			m_corr2Caps;						// correct words with 2 initial caps
	BOOL			m_corrCapSent;					// capitalize the first letter of a sentence
	BOOL			m_corrCapsLock;					// fix caps lock reversed
	BOOL			m_insSpacesSentEnd;			// add spaces at a sentence end
	int				m_numSpacesSentEnd;			// number of spaces after a '.'
	BOOL			m_charNames;						// do we show these lists/check for words?
```
	
* auto: 自動
* add: 追加、書き足す
* end: 最後、末尾
* Char (Character): 文字
* Spell: つづり、スペル
* check: 検査、確認、判定
* type: 種類、字種
* after: 後に
* do: 〜を行う、処理する
* show: 表示
* list: リスト、一覧
* we: 我々は(プログラマ側では)
* suggest: 示唆、候補
* corr, corrections: 訂正
* UC (Uppercase): 大文字
* ignore: 無視
* Num (Number): 数字、数値
* initial: 頭文字
* Cap (-s), capitalize: 大文字にする
* Lock: 固定、保持
* fix: 修正
* reverse: 反転、逆
* first: 頭、一、先頭、最初
* letter: 文字
* ins (Insert): 挿入
* Spaces: スペース、空白文字、一文字空ける
* sentence, Sent: センテンス、文

``` cpp
	BOOL			m_charExt;
	BOOL			m_sceneLoc;
	BOOL			m_shots;
	BOOL			m_timeOfDay;
	BOOL			m_trans;
	BOOL			m_fadeIn;
	BOOL			m_sceneHdr;							// last do we show
	BOOL			m_altDual;							// alt dual cols
	BOOL			m_propFonts;						// allow proportional fonts
```

* Ext (Extensions): エクステンション (技術上の注釈)
* Loc (Location): 場所、ロケーション
* Shot: 場面、ショット
* fadein: フェードイン
* trans (Transitions): 遷移、トランジション
* prop: プロポーショナル、等幅
* Hdr (Heading): ヘッダー
* time: 時
* Of: の
* Day: 日
* Dual: 両面、両側、双頭
* cols (Columns): カラム
* alt: 別の、代替の
 
``` cpp
	CString		m_sUserName;						// copy protection
	CString		m_sUserPW;
```

* User: ユーザー、利用者
* Name: 名前
* PW: パスワード
* copy: コピー、複製
* protection: 保護、防止

``` cpp
	// other misc global data
	int				m_defaultStyle;					// default style to use
	int				m_selWidth;							// width of selection area on left to select line
	int				m_selHeight;						// height of area between pages drawing page view
	CBrush		m_selBrush;							// color for selection area
	CBrush		m_faceBrush;						// button colors
	CBrush		m_lightBrush;						// button colors
	CBrush		m_shadowBrush;					// button colors
	CPen			m_outlinePen;						// lines in outline view

COLORREF	m_clrNotePos;
	COLORREF	m_clrAutoPrompt;
	COLORREF	m_clrAutoText;
```

* other: その他
* misc: 雑多な
* global: グローバル、全体、大域
* data: データ、情報
* default: デフォルト
* Style: スタイル
* width: 幅
* Height: 高さ
* select (-ion): 選択
* area: エリア、領域
* on: の上で
* left: 左
* to: 〜から〜まで
* line: 行
* between: の間
* drawing: 描画する
* page: ページ
* view: ビュー、表示
* face: フェイス、顔、前面
* light: ライト、明るい面
* shadow: シャドウ、陰影
* button: 押しボタン
* outline: アウトライン
* clr, colors: カラー、色
* Pen: ペン、筆
* Brush: ブラシ、刷毛
* CBrush: MFC
* CPen: MFC
* COLORREF: Win32 / DWORD 型 - Windef.h (Windows.h)
* Auto: 自動
* Pos: Properties, Proportional, Position, Post (類推不能)
* Note: 備考、注釈、注意、ノート
* Prompt: プロンプト
* Text: テキスト、文書、本文

``` cpp
	int				m_regFontWt;						// font weights
	int				m_boldFontWt;
	int				m_regPrnFontWt;
	int				m_boldPrnFontWt;
```

* reg (regular): レギュラー、通常
* bold: ボールド、太字
* Prn (Proportional): プロポーショナル、等幅
* Font: フォント、世帯
* Wt (Weight): ウェイト、太さ

``` cpp
	// prop sheet pages to start on
	int				m_listDlg;							// CDlgList
	int				m_scrListDlg;
	int				m_optnDlg;							// CDlgOption

	UINT			m_cfRTF;								// clipboard formats we need to create
	UINT			m_cfVS;

	CString		m_exeDir;								// dir the EXE file is in
	CString		m_userDir;							// user dir 
	CString		m_defDir;								// default dir when starting
	CString		m_stylDir;							// dir for styles
```

* prop (Properties): プロパティ
* sheet: シート、台紙、薄い紙
* start (-ing): 開始
* need: 必要
* create: 作成
* scr (Script): 脚本 
* List: リスト
* Dlg (Dialog): ダイアログ
* optn (Option): オプション
* cv (clipboard formats): クリップボード形式のデータ
* RTF (Rich Text Format): リッチテキスト形式のデータ
* CVS (Comma Value Separate): カンマ区切り値形式のデータ
* def (default): デフォルト
* sty (Style): スタイル
* exe (executable): 実行可能形式
