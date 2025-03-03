---
type: doc
layout: reference
category: Basics
title: コーディング規約
---

<!--original
- --
type: doc
layout: reference
category: Basics
title: Coding Conventions
- --
-->

# コーディング規約

<!--original
# Coding Conventions
-->

このページでは、Kotlin言語の現在のコーディングスタイルを紹介します。

<!--original
This page contains the current coding style for the Kotlin language.
-->

## 命名スタイル

よく分からない場合はJava のコード規約に従ってください：


<!--original
## Naming Style
If in doubt default to the Java Coding Conventions such as:
-->

* キャメルケースの使用（そして命名でのアンダースコアの使用を避ける）
* 型は大文字で始まる
* メソッドとプロパティは小文字で始まる
* 4スペースインデントの使用
* public関数はKotlin Docに登場するようなドキュメンテーションがないといけない

<!--original
* use of camelCase for names (and avoid underscore in names)
* types start with upper case
* methods and properties start with lower case
* use 4 space indentation
* public functions should have documentation such that it appears in Kotlin Doc
-->

### 関数の名前

関数、プロパティ、ローカル変数の名前は小文字で始まり、キャメルケース(camel case)を使ってアンダースコアは無しです：
（訳注：キャメルケースとはラクダのようなでこぼこした大文字小文字から来ていて、単語の区切りだけ大文字、それ以外は小文字とするルール）


```kotlin
fun processDeclarations() { /*...*/ }
var declarationCount = 1
```

規則の例外： クラスのインスタンスを作るファクトリーメソッドは返す抽象型と同じ名前にしても構いません：

```kotlin
interface Foo { /*...*/ }

class FooImpl : Foo { /*...*/ }

fun Foo(): Foo { return FooImpl() }
```

## コロン

<!--original
## Colon
-->

コロンが型と継承元のセパレータとして使用される際は、一つ前にスペースが必要です。 一方、インスタンスと型のセパレータとして使用するときには、スペースは不要です。

<!--original
There is a space before colon where colon separates type and supertype and there's no space where colon separates instance and type:
-->

``` kotlin
interface Foo<out T : Any> : Bar {
    fun foo(a: Int): T
}
```

<!--original
``` kotlin
interface Foo<out T : Any> : Bar {
    fun foo(a: Int): T
}
```
-->

## ラムダ

<!--original
## Lambdas
-->

ラムダ式では、スペースが波括弧の周りに必要です。また、パラメータを本体と分かつアロー（->）も同様です。 可能な限り、ラムダを括弧の外に渡す必要があります。

<!--original
In lambda expressions, spaces should be used around the curly braces, as well as around the arrow which separates the parameters
from the body. Whenever possible, a lambda should be passed outside of parentheses.
-->

``` kotlin
list.filter { it > 10 }.map { element -> element * 2 }
```

<!--original
``` kotlin
list.filter { it > 10 }.map { element -> element * 2 }
```
-->

短くてネストされていない（入れ子でない）ラムダ内では、 パラメータを明示的に宣言する代わりに `it` 規約を使用することを推奨します。パラメータを持つネストされたラムダでは、パラメータを常に明示的に宣言する必要があります。

<!--original
In lambdas which are short and not nested, it's recommended to use the `it` convention instead of declaring the parameter
explicitly. In nested lambdas with parameters, parameters should be always declared explicitly.
-->

### トレーリングカンマ

（訳注：リンクを貼るので一時的にここだけ最新の和訳にアップデートします）

トレーリングカンマ(trailing comma)はカンマのシンボルが最後の要素の後にもついているものの事を言います：

```kotlin
class Person(
    val firstName: String,
    val lastName: String,
    val age: Int, // トレーリングカンマ
)
```

トレーリングカンマを使う事は、幾つかの利点があります：

* バージョン管理ソフトのdiffが綺麗になる - 皆変更の場所だけを集中してみたいのだから
* 要素を追加したり順番を変えるのが簡単になる - 最後になったらカンマを削除したり最後じゃなくなったらカンマを追加したりしなくて良い
* コード生成などでオブジェクトの初期化を出力するのが楽になる。最後の要素でも気にせずカンマを出せば良いので

トレーリングカンマはいつでもオプショナルです - あなたのコードはトレーリングカンマ無しでも動きます。
Kotlinのスタイルガイドラインとしては宣言側ではトレーリングカンマを使う事を推奨しています。
呼ぶ側はあなたの好きなように選んで良い事になっています。

IntelliJ IDEAフォーマッタでトレーリングカンマを有効にするには、**Settings/Preferences | Editor | Code Style | Kotlin**に行って、
**Other**タブを開いて、**Use trailing comma**オプションを選びます。

## ユニット (Unit)

<!--original
## Unit
-->

関数がUnitを返す場合、戻り値の型は省略されるべきです：

<!--original
If a function returns Unit, the return type should be omitted:
-->

``` kotlin
fun foo() { // ": Unit" が省略されている

}
```

<!--original
``` kotlin
fun foo() { // ": Unit" is omitted here

}
```
-->