# 2023年6月20日

現在、判明している LuaRT のドキュメント([モジュール・リファレンス](https://luart.org/doc/modules.html))に関する問題をまとめたものです。引用の範囲内であると判断していますが、ドキュメントのライセンスが明示されていないため権利等で問題がありましたら Issue にてお知らせください。削除対応させていただきます。

筆者は活動休止中ですが、あまりにも誤字脱字など散見されるため見つけたら追記します。次回のクロール予定は八月以降です。ドキュメントのライセンスが公表された場合はこの限りではありません。翻訳準備は進めていますが……。

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

## compression/index.html

https://luart.org/doc/File.html は存在しない。正しくは https://luart.org/doc/sys/File.html です。

誤:
```html
<td><span><a href="../File.html">
```

正:
```html
<td><span><a href="../sys/File.html">
```

## string/index.html

String  functions: 余計な閉括弧が付いている (衍字)。

```
string.upper()	Convert a string to uppercase    string>
```

UTF8 functions: UFT8 ではなく UTF8 です (誤字)

```
string.ufind()	Search for the first pattern in an UFT8 string	number
```

## string/length.html

リンク切れ: LuaRT 1.4.0 では、```string.wlen()``` は存在しません(変更があったバージョンは特定できていません)。代わりに ```string.ulen()``` を使います。

> To get the length in characters for UTF8 strings, do not use the # operator, use string.wlen() instead.

加えてサンプルソースに文字化けとwlenがあります。このままでは正常に動作しません。

誤:
```lua
local summer_in_french = "�t�"

...

print( summer_in_french:wlen() )
```

正:
```lua
local summer_in_french = "été"

...

print( summer_in_french:ulen() )
```
