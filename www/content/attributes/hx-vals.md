+++
title = "hx-vals"
+++

`hx-vals`属性は、AJAXリクエストで送信されるパラメータに追加することができます。  

デフォルトでは、この属性の値は[JSON（JavaScript Object Notation）](https://www.json.org/json-en.html)形式の名前式値のリストです。

もし `hx-vals` が与えられた値を *評価* したい場合は、値の前に `javascript:` または `js:` を付けます。

```html
  <div hx-get="/example" hx-vals='{"myVal": "My Value"}'>リクエストに値を含めてHTMLを取得する</div>
  <div hx-get="/example" hx-vals='js:{myVal: calculateValue()}'>リクエストにJavascriptから動的な値を含むHTMLを取得する</div>
```

評価されたコードを使うと、`event` オブジェクトにアクセスできる。この例では、入力の中で最後にタイプされたキーの値を含んでいる。

```html
  <div hx-get="/example" hx-trigger="keyup" hx-vals='js:{lastKey: event.key}'>
    <input type="text" />
  </div>
```

## セキュリティへの配慮

* デフォルトでは、`hx-vals`の値は有効な[JSON](https://developer.mozilla.org/en-US/docs/Glossary/JSON)でなければならない。
  動的に計算されることは**ありません**。接頭辞`javascript:`を使用する場合、特にクエリー文字列やユーザーが生成したコンテンツのようなユーザー入力を扱う際に、[クロスサイトスクリプティング(XSS)](https://owasp.org/www-community/attacks/xss/)の脆弱性を引き起こす可能性があることを認識してください。

## メモ

* `hx-vals`は継承され、親要素に置くことができる。
* 変数の子宣言は親宣言を上書きする。
* 同じ名前の入力値は、変数宣言によって上書きされる。
