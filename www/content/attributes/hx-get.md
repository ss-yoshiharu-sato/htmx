+++
title = "hx-get"
+++

`hx-get`属性は、指定されたURLに `GET` を発行し、スワップストラテジーを使ってHTMLをDOMにスワップします：

```html
  <div hx-get="/example">Get Some HTML</div>
```

この例では、`div` に `/example` への `GET` を発行させ、返された HTML を `div` の `innerHTML` に入れ替えます。

### メモ

* `hx-get` は継承されない
* デフォルトでは `hx-get` はパラメータを返しません。これを変更するには、[hx-params](@/attributes/hx-params.md) 属性を使います。
* [hx-target](@/attributes/hx-target.md)属性を使ってスワップのターゲットをコントロールできます。
* [hx-swap](@/attributes/hx-swap.md)属性を使って、スワップストラテジーを制御することができます。
* [hx-trigger](@/attributes/hx-trigger.md)属性で、リクエストのトリガーとなるイベントを制御できます。
* リクエストと共に送信されるデータは、様々な方法でコントロールすることができます：[Parameters](@/docs.md#parameters)
* 空の `hx-get:""` は現在の url に get リクエストを行い、現在の HTML ページを入れ替えます。 
