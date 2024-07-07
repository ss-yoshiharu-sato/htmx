+++
title = "hx-delete"
+++

`hx-delete`属性は、指定されたURLに対して`DELETE`を発行し、スワップ戦略を使ってHTMLをDOMにスワップします：

```html
<button hx-delete="/account" hx-target="body">
  Delete Your Account
</button>
```

この例では、`button` が `/account` に対して `DELETE` を発行し、返された HTML を `body` の `innerHTML` に入れ替えます。

## メモ

* `hx-delete` は継承されない
* [hx-target](@/attributes/hx-target.md)アトリビュートを使ってスワップのターゲットをコントロールできます。
* [hx-swap](@/attributes/hx-swap.md)属性を使って、スワップ戦略を制御することができます。
* [hx-trigger](@/attributes/hx-trigger.md)属性で、リクエストのトリガーとなるイベントを制御できます。
* リクエストと共に送信されるデータは、様々な方法でコントロールすることができます：[パラメータ](@/docs.md#parameters)
* 成功した `DELETE` に続いて要素を削除するには、`200` ステータスコードと空のボディを返します。サーバーが `204` で応答した場合は、スワップは行われません：[リクエストとレスポンス](@/docs.md#requests)
