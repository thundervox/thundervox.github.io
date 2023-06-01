A Brief introduction (日本語)
=============================

Author: Randy Hollines

Date: March 4, 2018

Translatior: isVowel

Translated date: March, 15, 2022


ごあいさつ
==========

Objeck 言語の設計思想は使いやすい強い型付けのオブジェクト指向プログラミング言語です。 
2008 年当時、この言語は初期開発段階であったため、
既存のオブジェクト指向と関数型プログラミング言語の調査を行い、
それらの機能をシンプルにしたものを
Objeck として実装しました。

主要搭載機能:

-  シンプルで直観的なクラスライブラリ

-  関数型プログラミングのサポート

-  並列処理 (スレッドとミューテックス)

-  メモリの自動管理

-  ネイティブ JIT 方式による実行器（バイトコード計算機）

-  UTF-8 による I/O の Unicode サポート

-  クロスプラットフォームライブラリ

-  Windows, Linux および OS X のフルサポート

お使いになる前に
================

バイナリ (またはソースコード) を入手するには、プロジェクトのウェブサイト
`objeck.org <http://www.objeck.org/>`__ を開いてください。 Windows, Linux
および macOS 用の対話型インストーラもダウンロード可能です。
バイナリのアーカイブファイル (すなわち \*.zip と \*.tgz) は、
その他すべての対応プラットフォームでダウンロード可能です。
このディストリビューションはコンパイラ、仮想マシンとデバッガから構成されています。
コンパイラの名称は **obc** であり、仮想マシン (VM) の名称は **obr** です。

こちらは Objeck で記述した世界一有名な \"Hello World\" プログラムです:

.. code-block:: ruby

	class Hello {
		function : Main(args : String[]) ~ Nil {
			"Hello World"->PrintLine();
			"Καλημέρα κόσμε"->PrintLine();
			"こんにちは 世界"->PrintLine();
		}
	}

プログラムとして UTF-8 形式のテキストファイル **hello.obs** を保存します。
先述のコマンドは実行可能ファイル **hello.obe** を作成します。
その後、このファイルを実行します。

コードをコンパイルするには以下を入力します:

.. code-block:: bash

	obc -src hello.obs -dest hello.obe

コードを実行するには以下を入力します:

.. code-block:: bash

	obr hello.obe

Windows では結果を確認しやすくするために、テキストファイルへ実行結果を
リダイレクトしてからメモ帳で開いてみてください。

.. code-block:: bash

	obr hello.obe > hello.txt


コードのコンパイルと実行
========================

Objeck コンパイラは二種類のバイナリを生成します。
すなわち、実行可能ファイルとライブラリです。コンパイラへライブラリ名を
渡すことでライブラリを実行可能ファイルにリンクできます。
命名規約として実行可能ファイルの拡張子は \*\ **.obe** であり、
ライブラリの拡張子は **\*.obl** です。

こちらはもう少し詳しい用例です。
この用例は XML 処理プログラムのコンパイル後に実行します。
このプログラムではコレクションと XML 構文解析ライブラリをリンクします。

.. code-block:: bash

	obc -src examples/2_xml.obs -lib collect.obl,xml.obl -dest xml_path.obe
	obr xml_path.obe

この用例は暗号化ライブラリを用いたプログラムをコンパイル後に
実行します。

.. code-block:: bash

	obc -src examples/7_encrypt.obs -lib encrypt.obl -dest encryption.obe
	obr encryption.obe

多岐にわたるサンプルプログラムのリストは Rosetta code の
`solutions <https://github.com/objeck/objeck-lang/tree/master/programs/rc>`__
をご確認ください。そのほかのライブラリについても、より詳しく学ぶには
`API ドキュメンテーション <http://www.objeck.org/docs/api/index.html>`__ をご確認ください。

表 1 – コンパイラのオプション

