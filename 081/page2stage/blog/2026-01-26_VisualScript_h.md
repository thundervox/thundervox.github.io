# 令和8年1月26日

## オプション関連の変数

用途はコメントに書いてあるので英語が読めない読もうとしない初心者さん、楽天モバイルなどの通信容量無制限が使えない方、宗教上の理由でAIチャットやバイブコーディング環境が使えない零細限界プログラマ向けに逐一説明しなくてもいい気がしますが⋯⋯。そういう人はこんなところ読んでませんし、そもそもウェブ検索には引っかからないほどこのプロジェクトのディレクトリ階層は深めですからね。

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

