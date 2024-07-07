+++
title = "hx-validate"
+++

`hx-validate`属性は、リクエストを送信する前に、[HTML5 Validation API](@/docs.md#validation)によって要素自身を検証させます。

デフォルトでは `<form>` 要素だけがデータを検証しますが、他の要素は検証しません。`hx-validate="true"`を `<input>`、`<textarea>`、`<select>` に追加すると、リクエストを送信する前にデータを検証することができます。

## Notes

* `hx-validate` は継承されない
