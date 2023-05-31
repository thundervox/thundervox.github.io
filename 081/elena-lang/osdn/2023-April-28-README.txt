= ELENA プログラミング言語

[[Embed(84074668-31633400-a9d3-11ea-9fd6-9282ab80b537.jpg, float=checked)]]

^ [https://github.com/ELENA-LANG/elena-lang/tree/1bed61e492bdbcc9591368a1f5e4d240626a4f43 README.md (rev.1bed61e)] の部分翻訳です。^

[https://elena-lang.github.io/ elena-lang.github.io] | [https://github.com/ELENA-LANG/elena-lang/wiki/ELENA-Programming-Manual 取扱説明書] | [https://github.com/ELENA-LANG/elena-lang/blob/master/CHANGELOG.md 変更履歴] | [https://github.com/ELENA-LANG/elena-lang/blob/master/CONTRIBUTING.md 寄贈方法]

ELENA は遅延バインディングに対応した汎用プログラミング言語です。関数型プログラミングとオブジェクト指向プログラミングの機能を兼ね備えたマルチパラダイム言語です。強い型付けと弱い型付け、ランタイム変換、プリミティブ型のボクシングとアンボクシング、外部ライブラリの直接使用ができます。メッセージディスパッチを扱うために豊富なツールセットが用意されています : 多重メソッド、メッセージ資格付与、ジェネリックメッセージハンドラ。多重継承はミックスインと型のインターフェースでシミュレートします。組み込みスクリプトエンジンによりにカスタム定義のスクリプトをアプリケーションに組み込めます。 単体アプリケーションと仮想マシンのクライアントで使えます。

== 主要機能

 * 自由なオープンソース (MIT ライセンス)

 * 完全なソースコード

 * Unicode サポート (utf-8 / utf-16 / utf-32)

 * GUI による統合開発環境とデバッガ

 * オプション型 (型推論)

 * 多重ディスパッチと多重メソッド

 * 複数値による返値

 * 可変長メソッドのサポート

 * 生成可能メソッド

 * クロージャー

 * ミックスイン

 * 型のインターフェースと変換

 * クラスとコードのテンプレート

 * スクリプトエンジン

== 動作環境

 * '''Windows''' : x86 (32-bit) / x86-64 (64-bit)

 * '''Linux''' : x86 (32-bit) / x86-64 (64-bit) / ppc64le / arm64 (a64)

== ソースコードのダウンロードとコンパイル

ソースコードの取得方法は git リポジトリのクローンを行います。

{{{ code bash

git clone https://github.com/ELENA-LANG/elena-lang.git

}}}

=== Windows 版

コンパイラのコードは C++ で実装していますが外部依存ライブラリは不要です。必要なものは Visual Studio 2019 のみです。

システム環境変数 ''PATH'' へ ''BIN'' フォルダのパスを

追加するか ''Windows\System32'' へ elenavm.dll と elenart.dll をコピーしてください。

VS2019 でコンパイラをビルドするにはディレクトリを ELENA のルートフォルダへ移動して以下を実行します。

{{{ code bash

recompile60.bat

}}}

ライブラリをビルドするには以下を実行します。

{{{ code bash

rebuild_lib60.bat

}}}

サンプルソースコードをビルドするには以下を実行します。

{{{ code bash

rebuild_examples60.bat 

}}}

ロゼッタコード (Rosetta-code) 掲載のサンプルソースコードをビルドするには以下を実行します。

{{{ code bash

examples\rosetta\build.bat 

}}}

ユニットテストをするには以下を実行します。

{{{ code bash

lib_tests.bat

}}}

== ソースコードの構成

ELENA ソースコードの構成は以下のとおりです。

|| '''ディレクトリ'''  || '''概要''' ||

|| bin                 || バイナリと共有ライブラリ ||

|| bin\scripts     ||     スクリプトエンジンと仮想マシン (VM) のコンソールで使用するスクリプト||

|| bin\templates     ||   ELENA プロジェクトのテンプレート ||

|| asm                ||  コアルーチンのテンプレート (アセンブリ言語で実装) ||

|| dat\sg            ||   言語文法書           ||

|| dat\og            ||   言語最適化規約 ||

|| doc              ||    取扱説明書 ||

|| elenasrc3\elc      ||  コンパイラのソースコード ||

|| elenasrc3\elenart   || ランタイム共有ライブラリのソースコード ||

|| elenasrc3\elenasm ||   スクリプトエンジンのソースコード ||

|| elenasrc3\elenavm ||   仮想マシンのソースコード ||

|| elenasrc3\gui      ||  統合開発環境 (IDE) のソースコード ||

|| elenasrc3\tools     || ELENA ユーティリティのソースコード||

|| examples60          || ELENA サンプルソースコードの ||

|| src60               || ELENA ライブラリのソースコード ||

== コミュニティ

=== 1. Bugs, questions, suggestions?

=== 2. Implement "up for grab" issues

=== 3. Rosetta code

== 連絡先

== 関連情報

 * '''ナイトリービルド:''' https://ci.appveyor.com/project/arakov/elena-lang/build/artifacts

 * '''ELENA 取扱説明書:''' https://github.com/ELENA-LANG/elena-lang/wiki/ELENA-Programming-Manual

 * '''ELENA API 5.0:''' https://elena-lang.github.io/api/index.html

 * '''Git クローン URL:''' git://github.com/ELENA-LANG/elena-lang.git

 * '''チュートリアル:''' https://github.com/ELENA-LANG/tutorials

 * '''ELENA reddit:''' https://www.reddit.com/r/elena_lang/

 * '''ソースコード:''' https://github.com/ELENA-LANG/elena-lang

 * '''Twitter:''' https://twitter.com/elena_language

 * '''Rosetta code (ロゼッタコード):''' http://rosettacode.org/wiki/Category:Elena

== ライセンス

このパッケージで配布されるコンパイラと実行結果ファイルには MIT ライセンスが適用されます。詳細情報は LICENSE ファイルをお読みください。

----
