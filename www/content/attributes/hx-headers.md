+++
title = "hx-headers"
+++

`hx-headers`属性は、AJAXリクエストと一緒に送信されるヘッダに追加することができます。  

デフォルトでは、この属性の値は[JSON（JavaScript Object Notation）](https://www.json.org/json-en.html)形式の名前式値のリストです。

もし `hx-headers` に与えられた値を*評価*させたい場合は、値の前に `javascript:` または `js:` を付けることができます。

```html
  <div hx-get="/example" hx-headers='{"myHeader": "My Value"}'>
    リクエストにカスタムヘッダーを含むHTMLを取得する
  </div>
```

## セキュリティへの配慮

* デフォルトでは、`hx-headers`の値は有効な[JSON](https://developer.mozilla.org/en-US/docs/Glossary/JSON)でなければならない。 
  動的に計算されることはありません。`javascript:`接頭辞を使用する場合、特にクエリー文字列やユーザーが生成したコンテンツのようなユーザー入力を扱う際に、[クロスサイトスクリプティング(XSS)](https://owasp.org/www-community/attacks/xss/)の脆弱性を引き起こす可能性があることを認識してください。

## メモ

* `hx-headers` は継承され、親要素に配置することができる。
* ヘッダーの子宣言は親宣言を上書きする。
