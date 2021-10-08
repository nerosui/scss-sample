# Sass の利用レクチャー資料

## Sass の概要

<details>
<summary>Sassの概要</summary>
<div>

    簡単にいうと「CSS を効率的に書くための記法」

    記法 sass と scss があって今回は scss を行う

    公式サイト : https://sass-lang.com/

    今回は導入が簡単な 🆚 Code extension の[DartJS Sass Compiler and Sass Watcher](https://marketplace.visualstudio.com/items?itemName=codelios.dartsass)を利用する。

    https://marketplace.visualstudio.com/items?itemName=codelios.dartsass

</div>
</details>

## 対象と資料の範囲

---

### 対象となる人

<details>
<summary>対象となる人</summary>
<div>

- HTML と CSS3 が一通りかける。
- 変数や引数などの初歩のプログラミングが理解できる。
- VSCode 使いの人

</div>
</details>

### 対象となる Sass の範囲

<details>
<summary> 対象となる Sass の範囲</summary>
<div>

- 変数
- ネスト記法
- 一部の組み込み関数
- ループ処理や論理演算、関数は対象外

</div>
</details>

---

## インストール方法

- VSCode の extension から DartJS Sass Compiler and Sass Watcher をインストール

## はじめての Sass

- 適当なフォルダに scss ファイルを作る。
- 保存する。-> css ファイルが自動で作られる。
- 同時に min.css も作られる。
  - 保存先の変更やオプションは設定から行う。

ブラウザで確認  
開発ツールでSCSSまで参照できているのを確認する  

- トランスパイルエラーが起きるとVSCodeが教えてくれます。 => typoが少なくなります。

---

## 入れ子構造を使ってみよう

### 入れ子構造

scss を以下のようにすると

```scss
header {
  background-color: gray;
  width: 100%;
  .title {
    font-size: 3em;
  }
  // &をつけると親を参照します。
  &.dark-theme {
    background-color: gray;
  }

  // headerの中の.title **１行コメントはスラッシュ２個
  /* 従来のコメントも使えます */
}
```

出力は以下のようになります。

```css
header {
  background-color: grey;
  width: 100%;
}
header .title {
  font-size: 3em;
}
/* &をつけると親を参照します。*/
header.dark-theme {
  background-color: grey;
}
```

## メディアクエリ

入れ子の中でメディアクエリが使えます。

SCSS

```scss
header {
  border-bottom: 3px solid #efefef;

  @media screen and (min-width: 62.5em) {
    border-bottom: none;
  }
}
```

CSS

```css
header {
  border-bottom: 3px solid #efefef;
}
@media screen and (min-width: 62.5em) {
  header {
    border-bottom: none;
  }
}
```

ですが、厳密なWordPressのコーディングルールではメディアクエリは最後にまとめて書くようにする。
Gutenbergではそんな制約はないので、いつでもどこでもOK(そもそもminifyされて見えない)

## 変数を使ってみよう

データ型（数値、文字列、真偽、色、リスト）

変数の宣言と初期化

```scss
$base-font-size: 16px;

// 色を変数に
$grey-color: grey;
$base-color: rgba(210, 210, 210, 0.5);

// 文字列も
$dir: "../assets/";
$img: $dir + "image.png";

// 四則演算ができる + - * /
$second-font-size: $base-font-size - $base-font-size / 4;

// CSSの関数内で使う時などは#{}で囲む
.sub {
  font-size: calc(#{$base-font-size} - var(--main-font-size));
}

// !defaultをつけると値がない場合のみセットされる。
$grey-color: red !default;
```

CSSにもカスタムプロパティがあり、クライアントが変更したり、バリエーションを出したいときはカスタムプロパティを使う方がいい。  
SCSSの変数は定数を設定するときなどに利用する。

## 色を扱ってみよう

### lighten / darken

ビルドインモジュールの一つ、明るさをある一定量変更する。上限下限などが厳密ではない。  
他にも hsl 単位で変更するものなどがある。  
厳密に変更するのであれば scale-color を使う

```scss
div {
  background-color: lighten(rgba(0, 0, 0, 0.8), 20%);
  color: darken(rgba(255, 255, 255, 0.9), 20%);
}
```

```css
div {
  background-color: rgba(51, 51, 51, 0.8);
  color: rgba(204, 204, 204, 0.9);
}
```

## ファイルを分離させてみよう

### @import

```scss
@import "style";
```

拡張子をつけない場合、自動的に scss ファイルを読み込みます。  
CSS とは違い、トランスパイル時に全て一つのファイルに読み込まれます。  
アンダースコアをファイル名の先につけると、トランスパイル時に出力されないファイルになります。(partial ファイルと言います)。

### @use @forward

@import はグローバル空間を使っているので、誰がどこの段階で上書きしているのかわかりにくい。  
そのため、今後の CSS では@use を使いカプセル化を行っていく方針です。  
現状では@import を使っているフレームワークも多いので、完全な対応は不要ですが 、将来的には移行されると思われます。

---

## @mixin @include @extend

### @mixin @include

よく使う設定を@mixinで定義してincludeで呼び出します。

```scss
@mixin border($color:#666) {
  border-bottom: 1px solid $color;
}

#header {
  @include border(#999); 

  #gnav {
    overflow: hidden;
    @include border;
  }
}
```

```css
#header {
  border-bottom: 1px solid #999999;
}

#header #gnav {
  overflow: hidden;
  border-bottom: 1px solid #666666;
}
```

### @extend

css は継承元になるところにセレクタをカンマ区切りで列挙する仕様  
例: A を継承して B を作る A,B{font-size:16px}  
@extend は継承先に書くことができる

```scss
h1 {
  font-size: 3rem;
}
.h1 {
  @extend h1;
}

// セレクタにしたくないときはプレースホルダを使う
%box {
  margin-top: 15px;
  padding: 10px;
  background-color: #ccc;
}

.contenteBox {
  @extend %box;
  p {
    line-height: 1.3;
  }
}

.noteBox {
  @extend %box;
}
```

```css
h1,
.h1 {
  font-size: 3rem;
}

.contenteBox, .noteBox {
  margin-top: 15px;
  padding: 10px;
  background-color: #ccc;
}

.contenteBox p {
  line-height: 1.3;
}
```
