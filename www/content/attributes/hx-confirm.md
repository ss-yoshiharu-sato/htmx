+++
title = "hx-confirm"
+++

`hx-confirm` 属性はリクエストを発行する前にアクションを確認することができます。これは、アクションが破壊的で、ユーザーが本当にそのアクションを実行したいのかを確認したい場合に便利です。

例を挙げよう：

```html
<button hx-delete="/account" hx-confirm="Are you sure you wish to delete your account?">
  Delete My Account
</button>
```

## イベント詳細

`hx-confirm` によってトリガーされるイベントは、その `detail` に追加のプロパティを含む：

* triggeringEvent: 元のリクエストのトリガーとなったイベント
* issueRequest(skipConfirmation=false): AJAXリクエストを確認するために使用できるコールバック。
* question: HTML要素の `hx-confirm` 属性の値。

## メモ

* `hx-confirm` は継承され、親要素に置くことができる。
* デフォルトでは `hx-confirm` はブラウザの `window.confirm` を使用します。[この例](@/examples/confirm.md)に示すように、カスタマイズすることができます。
* `issueRequest`コールバックに `skipConfirmation` というブール値を渡すことができる。; trueの場合（デフォルトはfalse）、`window.confirmation`は呼び出されず、AJAXリクエストが直接発行されます。
