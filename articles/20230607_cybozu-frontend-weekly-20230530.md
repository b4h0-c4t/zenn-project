---
title: "TypeScript 5.1 RCなど: Cybozu Frontend Weekly (2023-05-30号)"
emoji: "🌸"
type: "tech"
topics: ["CybozuFrontendWeekly", "frontend"]
published: true
publication_name: "cybozu_frontend"
---

# はじめに

こんにちは！サイボウズ株式会社フロントエンドエキスパートチームの [BaHo](https://twitter.com/b4h0_c4t) です。

サイボウズでは毎週火曜日に Frontend Weekly という「1 週間の間にあったフロントエンドニュースを共有する会」を社内で開催しています。

今回は、2023/05/30 の Frontend Weekly で取り上げた記事や話題を紹介します。

# 取り上げた記事・話題

## Introducing Deopt Explorer

https://devblogs.microsoft.com/typescript/introducing-deopt-explorer/

V8 のトレースログを VSCode で確認できるツール Deopt Explorer を紹介しながら、TS 5.0 でのパフォーマンス改善での作業を解説している記事です。
Deopt Explorer は主にインラインキャッシュ周りの改善が見込めるツールで、コード上にあるメガモーフィックなオブジェクトを特定してくれるといった機能があるようですね。

## An Update on the Lock Icon

https://blog.chromium.org/2023/05/an-update-on-lock-icon.html

Chrome で HTTPS 通信を示す鍵アイコンが将来的に変更されるようです。
アドレスバー左に表示されているお馴染みの鍵アイコンですが、本来 HTTPS 通信であるという意味しかないにも関わらず、多くのユーザーがそのサイトに対する信頼性の証であると誤認されてしまうといった問題があったようです。
Chrome 117 からは HTTPS 通信に関わる情報は調整アイコンに吸収され、鍵アイコンは表示されなくなるとのことです。

## The Bun Bundler

https://bun.sh/blog/bun-bundler

Bun Bundler のベータ版がリリースされました。
バンドルの実行速度が速く、Bun の公式ツールなだけあって設定の手間も少ないようです。
また、これを用いてビルドターゲットをブラウザにすることもでき、Web アプリとしての利用も容易になるようです。

## Announcing connect() — a new API for creating TCP sockets from Cloudflare Workers

https://blog.cloudflare.com/workers-tcp-socket-api-connect-databases/

Cloudflare Worker で TCP socket を使って通信できるようになりました。
Web socket 用の API `connect()` を用いて簡単に通信を実現できるようです。

## Announcing database integrations: a few clicks to connect to Neon, PlanetScale and Supabase on Workers

https://blog.cloudflare.com/announcing-database-integrations/

上記に加えて、Neon 等への接続を容易にする DB インテグレーションもアナウンスされています。

## Core: Drop support for IE (all versions)

https://github.com/jquery/jquery/pull/5077

jQuery v5 で IE のサポートが切られるようです。
これにより、直近で jQuery の容量が 624bypes 削減されるようで、今後のリファクタリングによってより多くを改善できるといったコメントもありました。

## Announcing TypeScript 5.1 RC

https://devblogs.microsoft.com/typescript/announcing-typescript-5-1-rc/

TypeScript 5.1 のアナウンスです。

- 返り値が undefined と定義された関数において、明示的な `return` を必要としなくなりました
- 明示的なアノテーションによって get と set のアクセさに関係のない型を指摘できるようになりました
- JSX の要素をカスタマイズできるようになりました
- JSX を使用する時、属性に名前空間を利用できるようになりました
- etc

## Announcing Vue 3.3

https://blog.vuejs.org/posts/vue-3-3

Vue 3.3 がリリースされました。
`<script setup>` におけるジェネリック型のパラメータサポートや `defineProps` および `defineEmits` の型パラメータが外部インポートに対応するといった更新がされています。

## Bun v0.6.0

https://bun.sh/blog/bun-v0.6.0

Bun v0.6.0 のリリースノートです。
前述した Bundler の追加や、Standalone executable が追加されました。

## Introducing Baseline: a unified view of stable web features

https://developer.mozilla.org/en-US/blog/baseline-unified-view-stable-web-features/

ブラウザ互換性の指標として Baseline という概念が発表されました。
Baseline では主要ブラウザ全てで実装済みであるかが観点となっており、US 版の MDN では Baseline 化されている機能についてのページでは先頭にチェックマークが付くなどの対応がされています。

## lizod: 1kb 未満の zod の精神的後継

https://zenn.dev/mizchi/articles/lizod-is-lightweight-zod

mizchi さん作の軽量なスキーマ検証ライブラリについての紹介記事です。
既存の同種ライブラリである zod からユーティリティ等を削除することで Cloudflare Workers でのビルドサイズ問題の解消を図っているようです。

## What's new in CSS and UI: I/O 2023 Edition

https://developer.chrome.com/blog/whats-new-css-ui-2023/

令和版最新 CSS のまとめです。
以前 Weekly まとめでも紹介された機能が多く盛り込まれているので、興味のある方は一覧してみましょう。

## Deploying AVIF for more responsive websites

https://web.dev/avif-updates-2023/

画像やアニメーションのフォーマット AVIF を採用しましょうという記事です。
AVIF は既存の画像フォーマットと比較してファイルサイズを削減でき、エンコードもマルチスレッドを利用できたりと非常にメリットが大きいフォーマットです。
Edge を除いた主要ブラウザの対応も済んでいるため、利用し始めるにはちょうど良い時期かもしれません。