.. csv-table::
	:header: "オプション", "概要"
	:widths:       18,     82

	"-src", 		"',' で区切り指定したソースファイルのパス"
	"-lib", 		"',' で区切り指定したライブラリファイルのパス"
	"-tar", 		"出力形式です。オプションとして **exe** は実行可能ファイル、"
	"",				"**lib** はライブラリとなります。デフォルトは **exe** です。"
	"-opt", 		"最適化水準。 **s0** は消極的 (無し)、 **s3** は"
	"",				"積極的 (最高) です。デフォルトは **s0** です。"
	"-dest", 		"出力ファイル名"
	"-alt", 		"C 言語風のシンタックスで書かれたソースコードのコンパイル"
	"-debug", 		"指定時は、デバッガで使うデバッグアウトを生成します。"
	"", 			"(これは必ず引数の最後尾に指定してください)"

基本機能
========

最初にリテラル、変数と制御フローを調べてみましょう。

リテラルと変数
--------------

リテラルは大半のプログラミング言語で定義されています。
Objeck において、リテラルはオブジェクトとして扱われるため、
それらと関連付けられたメソッドがあります。

.. code-block:: ruby

	'\u00BD'->PrintLine();
	13->Min(3)->PrintLine();
	3.89->Sin()->PrintLine();
	"Hello World"->Size()->PrintLine();


こちらは変数の宣言と代入に関する数点の用例です。
明示的に変数の型を定義、または代入やキャストにより
暗黙的に型推論を行えます。変数の型推論を使うとキャストは
可能であっても、以降のプログラムで再定義できなくなります。

.. code-block:: ruby

	a : Int;
	b : Float := 13.5;
	c := 7.25; # Float として型推論
	d := (b * 2)->As(Int); # Int として型推論


表 2 – データ型

======== =================================
型       概要
======== =================================
Char     Unicode 文字値
Char[]   Unicode 文字配列
Bool     ブール値
Bool[]   ブール配列
Byte     1-byte 整数値
Byte[]   1-byte 整数配列
Int      4-byte 整数値
Int[]    4-byte 整数配列
Float    8-byte 十進数値
Float[]  8-byte 十進数配列
Object   抽象データ型の参照
Object[] 抽象データ型の配列
Function 関数の参照
======== =================================

コメント
--------

コメントは一行、または複数行に渡ります。 さらに、コメントは
バンドル、クラス、インタフェースと関数やメソッドから
コードのドキュメンテーションを生成するのに使われます。 
コードからドキュメンテーションを生成する方法は `プロジェクトのウェブサイト <http://www.objeck.org>`__
に掲載されている追加情報を参照してください。

.. code-block:: ruby

	flag := false; # 一行コメント
	#~
	複数行コメント。上述のフラグには 
	true や false を設定します
	~#


ロジックと制御フロー
--------------------

一般的な言語と同じく Objeck でも条件式と制御フローのロジックをサポートしています。 
唯一、些細な違いがあるとすれば条件付きステートメントの末尾には
セミコロンを付けることです。

If/else
~~~~~~~

\"if/else\" ステートメントは基本的な制御ステートメントです。

.. code-block:: ruby

	number := Console->ReadLine()->ToInt();
	if(number <> 3) {
		"3 と不等価"->PrintLine();
	} else if(number < 13) {
		"13 以下"->PrintLine();
	} else {
		"それ以外の数値"->PrintLine();
	};


Select
~~~~~~

\"Select\" ステートメントは整数と列挙型の値をコードブロックへ効率的に
割り当てるために使います。

.. code-block:: ruby

	select(c) {
		label Color->Red: { "赤色"->PrintLine(); }
		label Color->Green: { "緑色"->PrintLine(); }
		label Color->Purple: { "紫色"->PrintLine(); }
		other: { "その他の色"->PrintLine(); }
	};

	select(n) {
		label 9:
		label 19: { n->PrintLine(); } 
		label 27: { (3 * 9 = n)->PrintLine(); }
	};


この言語では以下のループ処理ステートメントをサポートしています。

Do
~~

\"do\" ループは単純な事前評価のループです。

.. code-block:: ruby

	i := 10;
	while(i > 0) {
		i->PrintLine();
		i -= 1;
	};


Do/While
~~~~~~~~

\"do/while\" ループは基本的な事後評価のループです。

.. code-block:: ruby

	i := 0;
	do { 
		i->PrintLine();
		i += 1;
	} while(i <> 10);


