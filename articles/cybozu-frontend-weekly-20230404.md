---
title: "Rome v12リリースなど: Cybozu Frontend Weekly (2023-04-04号)"
emoji: "🌸"
type: "tech"
topics: ["CybozuFrontendWeekly", "frontend"]
published: false
publication_name: "cybozu_frontend"
---

# はじめに

こんにちは！サイボウズ株式会社フロントエンドエキスパートチームの [BaHo](https://twitter.com/b4h0_c4t) です。

サイボウズでは毎週火曜日に Frontend Weekly という「1 週間の間にあったフロントエンドニュースを共有する会」を社内で開催しています。

今回は、2023/04/04 の Frontend Weekly で取り上げた記事や話題を紹介します。

# 取り上げた記事・話題

## Announcing Rome v12

https://rome.tools/blog/2023/03/28/rome12/

Rome v12 がリリースされました 🎉

- JSON 形式のパースに対応
- TypeScript4.7~5.0 をサポート
  - optional variance annotation
  - `extends` constrain on `infer`
  - const type parameters
  - `export type *`
- CLI 経由でのインポート順のソート
- etc

## storybookjs/storybook v7.0.0 Prerelease

https://github.com/storybookjs/storybook/releases/tag/v7.0.0

Stroybook の v7 がプレリリースされました 🎉

- [Vite の第一級サポート](https://storybook.js.org/blog/first-class-vite-support-in-storybook/)
- [NextJS のゼロコンフィグサポート](https://storybook.js.org/blog/integrate-nextjs-and-storybook-automatically/)
- [SvelteKit のゼロコンフィグサポート](https://storybook.js.org/blog/storybook-for-sveltekit/)
- [各フレームワークの API 対応](https://storybook.js.org/blog/framework-api/)
- [Component Story Format v3](https://storybook.js.org/blog/storybook-csf3-is-here/)
- [Docs を MDX2 でオーバーホールする機能の追加](https://storybook.js.org/blog/storybook-7-docs/)
- etc

## layer - vanilla extract

https://vanilla-extract.style/documentation/api/layer/

vanilla extract が layer に対応しました。
ポリフィルが使用されているわけではないので、現在 layer 機能が有効になっているクライアントでのみ動作するようです。

## Styling Addon: configure styles and themes in Storybook

https://storybook.js.org/blog/styling-addon-configure-styles-and-themes-in-storybook/

UI コンポーネントにテーマを提供するためのアドオンの話です。
このアドオンにより、フレームワークに依らずスタイルを統一してかけるようになります。

## ZOZOTOWN の Web ホーム画面を Next.js でリプレイスして得た知見

https://techblog.zozo.com/entry/replacing-zozo-with-nextjs-knowledge

ZOZOTOWN のフロントエンドをリプレイスするプロジェクトの話です。
開発効率の向上・運用コストの削減・人材獲得を目的として、API のマイクロサービス化とフロントエンドの新フレームワーク導入を実施したようです。
カナリアリリースやストラングラーパターンといった手法、アーキテクチャの導入により無停止での段階的なリプレイスに成功しています。

## Cloudflare Workers のためのフルスタックツールキット Superflare を試してみた

https://zenn.dev/azukiazusa/articles/superflare-for-cloudflare-workers

D1 Database や R2 Storage むけのユーティリティ機能を提供しているフルスタックツールキット Superflare を試した話です。
記事では簡単なアルバムアプリの実装からデプロイまでを通して Superflare の使い方に触れています。

## Future Proofing Your Remix App

https://remix.run/blog/future-flags

Remix の新機能に対するフラグ管理(Future Flags)についての話。

Remix では V2 リリースに向けて、`future.unstable_` と `future.v2_` というフラグを用意して新機能の管理を行なっているようです。
V2 の新 API に対応する機能は `future.v2_` フラグで管理され、unstable な機能は `future.unstable_` フラグで管理されており、それぞれ `remix.config.js` の `future flags` 項目から任意で利用可能となります。

## Rich Harris Talks SvelteKit and What’s Next for Svelte

https://thenewstack.io/rich-harris-talks-sveltekit-and-whats-next-for-svelte/

Svelte に大きめの修正をする準備が進行中であるという話です。
Svelte 周りの内部コードが TypeScript から JavaScript へ置き換えられるほか、大きなアイデアが取り入れられる予定だという。

## One In Two New Npm Packages Is SEO Spam Right Now

https://blog.sandworm.dev/one-in-two-new-npm-packages-is-seo-spam-right-now

2023 年 3 月に新しく公開された npm パッケージのうち半数以上が SEO スパムとして利用されているという話です。
ロシアの Telegram チャンネルや無料の電子書籍、V-Bucks といった典型的なスパムとして悪用されているようです。

## New to the web platform in March

https://web.dev/web-platform-03-2023/

各主要 Web ブラウザが 3 月にリリースした追加機能がまとめられた記事です。

# あとがき

サイボウズでは毎月、最終火曜日の 17 時から Frontend Monthly というイベントを YouTube Live で開催しています。その月のフロントエンド注目ニュースや、ゲストを呼んでの対談など、フロントエンドに関する発信をしていますので是非どうぞ！

https://cybozu.github.io/frontend-monthly/

また、サイボウズでは一緒にサイボウズのフロントエンドをより良くする仲間を募集しています。興味ある方はこちら ↓ から！

【フロントエンドエキスパート】
サイボウズのフロントエンドを最高にするためのチームです。

https://cybozu.github.io/frontend-expert/

https://cybozu.co.jp/recruit/entry/career/front-end-expert.html

【フロントエンドエンジニア（kintone アーキテクチャ刷新 PJ）】
クラウドサービス「kintone」のフロントエンドを新しくしています。

https://blog.cybozu.io/archive/category/%E3%83%95%E3%83%AD%E3%83%AA%E3%82%A2

https://cybozu.co.jp/recruit/entry/career/front-end-engineer-kintone.html
