---
title: "画面キャプチャをより厳密にできるElement Capture API - What's new in Browsers!"
emoji: "🍫"
type: "tech"
topics: ["Firefox", "browser", "frontend"]
published: false
publication_name: "cybozu_frontend"
---

https://developer.chrome.com/blog/new-in-chrome-121?hl=en

What's new in Browsers!は、サイボウズのフロントエンドエンジニアがブラウザの最新情報から気になるトピックを紹介するシリーズです。

今回はChrome 121からOrigin Trialが開始されたElement Capture APIについて紹介します。

## Element Capture API

https://developer.chrome.com/docs/web-platform/element-capture

Element Capture APIは、任意のHTML要素をキャプチャするためのAPIです。
主なユースケースとして、通話アプリケーションでの画面共有の実装が挙げられます。

### 既存の画面キャプチャ

ユーザの画面をキャプチャし、メディアストリーム化する既存のAPIとしてScreen Capture APIがあります。
以前まではChrome 104でサポートされた[Region Caputure](https://developer.chrome.com/docs/web-platform/region-capture?hl=ja)と呼ばれる手法で画面の切り抜きを実現していました。

```javascript
const captureTarget = document.querySelector("#captureTarget");
const cropTarget = await CropTarget.fromElement(mainContentArea);
```

このAPIは座標に依存せず、任意のHTML要素をターゲットとして画面の切り抜きを行うため、表示ずれによる意図しない情報の送信を防ぐことができました。

一方、Region Captureはターゲットの位置とサイズを基準として画面に表示されているピクセルをキャプチャします。
これにより、指定した要素上に異なる要素がfixされている場合は上に重なっている要素をキャプチャするため、意図しない要素がキャプチャに映り込んでしまうことがありました。

### 課題の解決

Element Capture APIは、指定した要素のサブツリーを切り出して、そこに含まれるDOMのみをキャプチャします。

```javascript
const captureTarget = document.querySelector("#captureTarget");
const restrictionCropTarget = await RestrictionTarget.fromElement(
  captureTarget
);
```

切り抜く領域の厳密性が保たれることで、意図しない領域のキャプチャによるセキュリティリスクがより軽減されます。

### 機能の有効化

この機能を試すには、以下のフラグを有効化する必要があります。

- chrome://flags/#enable-experimental-web-platform-features
- chrome://flags/#element-capture
