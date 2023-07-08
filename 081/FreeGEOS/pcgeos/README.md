# PC/GEOS

> この記事は [README.md](https://github.com/bluewaysw/pcgeos/blob/f088abcfe1600f00f103c80ce90427ad647bf91c/README.md) (Dec 31, 2022 版) の非公式翻訳です。まだまだ未完成ですが、順次作業を進めていきます。

# ビルド方法

## ビルド要件

The SDK requires "sed" (https://en.wikipedia.org/wiki/Sed) and "perl" (https://en.wikipedia.org/wiki/Perl) to be installed. Both are pre-installed in most Linux-distributions. Windows-users should install "sed" by adding the usr/bin of the official git distribution (https://git-scm.com) to the path (or Cygwin), and should use the perl-variant "Strawberry Perl" (http://strawberryperl.com/).

On Linux if you want to use swat for debugging with good system integration is is required to install xdotools package. It ensures swat receives the keyboard focus once needed. 

## WATCOM のインストールと環境変数の設定

## PC/GEOS SDK のビルド

### pmake ツールのビルド

```bash
cd pcgeos/Tools/pmake/pmake
wmake install
```

### その他 SDK ツール全般のビルド

```bash
cd pcgeos/Installed/Tools
pmake install
```

### PC/GEOS (ターゲット) コンポーネント全般のビルド

```bash
cd pcgeos/Installed
pmake
```

### ターゲット環境のビルド

```bash
cd pcgeos/Tools/build/product/bbxensem/Scripts
perl -I. buildbbx.pl
```

  - the answers to the questions from the above perl-script are:
    - nt (プラットフォーム 向け)
    - y (EC バージョン 向け)
    - n (DBCS 向け)
    - y (geodes 向け)
    - n (VM ファイル 向け)
    - and then you'll have to enter the path to a "gbuild"-folder in your LOCAL_ROOT-folder.
  - BTW: It's expected that the current version of the perl-script creates several "Could not find file _name_ in any of the source trees."-messages.

### ターゲット環境の起動 (DOSBox)



## ターゲット環境のカスタマイズ

ターゲット環境を自分用にカスタマイズするときは、 %ROOT_DIR%/bin/basbox.conf ファイルは変更しないでください。

- %LOCAL_ROOT% フォルダにbasebox_user.conf ファイルを作成します。

- ここで新しい設定項目を入力します。 These settings overwrite those from basebox.conf. 例えば、

```toml
[cpu]
cycles=55000
```

# 開発方法

PC/GEOS comes with extensive technical documentation that describes tools, programming languages and API calls from the perspective of an SDK user. This documentation can be found in the `TechDocs` folder and is available in Markdown format. Here are some entry points to the main volumes:

- はじめに
  - [チュートリアル](TechDocs/Markdown/tutorial.md) - the initial chapters describing the development environment are somewhat outdated, and still refer to the original two-machine setup for debugging, but this nevertheless gives a good idea of overall development process.
  - [基本概念](TechDocs/Markdown/concepts.md)
  - [ツール](TechDocs/Markdown/tools.md)
- C 言語による開発
  - [GOC キーワードと API コール](TechDocs/Markdown/routines.md)
  - [オブジェクト・リファレンス](TechDocs/Markdown/objects.md)
  - [クイック・リファレンス](TechDocs/Markdown/quickref.md)
- アセンブリによる開発
  - [アセンブリ言語 ESP](TechDocs/Markdown/esp.md)
  - [アセンブリ・リファレンス](TechDocs/Markdown/asmref.md)
  - [ドライバ開発キット](TechDocs/Markdown/ddk.md)

# 開発参加