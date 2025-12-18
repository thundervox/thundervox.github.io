# 2025年12月18日 - DlgDemoEnd の除去作業記録

## 目的
オープンソース版では不要になる DlgDemoEnd (試用期間終了の通知ダイアログ) の廃止

## 作業対象
* frame.cpp: DlgDemoEnd.h のインクルード削除、DlgDemoEndダイアログ使用箇所の削除
* VisualScript.cpp: DlgDemoEnd.h のインクルード削除
* VisualScript.rc: ダイアログリソースの削除

## リソース識別子
### VisualScript.rc
* IDD_DEMO_END

### AfxFormatString1
* IDC_DEMO_DATE
* IDC_DEMO_NAME
* IDC_ORDER
* IDC_DEMO_DISCOUNT

## 外部参照
* about.cpp: CDlgRegister, GoToWeb への参照あり。後でabout.cppは書き直す。
* Windward ライブラリ (strext.cpp): IntToCString
* profile.cpp: myGetProfileInt

## 備考
該当箇所さえ削除すれば DlgDemoEnd.h と DlgDemoEnd.cpp は不要になります。
