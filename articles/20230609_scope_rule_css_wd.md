---
title: "CSS WD にある @scope ルール"
emoji: "🌸"
type: "tech"
topics: ["frontend", "css"]
published: false
publication_name: "cybozu_frontend"
---

# `@scope` ルール

`@scope` は、指定したセレクタを最上位ノードとするサブツリーを基準としたセレクタマッチングを実現できる新機能です。

## シンタックス

`@scope` のシンタックスは後述のように定義されています。

```css
@scope [(<scope-start>)]? [to (<scope-end>)]? {
  <rule-list>
}
```

例えば、後述する例のように `#red` セレクタをスコープした状態で `p` に `color:red` を適用すると、`#red` に含まれる `p` のみにスタイルが適用されます。

```html
<main>
  <div id="red">
    <p>red</p>
  </div>
  <div id="green">
    <p>green</p>
  </div>
  <div id="red">
    <p>blue</p>
  </div>
</main>
```

```css
@scope (#red) {
  p {
    color: red;
  }
}
```

![](/images/20230609_scope_rule_css_wd/scope_example_01.png)

また、`@scope(selector1) to (selector2)` といった記法を用いることで `selector1` を含むその子孫かつ `selector2` の子孫ではない要素をスコープとして指定することができます。

```html
<main>
  <div id="red">
    <p>red</p>
    <div id="magenta">
      <p>magenta</p>
    </div>
    <div id="yellow">
      <p>yellow</p>
    </div>
  </div>
  <div id="green">
    <p>green</p>
  </div>
</main>
```

```css
@scope (#red) to (#yellow) {
  p {
    color: red;
  }
}
```

![](/images/20230609_scope_rule_css_wd/scope_example_02.png)

## `@scope` の影響

`@scope` には 3 つの主要な効果があります。

- `@scope` ブロックに含まれるスタイルはスコープされたスタイルルールとして扱われる
- `:scope` 疑似クラスは `@scope` で指定されたスコープルートに一致するようになる
- カスケードの優先順位にソースの読み込み順や詳細度よりも優先される指標としてスコープルートからの近接(proximate)が適用される

`:scope` は従来、DOM API を用いて要素を取得した際には取得された最上位ノードが、それ以外の場合は `:root` と同様の要素を参照していましたが、`@scope` の指定によって参照先が変更されるようになります。

### 近接

近接とは、スコープルートから指定されたセレクタまでの階層がどれくらい離れているかという指標で、階層が近ければ近いほどスタイルが優先して適用されます。
後述の例の場合、`#low` への近接は `#top` が 2、`#middle` が 1 となるため、`#middle` が指定されている方の `@scope` が優先されて適用されます。

```html
<div id="top">
  <div id="middle">
    <div id="low">hoge</div>
  </div>
</div>
```

```css
@scope (#top) {
  #low {
    color: red;
  }
}

@scope (#middle) {
  #low {
    color: green;
  }
}
```

![](/images/20230609_scope_rule_css_wd/scope_example_03.png)

`@scope` は詳細度を追加しません。
そのため、後述の例ではそれぞれのセレクタに対するスタイルの詳細度は互いに(0,1,0)として処理されますが、スコープが適用されているスタイルには近接が適用されるため優先されます。

```html
<div id="scope">
  <div id="content">hoge</div>
</div>
```

```css
@scope (#scope) {
  #content {
    color: red;
  }
}

#content {
  color: green;
}
```

![](/images/20230609_scope_rule_css_wd/scope_example_04.png)

## スコープルートの検索

`<scope-start>` で指定されたセレクタとマッチする各要素をスコープルートとしてスコープが作成されます。
`<scope-start>` が未指定の場合は、スタイルシートのオーナーノードに対する親要素がスコープルートになります。
後述の例の場合、`<div id="scope">` がスコープルートになります。

```html
<div id="scope">
  <style>
    @scope {
      p {
        color: red;
      }
    }
  </style>
  <p>red</p>
</div>
<p>green</p>
```

## スコープのネスト

`@scope` はネスト可能です。
ネストした場合、子の `@scope` は親の `@scope` セレクタによる制約を受けますが、スタイルは最も近接しているスコープノードからの近接のみ影響を受けます。
後述の例では、これまでの感覚では `color:red` が優先されそうに見えますが、実際には近接が最も近い `color:green` が適用されます。

```html
<div id="top">
  <div id="middle">
    <div id="low">
      <p>hoge</p>
    </div>
  </div>
</div>
```

```css
@scope (#top) {
  @scope (#middle) {
    p {
      color: red;
    }
  }
}

@scope (#low) {
  p {
    color: green;
  }
}
```

![](/images/20230609_scope_rule_css_wd/scope_example_03.png)

## 個人的に気になったこと

`@scope (selector1) to (selector2)` という記法ですが、直感的には `selector1` から `selector2` までの間に含まれる要素にマッチしそうですが、実際には `selector2` の子孫が含まれなくなるという仕様だったので少し困惑しました。
と思っていたのですが、執筆日前日にメーリングリスト似たようなことを言っている人がおり、`to` ではなく `excluding` にしてはどうかと提案していました。

よさそう。

## 最後に

最近 Chrome が [Intent to Ship](https://groups.google.com/a/chromium.org/g/blink-dev/c/OEfGbd74QnQ/m/KaX-2hhRAAAJ) を投稿して話題になっていた `@scope` ですが、個人的にコンポーネント単位のスタイリングに使ってみたいのでぜひ試したいです。
Chrome 117 あたりで利用できそうなの今後に期待ですね。
