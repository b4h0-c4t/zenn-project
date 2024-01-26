---
title: "<select>要素がより扱いやすく - What's new in Browsers!"
emoji: "🎍"
type: "tech"
topics: ["Firefox", "browser", "frontend"]
published: false
publication_name: "cybozu_frontend"
---

https://www.mozilla.org/en-US/firefox/122.0/releasenotes/

What's new in Browsers!は、サイボウズのフロントエンドエンジニアがブラウザの最新情報から気になるトピックを紹介するシリーズです。

今回はFirefox 122からサポートされた機能の中からLargestContentfulPaint APIと<select>要素に追加された2つの新機能について紹介します。

## LargestContentfulPaint API

https://developer.mozilla.org/en-US/docs/Web/API/LargestContentfulPaint

Performance APIsの1つである、LargestContentfulPaint APIがサポートされました。
このAPIは、ユーザの入力前に大きなコンテンツが描画されるタイミングに関する情報を提供できます。

既存のPerformance APIsと同様に[PerformanceEntry](https://developer.mozilla.org/ja/docs/Web/API/PerformanceEntry)から継承されており、計測を実施したい対象となるWebサイトにオブザーバーを設置することで利用できます。

```javascript
const observer = new PerformanceObserver((list) => {
  const entries = list.getEntries();
  const lastEntry = entries[entries.length - 1]; // Use the latest LCP candidate
  console.log("LCP:", lastEntry.startTime);
  console.log(lastEntry);
});

observer.observe({ type: "largest-contentful-paint", buffered: true });
```

取得できる主な計測対象としては下記のものが挙げられます。

- <img>要素
- SVGに含まれる<img>要素
- <video>要素の `poster` 属性に含まれる画像
- `background-image` を持つ要素
- <p>などのテキストノード

これら要素の描画時間など、LCPに関わるメトリクスを収集することが可能になります。

LargestContentfulPaint APIは、Firefox 122の実験的導入を以てSafari以外の主要ブラウザ全ての機能がサポートされました。

## `showPicker()` method in <select>

https://developer.mozilla.org/en-US/docs/Web/API/HTMLSelectElement/showPicker

<select>要素に `showPicker()` メソッドがサポートされました。
`showPicker()` は、JavaScript経由で<select>要素のピッカーを展開できるメソッドです。

```html:showpicker.html
<section>
  <h2>Show Picker!</h2>
  <select>
    <option value="foo">foo</option>
    <option value="bar">bar</option>
    <option value="baz">baz</option>
  </select>
  <button type="button">show picker!</button>
</section>
```

```javascript:showpicker.js
const button = document.querySelector("button");
const select = document.querySelector("select");

button.addEventListener("click", () => {
  select.showPicker();
})
```

@[codepen](https://codepen.io/b4h0-c4t/pen/ExMbxob)

上のcodepenでは、iframeを埋め込んでいる関係でsame-originエラーが発生しています。
Zenn上で動作例は表示できませんが、同様の実装を手元で実施してもらうことで確認ができます。

`showPicker` メソッドは、Safari on iOS以外の全てのブラウザで実験的に導入がされています。(Safari on macOSはTP)

## <hr> in <select>

https://developer.chrome.com/blog/hr-in-select

<select>要素の中で<hr>が利用可能になりました。
これによってリストをより視覚的に分割することが可能になります。

```javascript
<select name="majors" id="major-select">
  <option value="">Select a major</option>
  <hr>
  <option value="arth">Art History</option>
  <option value="finearts">Fine Arts</option>
  <option value="gdes">Graphic Design</option>
  <option value="lit">Literature</option>
  <option value="music">Music</option>
  <hr>
  <option value="aeroeng">Aerospace Engineering</option>
  <option value="biochemeng">Biochemical Engineering</option>
  <option value="civileng">Civil Engineering</option>
  <option value="compeng">Computer Engineering</option>
  <option value="eleng">Electrical Engineering</option>
  <option value="mecheng">Mechanical Engineering</option>
  <hr>
  <option value="polysci">Political Science</option>
  <option value="intr">International Relations</option>
  <option value="bizdev">Business Development</option>
  <hr>
  <option value="math">Mathematics</option>
  <option value="econ">Economics</option>
  <option value="stat">Statistics</option>
</select>
```

@[codepen](https://codepen.io/web-dot-dev/pen/GRzKzVK)

<select>要素内の<hr>対応は、Safari on iOS以外全ての主要ブラウザで一部導入されています。
アクセシビリティツリーに表示されないなどの制約がある状態での導入ですが、基本的な表示はどのブラウザでも試すことができます。
