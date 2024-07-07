+++
title = "hx-put"
+++

`hx-put`属性は、指定されたURLに `PUT` を発行し、スワップ戦略を使ってHTMLをDOMにスワップします：

```html
<button hx-put="/account" hx-target="body">
  Put Money In Your Account
</button>
```

この例では、`button` に `/account` への `PUT` を発行させ、返された HTML を `body` の `innerHTML` に入れ替えます。
 
## メモ

* `hx-put` は継承されない
* [hx-target](@/attributes/hx-target.md)アトリビュートを使ってスワップのターゲットをコントロールできます。
* [hx-swap](@/attributes/hx-swap.md)属性を使って、スワップ戦略を制御することができます。
* [hx-trigger](@/attributes/hx-trigger.md)属性で、リクエストのトリガーとなるイベントを制御できます。
* リクエストと共に送信されるデータは、様々な方法でコントロールすることができます：[パラメータ](@/docs.md#parameters)
