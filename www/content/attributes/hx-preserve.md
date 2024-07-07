+++
title = "hx-preserve"
+++

`hx-preserve`属性は、HTMLの置換時に要素を変更しないようにします。
`hx-preserve` が設定されている要素は、htmx が祖先要素を更新したときに `id` によって保存される。
`hx-preserve` が動作するためには、要素に不変の `id` を設定する*必要があります*。
レスポンスは同じ `id` を持つ要素を必要とするが、その型と他の属性は無視される。

注 `<input type="text">`（フォーカスとキャレットの位置が失われる）、iframe、ある種の動画など、残念ながら適切に保存できない要素もあります。このようなケースに対処するには、[morphdom extension](https://github.com/bigskysoftware/htmx-extensions/blob/main/src/morphdom-swap/README.md) をお勧めします。これはより精巧な DOMreconciliation を行います。

## メモ

* `hx-preserve` は継承されない
