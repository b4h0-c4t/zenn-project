---
title: "Node.js v20.0.0 の新機能 Process-based Permissions"
emoji: "🔑"
type: "tech"
topics: ["frontend", "nodejs"]
published: false
publication_name: "cybozu_frontend"
---

# Permissions とは

Node.js には、コードを読み込む際にそのコードが得られる権限をポリシーとして宣言できる機能があります。

https://nodejs.org/dist/v20.0.0/docs/api/permissions.html#process-based-permissions

この機能は主に、実行対象となる Node.js アプリケーションが指定されたリソース以外の読み込みを実施しないことを保証するためにあります。

以前までは Module-based Permissions と呼ばれる、モジュール単位で権限を指定可能な機能が実験的な機能として導入されていました。

# Module-based Permissions

本題に入る前に、Module-based Permissions についても少し触れておきます。
Module-based Permissions は名前の通り、実行ファイルで権限を管理するための機能です。

簡単なコード例を交えて紹介します。

`main.js` : `reader.js` から受け取った Buffer を json としてパースし、最初の `key` と `value` を出力するプログラム
`reader.js` : 渡されたファイル名を元にファイルの読み込みを実行して Buffer を返却するプログラム
`resource.json` : 読み込まれるファイル

```js:main.js
const reader = require("./reader.js");

const json = JSON.parse(reader("resource.json"));
console.log(Object.keys(json)[0], json[Object.keys(json)]);
```

```js:reader.js
const fs = require("fs");
```

const reader = (fileName) => fs.readFileSync(fileName);

module.exports = reader;

````

```json:resource.json
{
  "hello": "permissions!"
}

````

目的のコードが完成したら、次に実行ファイルすべてに対してポリシーを設定していきます。

```json:policy.json
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

```
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

# Process-based Permissions

Process-based Permissions では、Permission Model を用いて実行プログラムのアクセス制御を行います。
この機能が Module-based Permissions と異なるのは、モジュール単位ではなく実行プロセスごとに権限の付与ができる点です。

この機能を有効化するには、実行時に `--experimental-permission` フラグを使用します。
試しに Module-based Permissions の解説で取り扱った `main.js` に対してこの機能を有効化してみましょう。

```
$ node --experimental-permission main.js
node:internal/modules/cjs/loader:179
  const result = internalModuleStat(filename);
                 ^

Error: Access to this API has been restricted
    at stat (node:internal/modules/cjs/loader:179:18)
    at Module._findPath (node:internal/modules/cjs/loader:651:16)
    at resolveMainPath (node:internal/modules/run_main:15:25)
    at Function.executeUserEntryPoint [as runMain] (node:internal/modules/run_main:76:24)
    at node:internal/main/run_main_module:23:47 {
  code: 'ERR_ACCESS_DENIED',
  permission: 'FileSystemRead',
  resource: '/main.js'
}
```

何も指定せずに実行すると、上の通り FileSystemRead の権限がないとしてエラーになります。
このように、`--experimental-permission` フラグを有効化すると、Permission Model に定義される全ての権限に対して制限がかけられます。

今回の実行プログラムでは FileSystem の Read を利用しているため、実行時にカレントディレクトリに対してファイル読み込みの権限を付与してみます。

```
$ node --experimental-permission --allow-fs-read=$(pwd)/resource.json main.js
hello permissions!
(node:22823) ExperimentalWarning: Permission is an experimental feature
(Use `node --trace-warnings ...` to show where the warning was created)
```

問題なく実行できましたね。

Permission Model では、FileSystem 以外にも、全てのネイティブモジュールが定義されており、利用する機能にアクセスする場合は個別に有効かを実施する必要があります。
また、実行プログラム側の Runtime API として `process.permission.has()` 関数が提供され、boolean で特定のモジュールに対するアクセス権限があるかどうかを確認することができます。

```js
process.permission.has("fs.write"); // true or false
```

これによって、アクセス権限の有無による実行エラーの対処ができます。

# 最後に

本稿では、Node.js v20.0.0 の実験的機能である Process-based Permissions について解説しました。
日頃、Node.js の実行コードのアクセス権限についてあまり意識をしていない方も多いと思いますが、これらを利用してより厳格なセキュリティを構築していきましょう！
