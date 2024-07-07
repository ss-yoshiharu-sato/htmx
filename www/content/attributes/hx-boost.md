+++
title = "hx-boost"
+++

`hx-boost`属性は、通常のアンカーやフォームタグの代わりにAJAXを使用するように"ブースト"することができます。これには[nice fallback](https://en.wikipedia.org/wiki/Progressive_enhancement)があり、もしユーザーがjavascriptを有効にしていなくても、サイトは動作し続けます。

アンカータグの場合、アンカーをクリックすると `href` で指定された url に対して `GET` リクエストが発行され、その url がプッシュされてヒストリエントリが作成されます。  ターゲットは `<body>` タグであり、デフォルトでは `innerHTML` が使用される。`click`トリガーを除いて、これらはすべて適切な属性を使用して変更することができる。

フォームの場合、リクエストは `method` 属性のメソッドに基づいて `GET` または `POST` に変換され、`submit` がトリガーされる。この場合も、ターゲットはページの `body` となり、 `innerHTML` スワップが使用される。しかし、urlはプッシュされず、ヒストリエントリも作成されません。(urlをプッシュさせたい場合は、[hx-push-url](@/attributes/hx-push-url.md) 属性を使うことができます)。

以下はブーストリンクの例である：

```html
<div hx-boost="true">
  <a href="/page1">Go To Page 1</a>
  <a href="/page2">Go To Page 2</a>
</div>
```
これらのリンクは、それぞれのURLに対してajax `GET` リクエストを発行し、ボディの内部コンテンツをそれに置き換えます。

以下は、ブーストされたフォームの例である：

```html
<form hx-boost="true" action="/example" method="post">
    <input name="email" type="email" placeholder="Enter email...">
    <button>Submit</button>
</form>
```
このフォームは指定された URL に対して ajax `POST` を発行し、body の内部コンテンツをそれに置き換えます。

## メモ

* `hx-boost` は継承され、親要素に置くことができる。
* 同じドメインへのリンクで、ローカルアンカーでないリンクのみがブーストされる。
* すべてのリクエストはAJAX経由で行われるため、リダイレクトなどを行う際にはその点に留意すること。
* ブーストされたアンカーやフォームからのリクエストかどうかを調べるには、リクエストヘッダで[`HX-Boosted`](@/reference.md#request_headers)を探します。
* `hx-boost="false"`で子要素のブーストを選択的に無効にする。
* [`hx-preserve="true"`](@/attributes/hx-preserve.md)を使って、boostによる要素の置換とその子要素の置換を無効にする。
