# 2023年6月20日

現在、判明している LuaRT のドキュメント([モジュール・リファレンス](https://luart.org/doc/modules.html))に関する問題をまとめたものです。

引用の範囲内であると判断していますが、ドキュメントのライセンスが明示されていないため権利等で問題がありましたら Issue にてお知らせください。削除対応させていただきます。

筆者は活動休止中ですが、見つけたら追記します。

スペルチェックには[WebSpell（オンライン・スペルチェック）](https://lsd-project.jp/ja/service/webspell/index.html)を使用しています。


## canvas/Canvas-show.html

HTTrack でクロールすると canavs/Canvas-show.html が生成されてしまう。canavs ではなく canvas になっていない。

誤:
```html
  <link href="../canavs/Canvas-show.html" rel="canonical" />
```
正:
```html
  <link href="../canvas/Canvas-show.html" rel="canonical" />
```
