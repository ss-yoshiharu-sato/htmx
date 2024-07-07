+++
title = "hx-inherit"
+++

つまり、[hx-target](@/attributes/hx-target.md)のような属性が親要素に置かれ、すべての子要素はそのターゲットを継承します。この機能を好まず、属性の継承を明示的に指定することを好む人もいます。

この開発モードをサポートするために、htmx は `htmx.config.disableInheritance` 設定を提供します。これは `false` に設定することで、htmx 属性のデフォルトの動作が継承されないようにします。

`hx-inherit` 属性を使うと、属性の継承を手動で制御することができます。

htmxは属性継承を次のように評価する：

* 親ノードに `hx-inherit` が設定されている場合
  * `inherit="*"` この要素のすべての属性継承が有効になる。
  * `hx-inherit="hx-select hx-get hx-target"` 指定した1つまたは複数の属性に対してのみ継承を有効にする。

以下は、`htmx.config.disableInheritance`がfalseに設定されているときに、アンカータグのセットに対して`hx-target`属性を共有するdivの例です：

```html
<div hx-target="#tab-container" hx-inherit="hx-target">
  <a hx-boost="true" href="/tab1">Tab 1</a>
  <a hx-boost="true" href="/tab2">Tab 2</a>
  <a hx-boost="true" href="/tab3">Tab 3</a>
</div>
```

## メモ

* 続きを読む [Attribute Inheritance](@/docs.md#inheritance)