For
~~~

\"for\" ループは制御式で展開された制御ループです。

.. code-block:: ruby

	location := "East Bay";
	for(i := 0; i < location->Size(); i += 1;) {
		location->Get(i)->PrintLine();
	};


Each
~~~~

\"each\" ループは配列やコレクションに存在する要素全体を
反復処理する制御ループです。

.. code-block:: ruby

	area_code := Int->New[3];
	area_code[0] := 5;
	area_code[1] := 1;
	area_code[2] := 0;
	each(i : values) {
		area_code[i]->PrintLine();
	};


演算子
------

論理演算子、算術演算子およびビット単位演算子をサポートしています。
演算子における最下位から最上位までの優先順位は: **論理演算子、 [+, -]**
および **[*, /, %, <<, >>, and, or, xor]** です。
同一優先順位の演算子は左辺から右辺へ評価します。

表 3 - 論理演算子

======== =======================
演算子   概要
======== =======================
&        論理積 (および)
\|       論理和 (または)
=        等価
<>       不等価 (単項 not)
<        以下 (小なり)
>        以上 (大なり)
<=       以下または等価
>=       以上または等価
======== =======================

表 4 - 算術演算子

======== ===========
演算子   概要
======== ===========
\+       加算
\-       減算
\*       乗算
/        除算
%        余剰
======== ===========

表 5 – ビット単位演算子

======== ==============
演算子   概要
======== ==============
<<       左シフト
>>       シフト
and      ビット単位 and
or       ビット単位 or
xor      ビット単位 xor
======== ==============

図 1 - クレジットカードの簡易認証

.. code-block:: ruby

	class Luhn {
		function : IsValid(cc : String) ~ Bool {
			isOdd := true; oddSum := 0; evenSum := 0;
			for(i := cc->Size() - 1; i >= 0; i -= 1;) {
				digit : Int := cc->Get(i) - '0';
				if(isOdd) {
					oddSum += digit;
				} else {
					evenSum += digit / 5 + (2 * digit) % 10;
				};
				isOdd := isOdd <> true;
				};
			return (oddSum + evenSum) % 10 = 0;
		}
	
		function : Main(args : String[]) ~ Nil {
			IsValid("49927398716")->PrintLine();
			IsValid("49927398717")->PrintLine();
			IsValid("1234567812345678")->PrintLine();
			IsValid("1234567812345670")->PrintLine();
		}
	}


Base64 エンコーディング処理クラスよりコードを引用

.. code-block:: ruby

	# 基本的なエンコーディング処理のループ
	r := ""; i : Int; a := 0;
	for(i := 0; i < end; i += 3;) {
	a := (data[i] << 16) or (data[i+1] << 8) or (data[i+2]);
		r->Append( lut[0x3F and (a >> 18)] );
		r->Append( lut[0x3F and (a >> 12)] );
		r->Append( lut[0x3F and (a >> 6)] );
		r->Append( lut[0x3F and a] );
	};


配列、文字列とコレクション
--------------------------

動的割り当ての配列、 Unicode 文字列および多岐にわたるコンテナを
言語でサポートしています。


配列
~~~~~~

配列はインデックス付きリストのような型を扱えます。
配列はヒープから動的割り当てが行われた後にガベージコレクターにより
メモリが管理されます。ランタイムシステムは範囲検査をサポートしており、
配列の範囲が侵害されると実行を停止します。

配列の割り当てとインデックス処理

.. code-block:: ruby

	# Int 配列の割り当て
	boxes := Int->New[2,3];
	boxes[0,0] := 2;
	boxes[0,1] := 4;
	boxes[0,2] := 8;
	boxes[1,0] := 1;
	boxes[1,1] := 2;
	boxes[1,2] := 3;
	dims := boxes->Size(); # 次元数の取得
	dims[0]->PrintLine(); # 一次元
	dims[1]->PrintLine(); # 二次元

	# 文字列の作成とイテレート
	directions := String->New[4];
	directions[0] := "North";
	directions[1] := "South";
	directions[2] := "East";
	directions[3] := "West";
	each(i : directions) {
		directions[i]->PrintLine();
	};


