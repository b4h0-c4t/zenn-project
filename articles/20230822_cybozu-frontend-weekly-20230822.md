---
title: "RedwoodJS Build Competitionなど: Cybozu Frontend Weekly (2023-08-22号)"
emoji: "☀️"
type: "tech"
topics: ["CybozuFrontendWeekly", "frontend"]
published: true
publication_name: "cybozu_frontend"
---

# はじめに

こんにちは！サイボウズ株式会社フロントエンドエキスパートチームの [BaHo](https://twitter.com/b4h0_c4t) です。

サイボウズでは毎週火曜日に Frontend Weekly という「1 週間の間にあったフロントエンドニュースを共有する会」を社内で開催しています。

今回は、2023/08/22 の Frontend Weekly で取り上げた記事や話題を紹介します。

# 取り上げた記事・話題

## 認可のアーキテクチャに関する考察（Authorization Academy II を読んで）

https://zenn.dev/she_techblog/articles/6eff1f28d107be

認可設計に関する資料 Authorization Academy の考察記事です。
認可の関心分離方について整理されています。

## An update on Chrome Security updates – shipping security fixes to you faster

https://security.googleblog.com/2023/08/an-update-on-chrome-security-updates.html

Google Chrome のセキュリティ関連の更新が 4 週おきのアップデートとは別に毎週リリースされるようになります。

## RedwoodJS Conference Build Competition

https://build.redwoodjs.com/

RedwoodJS 主催のプロダクトコンペの告知です。
RedwoodJS を利用したプロダクトで応募して最大$5000 の賞金を獲得できます。
期間中は RedwoodJS のコアチームからの開発サポートも受けられるようですね。

## React 研修

https://speakerdeck.com/recruitengineers/react

株式会社リクルートのエンジニアコース React 研修資料です。
Web 開発の歴史や React で開発をする上での知識等をわかりやすく図解しています。

## node-core-test

https://github.com/nodejs/node-core-test

`node:test` の npm package 版です。

## decisions imports - epicweb-dev/epic-stack

https://github.com/epicweb-dev/epic-stack/blob/main/docs/decisions/031-imports.md

epic-stack が、絶対パスのインポートに tsconfig.json の path alias の設定と package.json の import field を併用するようになった決定です。

## Next.js に next/testmode という概念が出現し MSW x Playwright のテストがやりやすくなりそう

https://zenn.dev/uyas/articles/bc58a4bed15ed4

Next.js に test mode という機能が増えたことで、Server Components でも API をモックしてテストをかけるようになったという記事です。

## Vercel と提携し、ちょっと社はより多くの日本企業に向けてフロントエンドクラウドを提供します

https://prtimes.jp/main/html/rd/p/000000009.000045314.html

ちょっと株式会社が日本初の Vercel パートナーになったようです。

## Resume and pause animations in CSS

https://www.amitmerchant.com/run-and-pause-animations-in-css/

`animation-play-state` を使って CSS アニメーションを簡単に中断・再開する方法です。

## src: add built-in .env file support - nodejs/node

https://github.com/nodejs/node/pull/48890

Node.js が `.env` ファイルをビルトインサポートするようになります。

## How we reduced the size of our JavaScript bundles by 33%

https://dropbox.tech/frontend/how-we-reduced-the-size-of-our-javascript-bundles-by-33-percent

Dropbox が JS のバンドルサイズを 33% 削減した話です。
コード分割やバンドルの見直し、ツリーシェイキングの適用といったモダンな手法の適用によって既存プロダクトの JS サイズの軽量化に成功したようですね。
