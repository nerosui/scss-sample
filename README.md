# Sass の利用レクチャー資料

## Sass の概要

<details>
<summary>Sassの概要</summary>
<div>

    簡単にいうと「CSS を効率的に書くための記法」

    記法 sass と scss があって今回は scss を行う

    公式サイト : https://sass-lang.com/

    今回は導入が簡単な 🆚 Code extension の
    [DartJS Sass Compiler and Sass Watcher](https://marketplace.visualstudio.com/items?itemName=codelios.dartsass)
    を利用する。

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

## Sass CSS などの関連用語説明

- トランスパイル：変換すること。scss から css にトランスパイルする
- minify：改行などを削除しファイル容量を減らすこと
- BEM 記法：CSS の記法の一つ parent--content\_\_child--content などのように記載する

---

## インストール方法

- VSCode の extension から DartJS Sass Compiler and Sass Watcher をインストール

## はじめての Sass

- 適当なフォルダに scss ファイルを作る。
- 保存する。-> css ファイルが自動で作られる。
- 同時に min.css も作られる。
  - 保存先の変更やオプションは設定から行う。

ブラウザで確認  
開発ツールで SCSS まで参照できているのを確認する

- トランスパイルエラーが起きると VSCode が教えてくれます。 => typo が少なくなります。

## LESSONS

- [LESSON1](lesson/lesson1/README.md)
- [LESSON2](lesson/lesson2/README.md)
- [LESSON3](lesson/lesson3/README.md)

## 実践編

- [Bootstrap5のScss](lesson/bootstrap/README.md)