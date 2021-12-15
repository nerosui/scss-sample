# LESSON 2

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

CSS にもカスタムプロパティがあり、クライアントが変更したり、バリエーションを出したいときはカスタムプロパティを使う方がいい。  
SCSS の変数は定数を設定するときなどに利用する。

## 関数 @for

SCSS であらかじめ用意されている[関数](https://book.scss.jp/code/c8/07.html)があります。
全部使う必要はありませんが、知識として覚えておきましょう。

```scss
.flex-row {
  div {
    &.content {
      article {
        @for $i from 1 through 5 {
          &:nth-child(#{$i}) {
            background-color: lighten(rgba(0, 0, 0, 0.8), $i * 20%);
            color: darken(rgba(255, 255, 255, 0.9), $i * 20%);
          }
        }
      }
    }
  }
}
```

```css
.flex-row div.content article:nth-child(1) {
  background-color: rgba(51, 51, 51, 0.8);
  color: rgba(204, 204, 204, 0.9);
}
.flex-row div.content article:nth-child(2) {
  background-color: rgba(102, 102, 102, 0.8);
  color: rgba(153, 153, 153, 0.9);
}
.flex-row div.content article:nth-child(3) {
  background-color: rgba(153, 153, 153, 0.8);
  color: rgba(102, 102, 102, 0.9);
}
.flex-row div.content article:nth-child(4) {
  background-color: rgba(204, 204, 204, 0.8);
  color: rgba(51, 51, 51, 0.9);
}
.flex-row div.content article:nth-child(5) {
  background-color: rgba(255, 255, 255, 0.8);
  color: rgba(0, 0, 0, 0.9);
}
```

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
