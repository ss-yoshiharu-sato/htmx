[![</> htmx](https://raw.githubusercontent.com/bigskysoftware/htmx/master/www/static/img/htmx_logo.1.png "high power tools for HTML")](https://htmx.org)

*HTML用ハイパワーツール*

[![Discord](https://img.shields.io/discord/725789699527933952)](https://htmx.org/discord)
[![Netlify](https://img.shields.io/netlify/dba3fc85-d9c9-476a-a35a-e52a632cef78)](https://app.netlify.com/sites/htmx/deploys)
[![Bundlephobia](https://badgen.net/bundlephobia/dependency-count/htmx.org)](https://bundlephobia.com/result?p=htmx.org)
[![Bundlephobia](https://badgen.net/bundlephobia/minzip/htmx.org)](https://bundlephobia.com/result?p=htmx.org)

## 導入

htmxでは、[AJAX](https://htmx.org/docs#ajax)、[CSS Transitions](https://htmx.org/docs#css_transitions)、[WebSocket](https://htmx.org/docs#websockets)、[Server Sent Events](https://htmx.org/docs#sse)にアクセスできます。
[属性](https://htmx.org/reference#attributes)を使用して、HTMLで直接アクセスすることができます。
[モダンなユーザーインターフェース](https://htmx.org/examples)を[シンプルさ](https://en.wikipedia.org/wiki/HATEOAS)と
ハイパーテキストの[パワー](https://www.ics.uci.edu/~field/pubs/dissertation/rest_arch_style.htm)を使って、[最新のユーザーインターフェイス](https://www.ics.uci.edu/)を構築することができます。

htmxは小さく([~14k min.gz'd](https://unpkg.com/htmx.org/dist/))、
[依存性がなく](https://github.com/bigskysoftware/htmx/blob/master/package.json) &
[拡張可能](https://htmx.org/extensions)です。

## 動機

* なぜ`<a>`と`<form>`だけがHTTPリクエストできるのですか？
* なぜ`click`と`submit`イベントだけがトリガーになるのですか？
* なぜ`GET`と`POST`しか使えないのか？
* なぜ`スクリーン全体を書き換え`しなければならないのですか？

これらの任意の制約を取り除くことで、htmxはHTMLを[ハイパーテキスト](https://en.wikipedia.org/wiki/Hypertext)として完成させます。

## クイックスタート

```html
  <script src="https://unpkg.com/htmx.org@2.0.0"></script>
  <!-- have a button POST a click via AJAX -->
  <button hx-post="/clicked" hx-swap="outerHTML">
    Click Me
  </button>
```

[`hx-post`](https://htmx.org/attributes/hx-post)と[`hx-swap`](https://htmx.org/attributes/hx-swap) 属性は`htmx`の指示です：

> "ユーザーがこのボタンをクリックしたら、`/clicked`にAJAXリクエストを発行し、ボタン全体をレスポンスに置き換える"

htmxは[intercooler.js](http://intercoolerjs.org)の後継です。

### ノードパッケージとしてインストールする

npmを使用してインストールする

```
npm install htmx.org --save
```

Note `htmx`という古い壊れたパッケージがあることに注意してほしい。これは `htmx.org` である。

## ウェブサイト＆ドキュメント

* <https://htmx.org>
* <https://htmx.org/docs>

## 貢献

貢献したいですか？[寄稿ガイドライン](CONTRIBUTING.md)をご覧ください。

時間がない？それなら[スポンサーになる](https://github.com/sponsors/bigskysoftware#sponsors)のはどうでしょう？

### ハッキングガイド

ローカルでhtmxを開発するには、開発依存ファイルをインストールする必要があります。

以下を実行してください:

```
npm install
```

次に、ルートでウェブサーバーを実行します。

以下を使うのが最も簡単だ。:

```
npx serve
```

テスト・スイートを実行するには、次のページに移動する：

<http://0.0.0.0:3000/test/>

この時点で `/src/htmx.js` を修正して機能を追加し、`/test` 以下の適切な領域にテストを追加することができる。

* `/test/index.html` - 他のすべてのテストが含まれるルートテストページ
* `/test/attributes` - 属性別テスト
* `/test/core` - コア機能テスト
* `/test/core/regressions.js` - 回帰テスト
* `/test/ext` - エクステンションテスト
* `/test/manual` - 自動化できない手動テスト

htmxは[mocha](https://mochajs.org/)テストフレームワーク、[chai](https://www.chaijs.com/)アサーションフレームワーク、[sinon](https://sinonjs.org/releases/v9/fake-xhr-and-server/)を使ってAJAXリクエストをモックアウトしています。これらはすべてOKです。

`npm run ws-tests` を使えば、WebSockets と Server-Side Events 拡張機能のライブテストとデモを実行することもできる。

## 俳句

面倒も<br/>
原点回帰も<br/>
解決だ
