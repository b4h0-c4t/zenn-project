---
title: "すべての主要ブラウザでshadowrootmode実装 - What's new in Browsers!"
emoji: "🎍"
type: "tech"
topics: ["Firefox", "browser", "frontend"]
published: false
publication_name: "cybozu_frontend"
---

https://www.mozilla.org/en-US/firefox/123.0/releasenotes/

What's new in Browsers!は、サイボウズのフロントエンドエンジニアがブラウザの最新情報から気になるトピックを紹介するシリーズです。

今回はFirefox 123から `shadowrootmode` とWebCodec APIについて紹介します。

## `<template>` の `shadowrootmode` サポート

https://developer.mozilla.org/en-US/docs/Web/HTML/Element/template

`<template>` 要素の属性として `shadowrootmode` を指定することが可能になりました。
この機能によって、`<template>`要素を用いた宣言的なHTMLへのShadow Root追加が可能になります。

Interop 2024の重点領域に[Declarative Shadow DOM](https://developer.chrome.com/docs/css-ui/declarative-shadow-dom)が含まれており、`shadowrootmode` はこの領域に紐づく実装となっています。

既存のShadow DOMの実装は、`attachShadow()` を利用して任意のHTML要素にShadow Rootを追加することが一般的でした。

```javascript
const host = document.getElementById('shadowroot');
const shadowRoot = host.attachShadow({mode: 'open'});
shadowRoot.innerHTML = '<h1>Hello Shadow DOM</h1>';
```

このような命令型APIによるShadow Rootの実装は、クライアントサイドレンダリングの場合は問題なく動作します。
一方、サーバサイドレンダリングを用いてHTMLを生成している場合、`attachShdow()` を用いた実装ではShadow DOMのレンダリングが他コンテンツよりも遅れてしまう等の問題が発生します。

Declarative Shadow DOMでは、`shadowrootmode` を用いた `<template>` をHTMLへ記述することで、HTMLの読み込み時点でShadow Rootを生成します。

```html
<div>
  <template shadowrootmode="open">
    <style>
      p {
        margin: 0;
        padding: 4px;
      }
    </style>
    <p>This is Shadow DOM</p>
  </template>
</div>
```

`shadowrootmode` が指定された `<tempate>` 内部の要素は即座にレンダリングへ反映され、Shadow Rootが設定された状態となります。
この機能によって前述した課題が解決され、サーバサイドレンダリングを用いた開発でも問題なくShadow DOMを活用できるようになります。

`shadowrootmode` は、Firefox 123での対応を以てデスクトップ・モバイルともに全ての主要ブラウザで利用可能になりました。

## WebCodecs API

https://developer.mozilla.org/en-US/docs/Web/API/WebCodecs_API

Web Codecs APIは、Web開発者がビデオストリームをより低レベルで操作するための実験的なAPIです。

ビデオストリームのようなメディアを扱うためのAPIには既に[Web Audio API](https://developer.mozilla.org/ja/docs/Web/API/Web_Audio_API)や[WebRTC API](https://developer.mozilla.org/ja/docs/Web/API/WebRTC_API)といったものが存在しています。
一方で、これらのAPIはビデオストリームのフレームやビデオや音声がミックスされていない状態で扱うことはできません。

Web開発者はWebAssemblyで独自に機能を実装することでこの制約を回避してきました。
しかし、既にブラウザに組み込まれているにも関わらず、WebAssemblyで取り扱うためのコーデックを別途ダウンロードする必要があるため非効率でした。

WebCodecs APIはこの問題を解決するため、ブラウザに組み込まれているコーデックへの低レベルなアクセスを可能にしました。

現在、WebCodecs APIには後述の機能へアクセスが可能です。

- 生ビデオフレーム
- 音声データチャンク
- 画像デコーダ
- オーディオ及びビデオのデコーダ

また、現状ではメディアコンテナから音声とビデオを分離できないため、別途サードパーティのライブラリを使うことが推奨されています。

WebCodecs APIは、Firefox 123から `about:config` にて `dom.media.webcodecs.enabled` フラグを有効化することで利用可能です。
他主要ブラウザについては、Chrome及びEdgeがサポート済み、Safariが部分的にサポートされています。