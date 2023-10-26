---
title: "Firefox 119 から注目の新要素を紹介 - What's new in Browsers!"
emoji: "🎃"
type: "tech"
topics: ["Firefox", "browser", "frontend"]
published: false
publication_name: "cybozu_frontend"
---

What's new in Browsers!は、サイボウズのフロントエンドエンジニアがブラウザの最新情報から気になるトピックを紹介するシリーズです。

今回は Firefox 119 からサポートされた機能 ARIA reflection と `Cross-Origin-Embedder-Policy: credentialless` を紹介します。

## ARIA reflection

HTML 要素の aria 属性を `setAttribute()` メソッドを使用せずに参照・変更ができるようになりました。

以前は特定の要素に対して JavaScript 上から aria 属性を追加、変更する場合、後述のようなコードを書く必要がありました。

```js
buttonElement.setAttribute("aria-pressed", "true");
```

Firefox 119 のアップデートによって DOM API から直接 aria 属性を参照、更新できるようになります。

```js
buttonElement.ariaPressed = true;
```

このアップデートによる恩恵として、`setAttribute()` を用いたテキストベースの属性検索と比べて VSCode 等のエディター上での補完機能を活用できる点が挙げられます。
また、TypeScript の `HTMLElement` 属性に追加されれば型の保証を受けることも可能になります。

一方で、今回追加された ARIA reflection の対応は non-IDREF である ARIA 属性に限定されている点には注意が必要です。
例えば、`aria-labbelledby` のように他の要素を参照するような属性に対しては DOM API から値を参照、変更することができません。
この辺りの実装に関しては他主要ブラウザでもまだ未実装のため、今後に期待しましょう。

今回の Firefox のアップデートによって、主要なブラウザ全てで ARIA reflection がサポート済みになりました。

## `Cross-Origin-Embedder-Policy: credentialless`

Cross Origin Embedder Policy (COEP) は HTTP フィールドの一つで、サイドチャネル攻撃のリスクから通信を守るためのポリシーです。

COEP は、埋め込むリソースに対して Cross Origin Resource Policy (CORP) を命じさせるように強制することができます。
これによってクライアントへ意図しないリソースが読み込まれないことを保証することができます。

以前までは COEP に指定できる値は `require-corp` と `unsafe-none` の二種類がありました。

- `require-corp` は全てのサブリソースに対して CORP の指定を強制し、読み込むクロスオリジンリソースとして的確でないものをブロックします。
- `unsafe-none` は CORP の指定がなくともクロスオリジンリソースを読み込むことを許可します。

COEP によるリソース制御を有効にするためには `require-corp` の指定が必要ですが、全てのサブリソースに対して CORP を指定することは現実的に難易度が高いと言えます。

今回サポートされた `credentialless` では、CORP が不適格なリソースの読み込みをブロックする他に、クロスオリジンのリクエスト制御に関する指定がないリソースに対して cookies 等のクレデンシャルを除外したリソースの読み込みを許可します。
これによって機密性の高いリソースへのアクセスは COEP の指定によりブロックしつつ、それ以外のリソースはクロスオリジン設定をせずとも制限付きで読み込むことが可能になりました。

この機能は現在、主要ブラウザのうち Safari 以外はサポート済みです。
