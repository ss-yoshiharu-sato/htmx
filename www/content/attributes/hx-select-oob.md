+++
title = "hx-select-oob"
+++

`hx-select-oob`属性は、帯域外スワップでスワップする内容をレスポンスから選択することができます。 
この属性の値は、カンマで区切られた、帯域を入れ替える要素のリストです。この属性は、ほとんどの場合[hx-select](@/attributes/hx-select.md)と対になっています。

以下は、応答内容のサブセットを選択する例である：

```html
<div>
   <div id="alert"></div>
    <button hx-get="/info" 
            hx-select="#info-details" 
            hx-swap="outerHTML"
            hx-select-oob="#alert">
        Get Info!
    </button>
</div>
```

このボタンは `/info` に対して `GET` を発行し、`info-details` という id を持つ要素を選択する。これはDOM内のボタン全体を置き換え、さらにレスポンス内のid `alert`を持つ要素をピックアップし、DOM内の同じidを持つdivと入れ替えます。

カンマで区切られた値のリストの各値は、セレクタとスワップ戦略を `:` で区切ることで、有効な [`hx-swap`](@/attributes/hx-swap.md) 戦略を指定することができます。

例えば、アラートの内容を置き換えるのではなく、前置きにする：

```html
<div>
   <div id="alert"></div>
    <button hx-get="/info"
            hx-select="#info-details"
            hx-swap="outerHTML"
            hx-select-oob="#alert:afterbegin">
        Get Info!
    </button>
</div>
```

## メモ

* `hx-select-oob` は継承され、親要素に置くことができます。