文字列
~~~~~~

文字列は **String** クラスでサポートされた Unicode 文字のコレクションです。 
String クラスは挿入、検索、部分文字列、型解析 (すなわち、 **String** から **Float** への変換)
など多種多様な処理をサポートしています。 
変数の値についても文字列リテラル内へインライン化できます。 
文字列は文字の配列と UTF-8 バイトの配列へ変換可能です。 

.. code-block:: ruby

	name := "DJ";
	name += ' ';
	name += "Premier";
	name->SubString(2)->PrintLine();
	name->Size()->PrintLine();


日時計プログラムよりコードを引用

.. code-block:: ruby

	"時間\t\t太陽の時角\t\t午前 6 時～午後 6 時までの文字盤の時間軸における角度"->PrintLine();
	for(h := -6; h <= 6; h+=1;) {
		hra := 15.0 * h;
		hra -= lng - ref;
		hla := (slat* (hra*2*Float->Pi()/360.0)->Tan())
			->ArcTan() * 360.0 / (2*Float->Pi());
		"HR={$h}\t\tHRA={$hra}\t\tHLA={$hla}"->PrintLine();
	};


コレクション
~~~~~~~~~~~~

さらに、Vectors (ベクトル), Lists (リスト) および Maps (リスト) など
多種多様なコレクションの配列を言語でサポートしています。
コレクションクラスに関して詳しく知るには、
`API ドキュメンテーション <http://www.objeck.org/docs/api/index.html>`__
をご確認ください。 これらのクラスを使うには、コレクションのバンドルを必ず
以下の行でコードで参照してください:

.. code-block:: ruby

	use Collection;


コレクションを使うプログラムのコンパイル時は必要とされるライブラリを
必ずリンクしてください。例えば、

.. code-block:: bash

	obc -src genres.obs -lib collect.obl -dest genres.obe


**ベクトル** とは動的可変長配列です。 インデックス処理、イテレート、
および値の末尾追加において高速処理をサポートしています。
ベクトルの処理性能を改善するには処理前にメモリを割り当てます。

.. code-block:: ruby

	genres := Vector->New();
	genres->AddBack("ヒップホップ");
	genres->AddBack("クラシック");
	genres->AddBack("ジャズ");
	genres->AddBack("ロック");
	genres->AddBack("フォーク");
	each(i : genres) {
		genres->Get(i)->As(String)->PrintLine();
	};


**リスト** とは線形連結ノードのコレクションです。 値の挿入と削除において高速処理を
サポートしています。メモリのノードはオンデマンドで割り当てられますが、
**ベクトル** と同じようにノードでインデックスを直接使うことはできません。

.. code-block:: ruby

	artists := List->New();
	artists->AddBack("ヘンドリックス");
	artists->AddFront("ベック");
	# 中央への挿入でカーソルを戻す
	artists->Back(); 
	artists->Insert("大衆");
	# リストの先頭へカーソルを移動
	artists->Rewind(); 
	# 値のイテレート
	while(artists->More()) {
		artists->Get()->As(String)->PrintLine();
		artists->Next();
	};


**Map** (マップ) と **Hash** (ハッシュ) クラスは key/value ペアを処理します。
**Map** はツリーにある値を処理してからオンデマンドでメモリを割り当てます。 **マップ** はハッシュよりも
処理速度は遅いですが、メモリの処理効率は優れています。 **ハッシュ** はメモリ消費量を犠牲にすることで
キーを用いた配列のインデックス処理、および挿入と削除における高速処理をサポートします。

.. code-block:: ruby

	area_codes := IntMap->New();
	area_codes->Insert(510, "オークランド");
	area_codes->Insert(415, "サンフランシスコ");
	area_codes->Insert(650, "パロアルト");
	area_codes->Insert(408, "サンノゼ");
	area_codes->Find(510)->As(String)->PrintLine();


オブジェクトと関数
==================

冒頭で述べましたが、 Objeck はオブジェクト指向と関数型プログラミングの
コンセプトをサポートしています。 クラスと関数をコンテキストへ配置するための
プログラミングスコープ全体は以下の通りです:

