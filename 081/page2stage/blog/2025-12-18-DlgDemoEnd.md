# 2025年12月18日 - DlgDemoEnd の除去作業記録

## 目的
オープンソース版では不要になる DlgDemoEnd (試用期間終了の通知ダイアログ) の廃止

## 作業対象
* frame.cpp: DlgDemoEnd.h のインクルード削除、DlgDemoEndダイアログ使用箇所の削除
* VisualScript.cpp: DlgDemoEnd.h のインクルード削除
* VisualScript.rc: ダイアログリソースの削除
* resource.h: IDD_DEMO_END, IDC_DEMO_DISCOUNT 定義の削除

## リソース識別子
### VisualScript.rc
* IDD_DEMO_END: Dialog と DESIGNINFO の二箇所

### AfxFormatString1
これらはリソースIDとして使われているだけです。文字列の実体はリソースファイルではなく各 C++ コードにハードコードされています。
* IDC_DEMO_DATE
* IDC_DEMO_NAME
* IDC_ORDER
* IDC_DEMO_DISCOUNT

## 外部参照
* about.cpp: CDlgRegister, GoToWeb への参照あり。後でabout.cppは書き直す。
* Windward ライブラリ (strext.cpp): IntToCString
* profile.cpp: myGetProfileInt

## 備考
 * 該当箇所さえ削除すれば DlgDemoEnd.h と DlgDemoEnd.cpp は不要になります。
 * IntToCString は to_String へ置き換えられないか？ A. IntToCString は後方互換性のために残しておいてもいいけど、to_String は C++11以降なら使える→ [to_string - cpprefjp C++日本語リファレンス](https://cpprefjp.github.io/reference/string/to_string.html)

