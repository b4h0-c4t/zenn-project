---
title: "Vercelのストレージ提供開始など: Cybozu Frontend Weekly (2023-05-08号)"
emoji: "🌸"
type: "tech"
topics: ["CybozuFrontendWeekly", "frontend"]
published: true
publication_name: "cybozu_frontend"
---

# はじめに

こんにちは！サイボウズ株式会社フロントエンドエキスパートチームの [BaHo](https://twitter.com/b4h0_c4t) です。

サイボウズでは毎週火曜日に Frontend Weekly という「1 週間の間にあったフロントエンドニュースを共有する会」を社内で開催しています。

今回は、2023/05/08 の Frontend Weekly で取り上げた記事や話題を紹介します。

# 取り上げた記事・話題

## Million.js

https://millionjs.org/

React コンポーネントを比較的簡単に高速化できる仮想 DOM ライブラリです。
軽量化したい React コンポーネントを指定することで、Million.js 側が静的解析を実施し、コンポーネントの再描画を最小限に抑えることで高速化を実現しているようですね。

詳しい仕組みについては [Virtual DOM: Back in Block](https://millionjs.org/blog/virtual-dom) で解説されています。

## yoavbls/pretty-ts-errors

https://github.com/yoavbls/pretty-ts-errors

TS エラーを読みやすくしてくれる VSCode 拡張です。
複雑で大きめな型情報を扱うときに感じていたストレスから解放されます。

## Introducing storage on Vercel

https://vercel.com/blog/vercel-storage

Vercel がストレージ系のバックエンドを提供し始めるようです。
Vercel KV、Vercel Postgres、Vercel Blob の 3 種類が提供されるようで、それぞれのインフラは他サービスをパートナーとして構成されていいます。

また、Vercel Postgres について、Edge Runtime で ORM と Connection Pool を利用できるようにしている手法について調査している記事も話題になりました。

https://zenn.dev/laiso/articles/542fdfac2acb6b

## Next.js 13.4

https://nextjs.org/blog/next-13-4

Next.js 13.4 のリリース情報です。
React Server Component 等が Stable として導入された他、alpha リリースとして Server Actions が追加されました。

## React Canaries: Enabling Incremental Feature Rollout Outside Meta

https://react.dev/blog/2023/05/03/react-canaries

React が今後 Canary リリースを実施していくようです。

## Qwik Reaches v1.0

https://www.builder.io/blog/qwik-v1

Qwik が v1 になりました 🎉
初のメジャーリリースということで、今後の動向に注目ですね。

## Deno 1.33: Deno 2 is coming

https://deno.com/blog/v1.33

Deno v1.33 のリリース情報です。
KV データベースがビルトインされるなどの更新が入っています。
また、Deno 2 が数ヶ月後にリリースされることについて、改めて当初のビジョンなどについても言及していますね。

## A Gentle Introduction to Islands

https://deno.com/blog/intro-to-islands

Web サイトのごく一部にのみインタラクティブな体験が必要な場合に活用できる Islands Architecture Deno ベースでの実装について解説した記事です。

## Node v20.1.0 Release

https://nodejs.org/en/blog/release/v20.1.0

Node.js v20.1.0 のリリース情報です。
fs option に recursive が追加されるなど、地味に嬉しい更新が含まれています。