バンドル → クラス → メソッド・関数→ ローカルブロック

クラスとインタフェース
----------------------

その他の言語と同じく、**class** (クラス) は操作と関連づけられたデータの
抽象化コレクションです。 **interface** (インタフェース)は
クラスを実装する場合に条件を与えるための操作 (契約) の設定です。
Objeck において、クラスとインタフェースはすべてパブリックです。
クラスのメンバ変数は外界から保護されています。しかしながら、
外部クラスのソースから継承したクラスで親のメンバ変数へアクセスできます。
外部からクラスを呼び出すには必ず "getters" と "setters" を使い、
コンパイラで最適化したコードを生成してください。

静的パブリック **関数** と同じく、パブリックやプライベートの
**メソッド** があります。 実装が未定義であっても、 **インタフェース** には種類を問わず
メソッドや関数 (すなわち、**パブリック** や **プライベート**) の定義が可能です。 
最後に、 Objeck は **リフレクション** をサポートしているため、実行時におけるインスタンスの
動的内観をプログラマができるようにします。

以下は関連概念の大半を解説したコードの用例です。 
リフレクションとオブジェクトのシリアル化など各種機能について詳しく知るには
`API ドキュメンテーション <http://www.objeck.org/docs/api/index.html>`__
を参照してください。

図 2 – クラス、インターフェイスとリフレクション

.. code-block:: ruby

	interface Registration {
		method : virtual : public : GetColor() ~ String;
		method : virtual : public : GetMake() ~ String;
		method : virtual : public : GetModel() ~ String;
	}
	
	enum EngineType {
		Gas := 200,
		Hybrid,
		Electric,
		Warp
	}
	
	class Vehicle {
		@wheels : Int;
		@color : String;
		@engine_type : EngineType;
	
		New(wheels : Int, color : String, engine_type : EngineType) {
			@wheels := wheels;
			@color := color;
			@engine_type := engine_type;
	}
	
		method : public : GetColor() ~ String {
			return @color;
		}
	
		method : public : GetEngine() ~ EngineType {
			return @engine_type;
		}
	}
	
	class StarShip from Vehicle implements Registration {
		New() {
			Parent(13, "Metal Fuschia", EngineType->Warp);
		}
	
		method : public : GetMake() ~ String {
			return "Excelsior";
		}
	
		method : public : GetModel() ~ String {
			return "NX-2000";
		}
	
		method : public : EchoDescription() ~ Nil {
			"ボルグのパーティで、一緒に飲もう！"->PrintLine();
		}
	}
	
	class Pinto from Vehicle implements Registration {
		New() {
			Parent();
		}
	
		method : public : GetMake() ~ String {
			return "Ford";
		}
	
		method : public : GetModel() ~ String {
			return "Pinto";
		}
	}
	
	class VehicleTest {
		function : Main(args : String[]) ~ Nil {
			pinto := Pinto->New();
			star_ship := StarShip->New();
			type_of := pinto->TypeOf(Vehicle);
			type_of->PrintLine();
			type_of := star_ship->TypeOf(Vehicle);
			type_of->PrintLine();
			type_of := pinto->TypeOf(StarShip);
			type_of->PrintLine();
			registration := star_ship->As(Registration);
			registration->GetMake()->PrintLine();
			registration->GetColor()->PrintLine();
			enterprise := registration->As(StarShip);
			enterprise->EchoDescription();
		}
	}


無名クラス
~~~~~~~~~~

無名クラスは「インライン化」が求められるメソッドや
関数のインタフェースとして作成可能です。
外部変数はクラスのコンストラクタの参照として渡され場合、
無名クラスの内側で参照可能です。

図 3 – Objeck のシリアル化と継承

.. code-block:: ruby

	interface Greetings {
		method : virtual : public : SayHi() ~ Nil;
	}
	
	class Hello {
		function : Main(args : String[]) ~ Nil {
			hey := Base->New() implements Greetings {
				New() {}
				method : public : SayHi() ~ Nil {
					"おや..."->PrintLine();
				}
			};
	
			howdy := Base->New() implements Greetings {
				New() {}
				method : public : SayHi() ~ Nil {
					"こんにちわ！"->PrintLine();
				}
			};
		}
	}


