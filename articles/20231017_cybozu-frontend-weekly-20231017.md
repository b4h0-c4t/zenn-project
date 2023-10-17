---
title: "Changes to the web.dev infrastructure など: Cybozu Frontend Weekly (2023-10-17号)"
emoji: "🍁"
type: "tech"
topics: ["CybozuFrontendWeekly", "frontend"]
published: false
publication_name: "cybozu_frontend"
---

## はじめに

こんにちは！サイボウズ株式会社フロントエンドエキスパートチームの [BaHo](https://twitter.com/b4h0_c4t) です。

サイボウズでは毎週火曜日に Frontend Weekly という「1 週間の間にあったフロントエンドニュースを共有する会」を社内で開催しています。

今回は、2023/10/17 の Frontend Weekly で取り上げた記事や話題を紹介します。

## 取り上げた記事・話題

### CSS Findings From Photoshop Web Version

https://ishadeed.com/article/photoshop-web-css/

web 版の Photoshop で使われてる CSS の紹介記事です。

さまざまな場面で flexbox を活用しており、記事内には flexbox を活用したコンポーネントの事例が紹介されています。
また、多くの場所で Adobe が提供している web components を活用して View を作成しているようです。

### Changes to the web.dev infrastructure

https://web.dev/blog/webdev-migration?hl=en

web.dev がこれまで GitHub で ホスティングしていた CMS をやめ、Google が持つ共有インフラへ移行したことを告知しています。
サイトを運用していくにつれ、サイト作成当初に考えていたコンセプトから独自インフラを維持する必要性が薄れてきたためインフラを変更する決断に踏み切ったようです。
移行した結果、Google が持つローカライゼーションインフラをフックできるようになるため、今後は英語中心の開発者以外にもサービスを提供できるようになるそうです。

### Fresh 1.5: Partials, client side navigation and more

https://deno.com/blog/fresh-1.5

Fresh 1.5 のリリース記事です。

新しく `Partials` という SSR されたページにに対して、特定のコンポーネントのみを再描画させられるラップコンポーネントが追加されました。
また、`Link`に HTML 属性が追加され、現在のページやセクションを表現できるようになりました。

### Flat config rollout plans

https://eslint.org/blog/2023/10/flat-config-rollout-plans/

今年度末頃にリリース予定の ESLint v9 から flat config がデフォルトになり、`eslintrc` が非推奨になります。
また、v10 のリリースとともに `eslintrc` 対応が終了するとのことなので、既存プロジェクトでのライブラリアップデートの際は注意しましょう。

### Write your own Zod

https://zackoverflow.dev/writing/write-your-own-zod/

Zod ライクな Schema Validator を作成するための記事です。
実際のコードを交えてスキーマオブジェクトの扱いやバリデーションの実装について詳しく書かれています。

### Astro 3.3: Picture component

https://astro.build/blog/astro-330/

Astro 3.3 のリリース記事です。

複数の `<source>` 情報を持つ `<picture>` 要素を生成するための `<Picture>` コンポーネントが実験的に追加されています。
これにより、クライアントが描画する上で最適な `<source>` を複数の選択肢から決定できるようになりました。

### Just use vite! | remix-run/remix

https://github.com/remix-run/remix/discussions/7632

Vite のプラグインとして Remix が動作するようになりました。
Remix はコンパイラの分野に強い関心があるわけではないようで、現在主流である Vite のビルドパイプラインに実行環境を組み込むことでフレームワークとしての開発に専念したいという意図があるようです。
