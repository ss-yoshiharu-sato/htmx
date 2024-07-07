+++
title = "hx-patch"
+++

`hx-patch` 属性は、指定された URL に `PATCH` を発行し、スワップ戦略を使って HTML を DOM にスワップします：

```html
<button hx-patch="/account" hx-target="body">
  Patch Your Account
</button>
```

この例では、`button` が `/account` に対して `PATCH` を発行し、返された HTML を `body` の `innerHTML` に入れ替えます。
 
## メモ

* `hx-patch` は継承されない
* [hx-target](@/attributes/hx-target.md)アトリビュートを使ってスワップのターゲットをコントロールできます。
* [hx-swap](@/attributes/hx-swap.md)属性を使って、スワップ戦略を制御することができます。
* [hx-trigger](@/attributes/hx-trigger.md)属性で、リクエストのトリガーとなるイベントを制御できます。
* リクエストと共に送信されるデータは、様々な方法でコントロールすることができます：[パラメータ](@/docs.md#parameters)