列挙型と定数
~~~~~~~~~~~~

列挙型 (Enum) は名前付き定数値を列挙したものです。 列挙型の値は連続性があり、
オフセット値が起点となります。 定数、列挙型などは名前付き定数値ではあるものの、
各々に固有値を代入できます。

図 4 – Objeck の列挙型と定数

.. code-block:: ruby

	enum Color {
		Red,
		Blue,
		Green
	}
	
	enum Direction {
		Left := -100,
		Right,
		Up,
		Down
	}
	
	consts Products {
		Pip_Boy := 101,
		Valut_Suit := 111,
		Laser := 675
	}


シリアル化
~~~~~~~~~~

オブジェクトのシリアル化はオブジェクトのインスタンスをバイトへ変換・逆変換する仕組みです。
シリアル化はオブジェクトの状態を残したり (すなわちディスクへの保存)、
そのコピーをネットワークでやりとりするために使われます。 

図 5 – Objeck のシリアル化と継承

.. code-block:: ruby

	use Collection;
	
	class Thingy {
		@id : Int;
	
		New(id : Int) {
		@id := id;
		}
	
		method : public : Print() ~ Nil {
			@id->PrintLine();
		}
	}
	
	class Person from Thingy {
		@name : String;
		@values : StringMap;
	
		New(id : Int, name : String) {
			Parent(id);
			@name := name;
			@values := StringMap->New();
			@values->Insert("Jason", IntHolder->New(101));
			@values->Insert("Mark", IntHolder->New(9));
		}
	
		method : public : Print() ~ Nil {
			@id->PrintLine();
			@name->PrintLine();
			@values->Find("Jason")->As(IntHolder)->Get()->PrintLine(); 
			@values->Find("Mark")->As(IntHolder)->Get()->PrintLine(); 
		}
	}
	
	class Serial {
		function : Main(args : String[]) ~ Nil {
			t := Thingy->New(7);
			p := Person->New(13, "Bush");
	
			s := System.IO.Serializer->New();
			s->Write(t);
			s->Write(p);
	
			writer := IO.File.FileWriter->New("objects.dat"); 
			writer->WriteBuffer(s->Serialize());
			writer->Close();
	
			buffer := IO.File.FileReader->ReadBinaryFile("objects.dat"); 
			d := System.IO.Deserializer->New(buffer);
	
			t2 := d->ReadObject()->As(Thingy);
			t2->Print();
			p2 := d->ReadObject()->As(Person);
			p2->Print();
		}
	}


高階関数
--------

高階関数はプログラマがメソッドや関数を関数の引数として渡したり、
メソッドや関数を関数の返値として返すことができるようになります。 
強い型付けによる関数の参照に関するサポートが言語にあります。 
この機能における構成の特性では関数定義の
ネストができます。

図 6 – 関数のコンポジション

.. code-block:: ruby

	class FofG {
		@f : static : (Int) ~ Int;
		@g : static : (Int) ~ Int;
	
		function : Main(args : String[]) ~ Nil {
			compose := Composer(F(Int) ~ Int, G(Int) ~ Int);
			compose(13)->PrintLine();
		}
	
		function : F(a : Int) ~ Int {
			return a + 14;
		}
	
		function : G(a : Int) ~ Int {
			return a + 15;
		}
	
		function : native : Compose(x : Int) ~ Int {
			return @f(@g(x));
		}
	
		function : Composer(f : (Int) ~ Int, g : (Int) ~ Int) ~ (Int) ~ Int {
			@f := f;
			@g := g;
			return Compose(Int) ~ Int;
		}
	}


より具体的に説明すると、指定された関数の結果を
ベクトル内の要素全体に適用するような操作をする場合に
コレクションで使われます。

.. code-block:: ruby

	function : native : Run() ~ Nil {
		"平方根の結果..."->PrintLine();
		values := IntVector->New([1, 2, 3, 4, 5, 100]);
		squares := values->Apply(Square(Int) ~ Int);
		each(i : squares) {
			squares->Get(i)->PrintLine();
		};
	}
	
	function : Square(value : Int) ~ Int {
		return value * value;
	}


