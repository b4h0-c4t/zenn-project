---
title: ":has() が全ての主要ブラウザで利用可能に！ - What's new in Browsers!"
emoji: "🎅"
type: "tech"
topics: ["Firefox", "browser", "frontend"]
published: true
publication_name: "cybozu_frontend"
---

https://www.mozilla.org/en-US/firefox/121.0/releasenotes/

What's new in Browsers!は、サイボウズのフロントエンドエンジニアがブラウザの最新情報から気になるトピックを紹介するシリーズです。

今回は Firefox 121 からサポートされた機能の中から `:has()` と iframe の遅延読み込みについて紹介します。

## `:has()`

https://developer.mozilla.org/ja/docs/Web/CSS/:has

`:has()` は CSS の擬似クラスで、引数に渡した相対セレクタとマッチする要素が存在する要素を表します。

例えば、このようなスタイルを記述した場合、子要素に `h2` を含む `section` に対して `border: solid 1px #333` を適用するという表現になります。

```css
section:has(> h2) {
  border: solid 1px #333;
}
```

`:has()` の登場により、以前までは JavaScript を用いて表現する必要があった特定の子要素を含む親要素の表現を CSS のみで完結させられるようになりました。

前述したスタイルを例に `:has()` 以前との実装例を比較するのこのようになります。

```html:index.html
<h1>border with(out) :has()</h1>
<section>
  <h2>h2 title</h2>
  <p>hoge</p>
  <section>
    <h3>h3 title</h3>
    <p>fuga</p>
  </section>
</section>
<section>
  <h3>h3 title</h3>
  <p>fuga</p>
</section>
```

@[codepen](https://codepen.io/b4h0-c4t/pen/dyrbVBX)

```css:with_has.css
section:has(> h2) {
  border: solid 1px #333;
}
```

@[codepen](https://codepen.io/b4h0-c4t/pen/MWxgOKd)

```css:without_has.css
.section_with_h2 {
  border: solid 1px #333;
}
```

```javascript:without_has.js
const sections = document.querySelectorAll("section");

for (let section of sections) {
  for (let child of section.children) {
    if (child.tagName === "H2") section.className = "section_with_h2";
  }
}
```

より具体的なユースケースについては、[Cybozu Frontend Advent Calendar 2023](https://adventar.org/calendars/9255) 18 日目の記事が参考になるので合わせてご一読ください。

https://zenn.dev/yy616/articles/188e0761277fdf

`:has()` は Firefox 121 でのサポートをもって主要ブラウザ全てで利用可能になりました。

## iframe の遅延読み込み

https://developer.mozilla.org/ja/docs/Web/HTML/Element/iframe#loading

iframe に遅延読み込みの仕組みが導入されました。
これにより、画面外にある iframe の読み込みをユーザのスクロールまで延期できるようになり、ページ全体の読み込みが効率化されます。

iframe の遅延読み込みを有効化するには、対象の iframe の `loading` 属性に対して `lazy` を指定する必要があります。
また、`loading` 属性には `eager` と `lazy` という 2 つの値があり、`eager` はユーザのスクロールを待つことなく iframe を読み込みます。

使い分けとして、iframe 内部のコンテンツがページのメインコンテンツである場合は `eager`、それ以外の場合は `lazy` を指定することになると思われます。

`<iframe loading="lazy">` は Firefox 121 でのサポートをもって主要ブラウザ全てで利用可能になりました。
