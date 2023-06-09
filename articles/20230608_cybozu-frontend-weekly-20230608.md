---
title: "View Transition APIなど: Cybozu Frontend Weekly (2023-06-06号)"
emoji: "🌸"
type: "tech"
topics: ["CybozuFrontendWeekly", "frontend"]
published: true
publication_name: "cybozu_frontend"
---

# はじめに

こんにちは！サイボウズ株式会社フロントエンドエキスパートチームの [BaHo](https://twitter.com/b4h0_c4t) です。

サイボウズでは毎週火曜日に Frontend Weekly という「1 週間の間にあったフロントエンドニュースを共有する会」を社内で開催しています。

今回は、2023/06/06 の Frontend Weekly で取り上げた記事や話題を紹介します。

# 取り上げた記事・話題

## View Transitions

https://twitter.com/argyleink/status/1661800757304381443?s=20

View Transitions API を使って MPA で画面遷移時にアニメーションを追加するサンプルページを紹介しているツイートです。
Chrome で `chrome://flags/#view-transition-on-navigation` のフラグを有効化することで、手元の環境でも View Transition API の動作を確認することができます。
また、この API は 近々 Working Draft から Candidate Recommendation になるかもしれません。

## Introducing the popover API

https://developer.chrome.com/blog/introducing-popover-api/

Chrome 114 に実装された popover API の紹介記事です。
今まで座標計算や描画順といった問題で苦しめられてきた Popover の実装ですが、HTML と CSS の簡素な設定で実現できるようになりました。

## Firefox Developer Experience

https://fxdx.dev/

新しく作られた Firefox の DX ブログサイトです。
現状はまだ記事が少なく、WebDriver や DevTools のリリースノートなどがほとんどですが、今後の更新に期待が持てますね。

## Intent to Ship: CSS Motion Path

https://groups.google.com/a/chromium.org/g/blink-dev/c/BemiGubA8AM/m/ENBOzVZUAgAJ

CSS Motion Path で `circle` や `react()`、`ray()` といった関数が利用可能になるようです。
Chrome の 116 辺りから利用可能になる予定とのことです。

## Deno 1.34: deno compile supports npm packages

https://deno.com/blog/v1.34

Deno 1.34 のリリースノートです。

- `deno compile` が npm packages をサポート
- `deno.json` および CLI flags で Glob をサポート
- IP アドレスを含む TLS 認証をサポート

といった更新が含まれています。

## Parcel v2.9.0

https://parceljs.org/blog/v2-9-0/

Percel v2.9.0 のリリースノートです。
Percel は所謂 Zero-config なバンドラーで、今回の更新では後述の機能が追加されています。

- ESM 形式のプラグインをサポート
- ローカル環境でのプラグイン読み込みをサポート
- minifier を Terser から SWC へ更新

## vanjs-org/van

https://github.com/vanjs-org/van

script での読み込みだけで利用できる超軽量でリアクティブな UI フレームワークです。
軽量なリアクティブ UI フレームワークとして Preact などが思い浮かぶかもしれませんが、vanjs は依存管理やバンドルを必要としないため、既存の軽量 UI フレームワークとは違った需要を満たしてくれそうです。

## microsoft/devicescript

https://github.com/microsoft/devicescript

小型 IoT デバイス向けの TypeScript コンパイラです。
マイコンプログラミングといえば低水準言語でのコーディングが一般的ですが、こちらを利用することで TypeScript コードを独自 VM のバイトコードへ変換し、マイコンへの書き込みを行ってくれるようです。
メモリ管理周りが若干気になりますが、面白そうな取り組みですね。

## Opera unveils Opera One, an entirely redesigned browser

https://press.opera.com/2023/04/25/opera-one-developer/

Opera が新しいデザインのブラウザ Opera One を発表しました。
Chromium ベースで実装されており、現在アーリーアクセスが実施中とのことです。

## Design a superior user experience with the new Side Panel API

https://developer.chrome.com/blog/extension-side-panel-launch/

Chrome 拡張からサイドパネルを利用可能になりました。
サイドパネルは、ページに関連のある情報を表示するための機能として備わっていました。
今回のアップデートによって、Chrome 拡張を通してこれをカスタマイズできるようになります。
この API を用いた Chrome 拡張が今後普及してくるのが楽しみですね。

## RedwoodJS’ Next Epoch: All In on React Server Components

https://tom.preston-werner.com/2023/05/30/redwoods-next-epoch-all-in-on-rsc.html

RedwoodJS が近い将来に React Server Components を利用した SSR 機能を実装すると発表しました。
RedwoodJS は JavaScript/TypeScript で構築された React ベースのフルスタックな Web アプリケーションフレームワークです。
フロントエンド部分は主に CSR を前提として構築されてきましたが、SEO や OG タグ、ページサイズといった理由から SSR を導入する方針に決めたようです。

## New CSS color spaces and functions in all major engines

https://web.dev/color-spaces-and-functions/

主要ブラウザ全てで利用可能になった色空間へのアクセスや色操作関数についての紹介記事です。
この記事では主に `color()` と `color-mix()` について取り上げられています。

## Intent to Ship: @scope

https://groups.google.com/a/chromium.org/g/blink-dev/c/OEfGbd74QnQ/m/KaX-2hhRAAAJ

CSS `@scope` が Chrome 117 に実装されるようです。
`@scope` は指定されたセレクタにマッチした要素をスコープの上限として設定し、その子孫要素でのみ適用されるスタイルをブロックに記述することができます。
また、任意で下限にあたる要素も指定することができ、指定した場合は上限要素の子孫でかつ加減要素の子孫ではない要素に対してスタイルが適用されます。

## Introducing Pulse: Real-Time Database Change Events Made Easy

https://www.prisma.io/blog/introducing-pulse-jtu4UPC8ujy4

Prisma Client から DB の更新情報を購読し、リアルタイムでの更新処理を可能にするための機能 Prisma Pulse が発表されました。
DB の状態確認のためにポーリングといった手段を用いずにシームレスな通信が可能になるようです。

## JavaScript Macros in Bun

https://bun.sh/blog/bun-macros

Bun が bundle-time で JavaScript を実行する Macros の機能をリリースしました。
例えば Git commit hash を埋め込んだり、事前に fetch を処理したりといった活用ができます。

## server component roadmap #19772 nuxt/nuxt

https://github.com/nuxt/nuxt/issues/19772

Nuxt が ServerComponent の対応を進めているようです。
すでにロードマップが進行しており、いくつかの実装は済んでいるようですね。
