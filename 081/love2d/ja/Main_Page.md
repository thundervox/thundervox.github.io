# Main Page (日本語)

## ありがとうございます

ご承知のとおり、 [LÖVE](http://love2d.org) は Lua プログラミング言語で 2D ゲームを開発デキるフレームワークです。 LÖVE は完全にフリーであるため、フレンドリーなオープンソースのホビープロジェクトだけでなく、シビれるような、クローズドソースのプロジェクトにも採用されています。

こちらからご興味のある記事を読み進められます。

* [Getting Started](Getting_Started)
* [Building LÖVE](Building_LOVE)
* [Category:Tutorials](Tutorials)
* [love](love) (モジュール)
* [Game Distribution]()
* [Config Files]()
* [Licenseライセンス](License) (フリー！)
* [ゲーム](Category_Games)
* [ライブラリ](Category_Libraries)
* [ソフトウェア](Category_Software)
* [スニペット](Category_Snippets)
* [改訂履歴](Version_History)

## Lua

Lua は未経験ですか？  本当にクールなプログラミング言語です！  本書は Lua の教科書ではありませんが、ありがたいことに第三者による素晴らしい解説資料があります。

* [Programming in Lua (first edition)](http://lua.org/pil)
* [Lua-Users Tutorials](http://lua-users.org/wiki/TutorialDirectory)
* [Lua 5.1 Reference Manual](http://www.lua.org/manual/5.1/)

## Hello World

このソースコードは LÖVE で実行すると、縦 800, 横 600 のウィンドウで黒色の背景色に白色の 'Hello World' テキストを表示します。

```lua
function love.draw()
    love.graphics.print('Hello World!', 400, 300)
end
```

----
このページの最終更新日時は [2022年01月20日(木) 午後23時12分](https://love2d.org/w/index.php?title=Main_Page&oldid=27392) です。

特に記載がない限り、内容は [GNU Free Documentation License 1.3](http://www.gnu.org/copyleft/fdl.html) ライセンスで利用できます。
