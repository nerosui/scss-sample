# LESSON1

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

ですが、厳密な WordPress のコーディングルールではメディアクエリは最後にまとめて書くようにすることになっています。  
Gutenberg ではそんな制約はないので、いつでもどこでも OK(そもそも minify されて見えない)
