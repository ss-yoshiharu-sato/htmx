+++
title = "hx-params"
+++

`hx-params`属性は、AJAXリクエストと一緒に送信されるパラメータをフィルタリングすることができます。  

この属性で取り得る値は以下の通り：

* `*` - すべてのパラメータを含む（デフォルト）
* `none` - パラメータを含まない
* `not <param-list>` - コンマで区切られたパラメータ名のリスト以外を含む
* `<param-list>` - コンマで区切られたパラメータ名のリストをすべて含める

```html
  <div hx-get="/example" hx-params="*">Get Some HTML, Including Params</div>
```

このdivは`POST`と同じようにすべてのパラメータを含みますが、通常の`GET`と同じようにURLエンコードされてURLに含まれます。

## メモ

* `hx-params` は継承され、親要素に置くことができる。
