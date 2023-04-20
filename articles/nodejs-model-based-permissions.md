---
title: "Node.js v20.0.0 の新機能 Process-based Permissions"
emoji: "🔑"
type: "tech"
topics: ["frontend", "nodejs"]
published: false
publication_name: "cybozu_frontend"
---

## Permissions とは

Node.js には、コードを読み込む際にそのコードが得られる権限をポリシーとして宣言できる機能があります。

https://nodejs.org/dist/v20.0.0/docs/api/permissions.html#process-based-permissions

この機能は主に、実行対象となる Node.js アプリケーションが指定されたリソース以外の読み込みを実施しないことを保証するためにあります。

以前までは Module-based Permissions と呼ばれる、モジュール単位で権限を指定可能な機能が実験的な機能として導入されていました。

## Module-based Permissions

本題に入る前に、Module-based Permissions についても少し触れておきます。
Module-based Permissions は名前の通り、実行ファイルで権限を管理するための機能です。

簡単なコード例を交えて紹介します。

`main.js` : `reader.js` から受け取った Buffer を json としてパースし、最初の `key` と `value` を出力するプログラム
`reader.js` : 渡されたファイル名を元にファイルの読み込みを実行して Buffer を返却するプログラム
`resource.json` : 読み込まれるファイル

```main.js:js
const reader = require("./reader.js");

const json = JSON.parse(reader("resource.json"));
console.log(Object.keys(json)[0], json[Object.keys(json)]);
```

```reader.js:js
const fs = require("fs");

const reader = (fileName) => fs.readFileSync(fileName);

module.exports = reader;
```

```resource.json:json
{
  "hello": "permissions!"
}

```

目的のコードが完成したら、次に実行ファイルすべてに対してポリシーを設定していきます。

```policy.json:json
{
  "resources": {
    "./main.js": {
      "integrity": "sha256-AbAVZBk8gatwFiCOT4I2SvKW4foA/S+knDnFYYjOS18=",
      "dependencies": {
        "./reader.js": "./reader.js"
      }
    },
    "./reader.js": {
      "integrity": "sha256-vGpKmyVxtHMAZzW6lATnMIqfb4uNuJ1k5AMCDxnY2fY=",
      "dependencies": {
        "fs": true
      }
    }
  }
}
```

すべての実行ファイルに共通して、`integrarity` の設定は必須です。
`integrarity` は実行ファイルのハッシュ値が格納されており、これを元に第三者がコードの改変を行なっていないかを評価します。

ドキュメントに記載されている通り、一例として後述のようなコマンドで生成することができます。

```sh
node -e 'process.stdout.write("sha256-");process.stdin.pipe(crypto.createHash("sha256").setEncoding("base64")).pipe(process.stdout)' < {ファイル名}
```

また、今回は `main.js` は `reader.js` を、`reader.js` は `fs` を `require` しているためそれぞれ `dependencies` へ記載します。
`dependencies` はその実行ファイルがアクセス可能な実行ファイルを定義することができ、想定されていない実行ファイルへのアクセスを防止する効果が期待できます。

これらのファイルが揃ったら、早速 `main.js` を実行してみましょう。

```
hello permissions!
(node:14845) ExperimentalWarning: Policies are experimental.
(Use `node --trace-warnings ...` to show where the warning was created)
```

上記のような文が表示されたら成功です、おめでとうございます。

:::実行するディレクトリと同階層に `package.json` が同階層にある場合、そちらの整合性も確認して実行が失敗する場合があります。:::

これまで作った実行プログラムに対して、`require` 先を増やしたりコードを改変した場合、`Error [ERR_MANIFEST_ASSERT_INTEGRITY]: (以下略)` のようなエラーが表示されて実行できないことがわかると思います。
このように意図しない改変がされた実行プログラムに対してそれを検知できるのが Module-based Permission の機能になります。

## Process-based Permissions