JIT コンパイルによるメソッドと関数
----------------------------------

プログラムの処理速度を高速化するには、 JIT でメソッドや関数の
バイトコードをマシンコードへ事前コンパイルできることがあります。
メソッドや関数は初回呼び出し時にコンパイルされます。
それ以降に呼び出すとコンパイル済みの各マシンコードを実行します。

指定された関数やメソッドに関して、実行時に JIT コンパイルのマシンコードへ変換するには
**native** キーワードを使います。 JIT コンパイルの候補としては計算上は高価で
頻繁に呼び出されるメソッド・関数、あるいは処理時間のかかるループがある
メソッド・関数が挙げられます。 

この素数プログラムの処理時間を観察するには
**native** キーワード指定の有無で比較してください。

図 7 – JIT コンパイルによる素数

.. code-block:: ruby

	class FindPrime {
		function : Main(args : System.String[]) ~ Nil {
			Run(100000);
		}
	
		function : native : Run(topCandidate : Int) ~ Nil {
			candidate : Int := 2;
			while(candidate <= topCandidate) {
				trialDivisor : Int := 2;
				prime : Int := 1;
				found : Bool := true;
				while(trialDivisor * trialDivisor <= candidate & found) {
					if(candidate % trialDivisor = 0) {
						prime := 0;
						found := false;
					}
					else {
						trialDivisor += 1;
					};
				};
	
				if(found) {
					candidate->PrintLine();
				};
				candidate += 1;
			};
		}
	}


ライブラリの作成方法
--------------------

クラスライブラリの作成は割と簡単です。 クラスをファイルに記述してから、
"\ **-tar lib**\ " オプションでコードをコンパイルします。
なお、クラスとファイルは一本、またはそれ以上で構成可能です。 
クラスライブラリのコードに "main" 関数は記述できません。

.. code-block:: ruby

	class Pair {
		@key : Compare;
		@value : Base;
	
		New(key : Compare, value : Base) {
			@key := key;
		@value := value;
		}
	
		method : public : GetKey() ~ Compare {
			return @key;
		}
	
		method : public : Get() ~ Base {
			return @value;
		}
	}


コードをコンパイルするには以下を入力します:

.. code-block:: bash

	obc -src pair.obs –tar lib -dest pair.obl


ライブラリをプログラムで使うには以下を入力します:

.. code-block:: bash

	obc -src points.obs –lib pair.obl -dest point.obe


デバッガの用法
==============

コマンドラインデバッガはプログラムの実行時に、その動作をプログラマが
検証できるようにします。 デバッガを使うには、最初にデバッグシンボル付きで
プログラムを必ずコンパイルしてください。これにはコンパイラへ \"-**debug**\"
オプションを渡します。

このドキュメントの「演算子」セクションにあるクレジットカードの
簡易認証プログラムを例題として扱います。 まず、UTF-8 (または ASCII)
形式でテキストファイル **luhn.obs** をプログラムとして保存してください。 
以下のコマンドはデバッグ版の実行可能ファイル **luhn.obe**
を作成します。 

コードをコンパイルするには以下を入力します:

.. code-block:: bash

	obc -src luhn.obs -dest luhn.obe -debug


この用例では、ソースファイルが実行可能ファイルと同じ場所にあると
想定します。デバッガを起動するには以下を入力してください:

.. code-block:: bash

	obd -exe luhn.obe -src .


はじめに、ブレークポイントを 17 行目に設定してからプログラムを実行します。

.. code-block:: bash

	> b luhn.obs:17
	added breakpoint: file='luhn.obs:17'
	> r
	break: file='luhn.obs:17', method='Luhn->Main(..)'


つぎに、ブレークポイント周辺のコードをリスト表示します。

.. code-block:: ruby

	> l
		12: };
		13: return (oddSum + evenSum) % 10 = 0;
		14: }
		15:
		16: function : Main(args : String[]) ~ Nil {
	=>      17: IsValid("49927398716")->PrintLine();
		18: IsValid("49927398717")->PrintLine();
		19: IsValid("1234567812345678")->PrintLine();
		20: IsValid("1234567812345670")->PrintLine();
		21: }
		22: }


