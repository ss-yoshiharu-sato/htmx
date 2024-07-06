+++
title = "hx-post"
+++

`hx-post` 属性は、指定された URL に `POST` を送信し、交換条件設定を使って HTML を DOM で書き換えます：

```html
<button hx-post="/account/enable" hx-target="body">
  Enable Your Account
</button>
```

この例では、`button` に `/account/enable` への `POST` を発行させ、返された HTML を `body` の `innerHTML` に入れ替えます。
 
## メモ

* `hx-post` は継承されない
* [hx-target](@/attributes/hx-target.md)属性を使ってスワップのターゲットをコントロールできます。
* [hx-swap](@/attributes/hx-swap.md)属性を使って、交換条件設定を制御することができます。
* [hx-trigger](@/attributes/hx-trigger.md)属性で、リクエストのトリガーとなるイベントを制御できます。
* リクエストと共に送信されるデータは、様々な方法でコントロールすることができます：[Parameters](@/docs.md#parameters)
