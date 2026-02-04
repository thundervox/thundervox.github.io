# 命名規則早見表 (未完成)
Naming Convention

あまりの資料の無さはしかたないのですが、同じことは二度も書きたくないので、意味や読み方がわからないなら、この早見表を手掛かりにしましょう。

ぼやき: なんだこれは。略語の一義性なんてあったもんじゃないぞ。リファクタリングだ。


## 接頭辞・接尾辞

| 略式 | 正式 |
| ----- | --------- |
|  a    | **A**SCII |
| afx | **A**pplication **F**ramework e**X**tensions |
| alt | **Alt**ernative |
| App | **A**pplication |
| b | **b**ool, **b**oolean |
| btn | **B**utto**n** |
| Buf | **Buf**fer |
| C    | **C**lass, MF**C**, **C**haracters |
| Cap, caps | **Cap**tion, **Cap**ital (-s, -ize)  |
| cf | **c**lipboard **f**ormats |
| CG | **C**ode **G**enerator/Wizard |
| cmb | **C**om**b**o **B**ox ||
| Cmd | **Com**man**d** |
| Cols | **Col**umn**s**, **Col**or**s** |
| clr | **C**o**l**o**r**, **Cl**ea**r** | 
| corr | **Corr**ect |
| CVS | **C**omma **V**alue **S**eparate |
| dev | **Dev**ice, **Dev**elop (-er/-ment) |
| def | **def**ault, **def**ine |
| DC | **D**evice **C**ontext |
| Dict | **Dict**ionary|
| Dir | **Dir**ectory |
| Disp | **Disp**lay |
| do | do |
| dw | **dw**ord, **D**ouble **W**ord |
| Dlg | **D**ia**l**o**g** |
| DX | **D**ata e**x**change |
| DDX | **D**ynamic **d**ata e**x**change |
| DDV | **D**ynamic **d**ata **v**alue |
| Ext | **Ext**ension, **Ext**ernal, **Ext**erior |
| exe | **Exe**cut (-e, -able) |
| h    | **H**exadecimal, **H**andle, **H**eader flie |
| Hdr | **H**ea**d**e**r** |
| Ht   | **H**eigh**t** |
| Hund | **Hund**redths |
| inc | **Inc**lude |
| int | **Int**eger |
| ins | **Ins**ert |
| inst | **Inst**all, **Inst**ance |
| ind | **Ind**ex |
| IDC | Resource ID of Constant? |
| IDD | Resource ID of Dialog? |
| IDS | Resource ID of String? |
| Lang | **Lang**uage |
| len | **Len**gth |
| Loc | **Loc**ation |
| lst | **Li**s**t** |
| LPCTSTR | |
| lpsz | |
| min | **min**imum, **min**utes |
| msg | **Me**ssa**g**e |
| Num |**Num**ber |
| m_ | **M**ember |
| Ob | **Ob**ject |
| optn | Option |
| p | **P**ointer |
| PCH | **P**re**c**ompiled **H**eader |
| pix | **Pix**els |
| Pos | **Pos**ition, **Pos**t, **P**r**o**pertie**s** |
| prn | **Pr**oportio**n**al, **Pr**i**n**ter |
| pro | **Pro**fessional |
| prop | **Prop**ortional, **Prop**erties |
| PW | **P**ass**w**ord |
| ref |  **Ref**erence |
| reg | **Reg**ular, **Reg**istration, **Reg**istry |
| rep | **Rep**eat, **Rep**lace |
| res | **Res**ource, **Res**olution |
| RTF | **R**ich **T**ext **F**ormat |
| RTL | **R**ight **t**o **L**eft  |
| s, str, STR | **S**tring |
| sav | **Sav**e |
| scr | **Scr**eenplay, **Scr**ipt
| sec | **Sec**onds |
| std | **St**andar**d** |
| Sel | **Sel**ect (-ion) |
| Sent | **Sent**ence |
| Spec | **Spec**ifications |
| Supt | **Sup**por**t** |
| sws | **S**creen **W**riter **S**tudio |
| Tech | **Tech**nical |
| trans | Transitions |
| UC | **U**pper**c**ase |
| UI | **U**ser **I**nterface |
| val | **V**alue |
| VS | **V**isual**S**cript |
| Wid | **Wid**th |

### リファクタリング案
* UC は UpperCase と書くなよ。わかるかよ。まだUCaseのほうがいい。
* properties の略語は混乱しすぎ。Page2Stageにはシソーラス機能あるのに何考えているんだ！？　長過ぎるなら一義性を確保しつつ短めの類語に置き換えよ。
* プロパティなど数か所しか使わない使用頻度の少ないものなら略語は使うな。
* 略語は頻繁に用いるシンボルに限って使うこと。そうしないと意味がない。
* 略語には世間共通の慣例がある。そういうのを無視して定義しない。
* なんのための略語なのか熟考して定義すること。
* ノリでその場の雰囲気で浅く考えたものは定義しないこと。そういうのは後で絶対メンテナンスで足を引っ張る。
* プロパティ用のグローバル変数に略語を使うくらいならクラス作って定義したほうがいいと思う。ちゃんと分けてわかりやすくなるし。インスタンスは theProperties や theEnv などできるし。

## MFC 関連


## ファイルサービス
* CFile
* CMemFile
* CSharedFile
* CStdioFile

## グラフィックの描画
* CDC
* CClientDC
* CPaintDC
* CWindowDC

## グラフィックの描画オブジェクト
* CBitmap
* CBrush
* CFont
* CPalette
* CPen


## アプリケーションアーキテクチャ
* CDocument


## コントロール
* CButton
* CComboBox

* CString
* HINSTANCE
* PreTranslateMessage
* CArray

* CWaitCursor

* CMDIChildWnd
* CMenu
* CWinApp
* CWnd
* CDataExchange
* CScrollBar
* CComboBox
* CListBox
* CStatic
* CProgressCtrl


## 表示
* CView
* 


---


## コントロールとサポートクラス
* CCmdUI
* CDataExchange


## データ型 (単値)
* CPoint
* CRect
* CSize
* CTime

# Windows API 関連

* COLORREF
* GetProfileString
* WriteProfileInt
* MapiRecipDesc
* FreeLibrary