さて、 \"IsValid\" 関数へステップインします。

.. code-block:: ruby

	> s
	> break: file='luhn.obs:2', method='Luhn->IsValid(..)'
	> l
		1: class Luhn {
	=>      2: function : IsValid(cc : String) ~ Bool {
		3: isOdd := true; oddSum := 0; evenSum := 0;
		4: for(i := cc->Size() - 1; i >= 0; i -= 1;) {
		5: digit : Int := cc->Get(i) - '0';
		6: if(isOdd) {
		7: oddSum += digit;
		8: } else {
		9: evenSum += digit / 5 + (2 * digit) % 10
		10: };
	> n


\"cc\" の値を表示します。

.. code-block:: bash

	> p cc
	print: type=System.String, value="49927398716


さて、 9 行目でブレークして \"evenSum\" の値を表示します。

.. code-block:: bash

	> b 9
	added breakpoint: file=’luhn.obs:9’
	> c
	> break: file=’luhn.obs:9’, method=’Luhn->IsValid(..)’
	> n
	> break: file=’luhn.obs:11’, method=’Luhn->IsValid(..)’
	> p evenSum
	print: type=Int, value=2


最後に、コールスタックを終了前に出力します。

.. code-block:: bash

	> stack
	stack:
	frame: pos=2, class=Luhn, method=IsValid(o.System.String), file=luhn.obs:5
	frame: pos=1, class=Luhn, method=Main(o.System.String*), file=luhn.obs:17
	> q
	breakpoints cleared.
	goodbye.


表 6 – デバッガのコマンド

+---------------+------------------------------------+----------------------+
| コマンド      | 概要                               | 用例                 |
+===============+====================================+======================+
| **[b]** reak  | ブレークポイントの設定             | b luhn.obs:17        |
|               |                                    |                      |
|               |                                    | b                    |
+---------------+------------------------------------+----------------------+
| breaks        | ブレークポイントの全表示           |                      |
+---------------+------------------------------------+----------------------+
| **[d]** elete | ブレークポイントの削除             | d luhn.obs:17        |
+---------------+------------------------------------+----------------------+
| clear         | ブレークポイントの全消去           |                      |
+---------------+------------------------------------+----------------------+
| **[n]** ext   | 同じメソッドや関数内の次行にある   |                      |
|               | デバッグ情報へ移動                 |                      |
|               |                                    |                      |
+---------------+------------------------------------+----------------------+
| **[s]** tep   | 次行にあるデバッグ情報へ移動       |                      |
|               |                                    |                      |
+---------------+------------------------------------+----------------------+
| **[j]** ump   | 現在のメソッドや関数から           |                      |
|               | ジャンプすることで次行にある       |                      |
|               | デバッグ情報へ移動                 |                      |
+---------------+------------------------------------+----------------------+
| args          | プログラムの引数を指定             | args \"Hello World\" |
+---------------+------------------------------------+----------------------+
| **[r]** un    | ロード済みのプログラムを実行       |                      |
+---------------+------------------------------------+----------------------+
| **[p]** rint  | メタデータと併せて、式の値を表示   | p cc                 |
|               |                                    |                      |
+---------------+------------------------------------+----------------------+
| **[l]** ist   | ソースファイル全体の行、           | L                    |
|               | または現在のブレークポイント付近の |                      |
|               | 行をリスト表示します。             |                      |
+---------------+------------------------------------+----------------------+
| **[i]** nfo   | クラスに関する変数を表示           | i                    |
+---------------+------------------------------------+----------------------+
| stack         | メソッドや関数のコールスタックに   |                      |
|               | 関するスタックの表示               |                      |
+---------------+------------------------------------+----------------------+
| exe           | 新しい実行可能ファイルのロード     | exe \"luhn.obe\"     |
+---------------+------------------------------------+----------------------+
| src           | 新しいソースパスの指定             | src \".\"            |
+---------------+------------------------------------+----------------------+
| **[q]** uit   | 現在のデバッグセッションを終了     |                      |
+---------------+------------------------------------+----------------------+
