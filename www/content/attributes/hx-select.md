+++
title = "hx-select"
+++

`hx-select` 属性は、レスポンスからスワップさせたい内容を選択することができます。この属性の値は、レスポンスから選択する要素の CSS クエリセレクタです。

以下は、応答内容のサブセットを選択する例です。：

```html
<div>
    <button hx-get="/info" hx-select="#info-details" hx-swap="outerHTML">
        Get Info!
    </button>
</div>
```

このボタンは`/info`に対して`GET`を発行し、`info-detail`というidを持つ要素を選択します。これはDOM内のボタン全体を置き換えます。

## Notes

* `hx-select` は継承され、親要素に置くことができる。
