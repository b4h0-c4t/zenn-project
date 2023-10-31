---
title: "Next.js 14 リリースなど: Cybozu Frontend Weekly (2023-10-31号)"
emoji: "👻"
type: "tech"
topics: ["CybozuFrontendWeekly", "frontend"]
published: false
publication_name: "cybozu_frontend"
---

## はじめに

こんにちは！サイボウズ株式会社フロントエンドエキスパートチームの [BaHo](https://twitter.com/b4h0_c4t) です。

サイボウズでは毎週火曜日に Frontend Weekly という「1 週間の間にあったフロントエンドニュースを共有する会」を社内で開催しています。

今回は、2023/11/31 の Frontend Weekly で取り上げた記事や話題を紹介します。

## 取り上げた記事・話題

### Rspress, the Rspack-based static site generator

https://github.com/orgs/web-infra-dev/discussions/5

Rspack ベースの Static Site Generator である Rspress の v1 がリリースされました。
i18n 対応やコンポーネントのプレビューなど、様々な機能が盛り込まれているようです。

### Faster TypeScript builds with --isolatedDeclarations

https://portal.gitnation.org/contents/faster-typescript-builds-with-isolateddeclarations

TypeScript に今後実装予定の `--isolatedDeclarations` オプションについての動画です。

型定義のファイル間依存が複雑化することによって型定義の解析処理が並列化できず、出力に時間がかかってしまう課題を解決するためのオプションです。
このオプションによって他ファイルからインポートされた関数等の型がインポート先で推論されるようになり、型定義ファイル出力におけるファイル間の依存が軽減されるようです。

### Why I Won't Use Next.js

https://www.epicweb.dev/why-i-wont-use-nextjs

Kent C. Dodds 氏がなぜ Next.js ではなく Remix を使うのかを綴っている記事です。

フレームワーク固有のボイラープレートを学ばなければならないことや React と Next.js の境界を曖昧にしようとしているのではないかという疑念があり、Remix を利用しているそうです。

### Vue Language Server から生まれた Volar.js と、それが秘める可能性

https://speakerdeck.com/mizdra/vue-language-server-karasheng-mareta-volar-dot-js-to-soregami-meruke-neng-xing

組み込み言語の language server を構築するための汎用ツール Volar.js の紹介スライドです。
一つのファイルで複数の言語を解釈する必要があるなど、組み込み言語特有の language server 実装の難しさを解決する 汎用 LSP Volar.js とそのアプローチについて解説しています。

### Start building with Next.js

https://nextjs.org/learn

Next.js 学習リソースです。
App Router を活用した Next.js 開発を学びたい人におすすめです。

### Next.js 14

https://nextjs.org/blog/next-14

Next.js 14 のリリースノートです。

Turbopack の導入や Server Actions の Stable 化といった更新を含んでいます。
また、Next Conf 開催についても触れられています。
