---
title: "など: Cybozu Frontend Weekly (2023-07-04号)"
emoji: "🌴"
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

## Boshen/oxc Linter Roadmap

https://github.com/Boshen/oxc/issues/481

oxc の linter 実装についてのロードマップです。
bike-shedding になりがちな style や convention 以外のルールにフォーカスして、この２ヶ月で実装していくそうです。
プラグインは GraphQL のような DSL を提供してサポート予定のようです。

## styled-components/styled-components v6.0.0

https://github.com/styled-components/styled-components/releases/tag/v6.0.0

styled-components の v6 メジャーバージョンアップデートが来ました。
型を配布するようになった他、いくつかの内部実装の変更が多いようです。

社内ではマイグレーションガイドに従ってアップデートした結果エラーが発生したという情報が多く寄せられていたので、アップデートの際は腰を据えて実施しましょう。

## CJS/ESM 周りが今アツい！

https://deno.com/blog/commonjs-is-hurting-javascript

https://bun.sh/blog/commonjs-is-not-going-away

Deno と Bun が CJS についての記事を投稿していて話題になっています。
Deno は CJS の辛さについて、Bun は CJS の良さについてそれぞれ記述していて対比のようになっているのが特徴的ですね。

それぞれのランタイムで利用するコンテキストが異なるため一概には結論付けられませんが、今後の選択の参考になると良いですね。

## WebAssembly - web.dev

https://web.dev/webassembly/

web.dev に WebAssembly 関連のページができました。

## Breaking Up with SVG-in-JS in 2023

https://kurtextrem.de/posts/svg-in-js

SVG を JSX に埋め込むことによるバンドルサイズへの影響の話です。
JSX へ SVG を埋め込むと JS サイズが増大するため、`<img>` での受け込みや SVG スプライトなどでうまくやろうという内容が詳細に解説されています。

## The Cost Of JavaScript in 2023

https://speakerdeck.com/addyosmani/the-cost-of-javascript-in-2023

JS の実行を高速化するために必要なコード分割やハイドレーションなどの幅広いテクニックを俯瞰して見ることができる概論的な資料です。
パフォーマンス改善に興味がある人はぜひ閲覧してみましょう。

## Announcing Svelte 4

https://svelte.dev/blog/svelte-4

Svelte 4 がリリースされました。
Svelte をインストールした際のデータ量削減や IDE 機能の改善など、DX に関するアップデートが実施されています。

以前から進んでいた Svelte 内部コードの JavaScript 移行も無事に完了したようですね。

## AWS Lambda レスポンスストリーミングの紹介

https://aws.amazon.com/jp/blogs/news/introducing-aws-lambda-response-streaming/

https://aws.amazon.com/jp/blogs/news/implementing-ssr-streaming-on-nextjs-with-aws-lambda-response-streaming/

AWS Lambda で Streaming が利用できるようになりました。

Next.js の App Router でも利用できるようなので、デプロイ先の検討候補が増えそうですね。

## Announcing TypeScript 5.2 Beta

https://devblogs.microsoft.com/typescript/announcing-typescript-5-2-beta/

TS 5.2 beta がアナウンスされました。
今回のバージョンでは、一時期話題になっていた `using` 修飾子の対応が含まれています。

## ES2023 was approved by Ecma International

https://www.ecma-international.org/news/ecma-international-approves-new-standards-at-the-125th-general-assembly-27-june-2023/

https://twitter.com/robpalmer2/status/1674416934211952643

Ecma International 125 で採択された ES2023 の新要素です。

- Array findFromLast()
- Change Array by Copy
- Hashbang Grammar
- Symbols as WeakMap keys
