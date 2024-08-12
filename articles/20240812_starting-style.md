---
title: "すべての主要ブラウザで利用可能になったアットルール@starting-styleとは"
emoji: "🏃"
type: "tech"
topics: ["frontend", "browser", "css"]
published: false
publication_name: "cybozu_frontend"
---

:::message
この記事は [Cybozu Summer Blog Fes'24](https://cybozu.github.io/summer-blog-fes-2024/) (Frontend Stage) DAY 12の記事です。
:::

本記事では2024-08-06にリリースされた Firefox 129をもって主要なブラウザすべてで利用可能になったアットルール `@start-style` について紹介します。

https://developer.mozilla.org/ja/docs/Web/CSS/@starting-style

## トランジション開始時のスタイルを指定できる `@starting-style`

`@starting-style` はトランジションされる要素に対して、CSS プロパティの開始値を定義するためのプロパティです。

従来の CSS 記法では `display: none;` が指定されている要素にトランジションを使用した場合、トランジションが発生しませんでした。
そこで、`@starting-style` ルールを用いてトランジション開始時のスタイルをしているすることで元の要素に `display: none;` が指定されていたとしても正しくトランジションを発火させることができるようになります。

```css
.open-content {
  display: none;
  width: 100px;

  @starting-style {
    width: 0px;
  }
}

.open {
  display: block;
  transition: width 4s;
}
```

@[codepen](https://codepen.io/b4h0-c4t/pen/xxoXMKV)

### 記法

記法は既存のアットルールと同様に、独立したブロックとして記述する方法か、既存ルールセットの入れ子として記述する方法の二パターンが存在します。

```css
@starting-style {
  .hoge {
    // style
  }
}

.fuga {
  // style

  @starting-style {
    // style
  }
}
```

### 注意点

`@starting-style` は対象となる要素がDOMとしてレンダーされた時もしくは `display: none;` から可視状態になった時のみ機能します。

そのため、たとえば既に描画されているコンテンツにトランジションを発火させる時、トランジションの開始フレームを既存の状態から変化させるといった用途で使用することはできません。

下の例は、すでに表示されている要素にトランジションを適用する際、開始直後に一度透明化させる意図で `@starting-style` を適用したものです。

`display: none;` が適用されている要素は `opacity: 0;` が正しく適用されている一方で、既に表示されている方の要素はトランジションが開始しても透明化されていないことがわかります。

@[codepen](https://codepen.io/b4h0-c4t/pen/PorJvoR)

そのため、一度発火したトランジションを再度同様に発火させるためには `@starting-style` が適用されている要素を削除して再生成するまたは一度 `display:none;` へ状態を戻す必要があります。

もし、描画済みの要素に開始フレームを適用したいのであれば `@starting-style` ではなく、既存の CSS アニメーションを利用するようにしましょう。

### 制限事項

Firefox 129現在、初期状態が `display: none;` となっている要素に対しては `@starting-style` が適用されない部分的サポートという形で導入されています。

今後フルサポートされるまでは Firefoxで前述したような実装ができないため、お気をつけください。