---
title: "Firefox 120 から注目の新要素を紹介 - What's new in Browsers!"
emoji: "☃️"
type: "tech"
topics: ["Firefox", "browser", "frontend"]
published: true
publication_name: "cybozu_frontend"
---

What's new in Browsers!は、サイボウズのフロントエンドエンジニアがブラウザの最新情報から気になるトピックを紹介するシリーズです。

今回は Firefox 120 からサポートされた機能 UserActivation API と Early Hints Preconnect を紹介します。

## UserActivation API

UserActivation API は、そのページに対してユーザが現在アクティブであるかどうかと以前アクティブであったかどうかを取得できる実験的な機能です。

`navigator.userActivation` から該当機能へアクセスすることができ、`hasBeenActive` と `isActive` という二種類のプロパティを参照することが可能です。
ウィンドウにおけるユーザーのアクティブ状況は **粘着的な有効化** と **一時的な有効化** の二種類があり、それぞれの状態が `hasBeenActive` と `isActive` に紐づいています。

使用例としては、ページが初めて一時的に有効化された際にアニメーションの読み込んで自動再生を始めるといったように、一般的にユーザの操作外で発火するとバッドプラクティスとして扱われるようなイベントのハンドリングに活用することができます。

User Activation API は Firefox 120 でのフルサポートを以て、主要なブラウザすべてで利用可能になりました。

## Early Hints Preconnect

Early Hints Preconnect は、サーバがリクエストに対する最終的なレスポンスを返す前にリソースのリンクヘッダーを送信するためのステータスコードです。
Firefox でこの機能が有効化されたことにより、Cloudflare 等の Early Hints Preconnect を使用しているサービスでのページ読み込みがより高速化されます。

この仕組みによってページロードが高速化される仕組みとして、Web サーバはクライアントからリクエストを受け取りレスポンスを構築している間にページの読み込みに必要なその他のリソースのリンクを含むレスポンス(103 Early Hints)を一度クライアントへ返します。
そのレスポンスを受け取ったクライアントは、200 OK のレスポンスが帰ってくるまでの間にその他必要なリソースを事前に読み込みに行きます。
このように、今までは 200 OK が返却された後でしか読み込めなかったリソースを事前に把握し読み込めるようになったことで、最終的なロードタイム高速化につながっています。

![](/images/20231130_whats-new-in-browser-firefox-120/EarlyHints.png)

Early Hints Preconnect は Firefox 120 でのサポートを以て、主要なブラウザすべてで利用可能になりました。
一方で、preload については Firefox がフラグ月サポートになっており、Safari ではサポートされていないため注意が必要です。
