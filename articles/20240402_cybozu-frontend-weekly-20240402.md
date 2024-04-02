---
title: "RedwoodJSがRSCに対応: Cybozu Frontend Weekly (2024-04-02号)"
emoji: "🌸"
type: "tech"
topics: ["CybozuFrontendWeekly", "frontend"]
published: false
publication_name: "cybozu_frontend"
---

## はじめに

こんにちは！サイボウズ株式会社フロントエンドエキスパートチームの [BaHo](https://twitter.com/b4h0_c4t) です。

サイボウズでは毎週火曜日にFrontend Weeklyという「1週間の間にあったフロントエンドニュースを共有する会」を社内で開催しています。

今回は、2024/04/02のFrontend Weeklyで取り上げた記事や話題を紹介します。

## 取り上げた記事・話題

### Making state easy with D1 GA, Hyperdrive, Queues and Workers Analytics Engine updates

https://blog.cloudflare.com/making-full-stack-easier-d1-ga-hyperdrive-queues

CloudflareのD1とHyperdriveがGAになりました。

同時に正式な料金も発表されており、D1は無料枠があるとのことです。
また、この無料博は今後削除する予定がないと強調されていました。

HyperdriveはWorkerd Paid Plan ($5/mo)に入っている場合追加コストなしで利用できます。

### Bun 1.1

https://bun.sh/blog/bun-v1.1

Bun 1.1がリリースされました。

Windows対応やNode.js互換性の向上、WebSocketサポートといったアップデートが盛り込まれています。
Node.jsの互換性に関して、node:fsやnode:pathといった組み込みモジュールごとバンドル可能になっているようです。
他にもマクロ機能やテスト向けのMatcherやMock機能など多くの機能が追加されました。

### 【2024年4月1日のTypeScriptニュース】次期バージョンでオブジェクト型に追加される新機能の紹介

https://qiita.com/uhyo/items/787a475bb618811d3771

※本記事はエイプリルフール記事です。

TypeScriptの時期バージョン5.5.555に実装予定のArranged Field Definitionという機能を紹介するジョーク記事です。
読み応えがあるのでぜひご一読ください。

### React Server Components now in RedwoodJS

https://redwoodjs.com/blog/rsc-now-in-redwoodjs

RedwoodJSがBighornエポックのプレビューにてRSCをサポートしました。

### Intent to prototype & ship: URL.parse()

https://groups.google.com/a/mozilla.org/g/dev-platform/c/3QgJqDYpEwA/m/4n1pJEtqAAAJ

Firefox 126に `URL.parse()` が試験的に導入されます。

### Deno 1.42: Better dependency management with JSR

https://deno.com/blog/v1.42

Deno 1.42がリリースされました。

JSRの第1級サポート、Node.jsやnpmとの互換性に関するアップデートが含まれています。

### 【告知】「フロントエンドカンファレンス北海道2024」を、2024年8月24日（土）に開催します！ 

https://note.com/fec_hokkaido/n/nbb62b53069a5

2024年8月24日土曜日に北海道札幌市にて「フロントエンドカンファレンス北海道2024」が開催されます。
スポンサーやプロポーザルの募集は後日発表とのことです。

### On disabled and aria-disabled attributes

https://kittygiraudel.com/2024/03/29/on-disabled-and-aria-disabled-attributes/

disabled と aria-disabled 属性の使い分け方についてについて解説している記事です。

記事内では、

- disabled：何らかの理由で値が無関係になった要素に使用
- aria-disabled：要素自体はフォーカス可能でvalidationをトリガーできるため、対話的に使用

といった違いがあると解説されています。

### Introducing “pages router”

https://waku.gg/blog/introducing-pages-router

RSCのミニマムフレームワークWakuがファイルベースルーティングをサポートしました。

segment routeやcatch-all segmentなどが使ええるようになり、static renderingとdynamic renderingはファイル内でgetConfig APIを使用することで切り替えられるようになりました。

### React フレームワークの 動向と選定基準 

https://speakerdeck.com/azukiazusa1/react-huremuwakuno-dong-xiang-toxuan-ding-ji-zhun

React フレームワークの動向と選定基準について解説しているスライドです。

Next.jsのRouterやRemixのモード選択なども含めて、モダンなフレームワークを網羅的に比較しています。

### CSS color-scheme-dependent colors with light-dark()

https://web.dev/articles/light-dark

CSS Module Level 5で追加された `light-dark()` を活用してより柔軟にダークモード対応をしようという記事です。

CSS Color Module Level 4の `Canvas` と `CanvasText` を組み合わせて簡易的に実現できていたダークモード対応ですが、`light-dark()` の登場によってテキスト色や背景色以外のCSSプロパティに対して任意の色を適用可能になりました。

### Power of Partial Prerendering with Bun

https://aralroca.com/blog/partial-prerendering

BunのPrerendering macroプラグインを使ってNext.jsのPartial Prerenderingのような挙動を実現できるという記事です。
