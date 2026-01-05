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

## view.cpp / .h

* ReplaceWord
* ResetDict
* CVisualScriptView::OnToolsThesaurus
* CVisualScriptView::ThesDone

## Wintertree API

### Sentry Spelling Checker Engine (ssce.h)

* SSCE_S16
* SSCE_S32
* SSCE_AddToLex
* SSCE_GetLexInfo
* SSCE_GetLex
* SSCE_ClearLex
* SSCE_OpenSession
* SSCE_CloseSession
* SSCE_OpenLex
* SSCE_SetOption
* SSCE_Version
* SSCE_SetRegTreeName
* SSCE_Suggest
* SSCE_CheckWord
* SSCE_FILE_NOT_FOUND_ERR
* SSCE_IGNORE_CAPPED_WORD_OPT
* SSCE_MAX_WORD_SZ
* SSCE_STRIP_POSSESSIVES_OPT
* SSCE_UNCAPPED_WORD_RSLT
* SSCE_MIXED_CASE_WORD_RSLT
* SSCE_MIXED_DIGITS_WORD_RSLT
* SSCE_CONDITIONALLY_CHANGE_WORD_RSLT


## ダイアログとクラス
* DlgThes : CDlgThes, CThesaurus
* SpellCheck : CDlgSpellCheck, CDlgSpellCheck, CSpellingDictionary

view.cpp から呼び出します(Page2Stage/MFCはMVCモデルのようです)。


### 関連資料

 *
 * 

## 将来の予定

* デッドコード削除後にリライトをして無事にビルドできるようになってからスペルチェッカーの再実装
* スペルチェッカーエンジンはHunspellなど
* シソーラス(類義語、同義語)はOpenThesaurusやWordNetベースで再実装


