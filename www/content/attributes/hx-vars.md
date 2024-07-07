+++
title = "hx-vars"
+++

**注: `hx-vars` は非推奨となり、[`hx-vals`](@/attributes/hx-vals.md) の方がデフォルトでは安全です。**

`hx-vars`属性は、AJAXリクエストで送信されるパラメータに動的に追加することができます。  

この属性の値はカンマで区切られた `name`:`<expression>` 値のリストで、javascript [Object Literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Grammar_and_types#Object_literals) の内部構文と同じです。

```html
  <div hx-get="/example" hx-vars="myVar:computeMyVar()">Get Some HTML, Including A Dynamic Value in the Request</div>
```

## セキュリティへの配慮

* `hx-vars`の式は動的に計算されるので、実行されるJavaScriptコードを追加することができます。これは[クロスサイトスクリプティング(XSS)](https://owasp.org/www-community/attacks/xss/)の脆弱性につながる可能性があります。クエリー文字列やユーザー生成コンテンツのようなユーザー入力を扱う場合は、[hx-vals](@/attributes/hx-vals.md)を使うことを検討してください。

## メモ

* `hx-vars`は継承され、親要素に置くことができる。
* 変数の子宣言は親宣言を上書きする。
* 同じ名前の入力値は、変数宣言によって上書きされる。
