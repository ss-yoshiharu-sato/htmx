+++
title = "hx-history"
+++

`hx-history` 属性を `false` に設定することで、htmx がページ状態のスナップショットを取るときに、機密データが localStorage キャッシュに保存されるのを防ぐ。

履歴ナビゲーションは期待通りに機能しますが、復元時には履歴キャッシュの代わりにサーバーからURLがリクエストされます。

例を挙げよう：

```html
<html>
<body>
<div hx-history="false">
 ...
</div>
</body>
</html>
```

## メモ

* `hx-history="false"`は、現在のページの状態を履歴キャッシュから禁止するために、文書中の*どこにでも*存在させることができます(すなわち、履歴スナップショット[hx-history-elt](@/attributes/hx-history-elt.md)のために指定された要素の外側でさえも)。
