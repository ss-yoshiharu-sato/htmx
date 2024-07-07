+++
title = "hx-prompt"
+++

`hx-prompt` 属性を使うと、リクエストを発行する前にプロンプトを表示することができます。プロンプトの値は `HX-Prompt` ヘッダとしてリクエストに含まれます。

例を挙げよう：

```html
<button hx-delete="/account" hx-prompt="Enter your account name to confirm deletion">
  Delete My Account
</button>
```

## メモ

* `hx-prompt` は継承され、親要素に置くことができます。
