+++
title = "hx-ext"
+++

`hx-ext` 属性は、要素とそのすべての子要素に対して htmx [extension](https://extensions.htmx.org) を有効にします。

値には、単一の拡張子名、または適用する拡張子のコンマ区切りリストを指定できる。

`hx-ext`タグは、プラグインをDOM全体に適用させたい場合は親要素に、すべてのhtmxリクエストに適用させたい場合は`body`タグに置くことができます。

## Notes

* `hx-ext`は親要素に継承されマージされるので、DOM階層のどの要素でも拡張機能を指定することができ、すべての子要素に適用されます。

* `hx-ext="ignore:extensionName"`を使うと、親ノードで定義されている拡張子を無視することができます。


```html
<div hx-ext="example">
  "Example" extension is used in this part of the tree...
  <div hx-ext="ignore:example">
    ... but it will not be used in this part.
  </div>
</div>
```

