# LESSON 3

---

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

よく使う設定を@mixin で定義して include で呼び出します。

```scss
@mixin border($color: #666) {
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

.contenteBox,
.noteBox {
  margin-top: 15px;
  padding: 10px;
  background-color: #ccc;
}

.contenteBox p {
  line-height: 1.3;
}
```
