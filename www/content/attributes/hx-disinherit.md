+++
title = "hx-disinherit"
+++

htmxのデフォルトの動作は、多くの属性を自動的に「継承」します。: つまり、[hx-target](@/attributes/hx-target.md)のような属性が親要素に置かれ、すべての子要素はそのターゲットを継承します。

`hx-disinherit`属性はこの属性の自動継承を制御することができます。例えば、ページの `body` 要素に `hx-boost` を配置し、ページの特定の部分でその動作を上書きすることで、より特殊な動作をさせることができます。

htmxは属性継承を次のように評価する：

* 親ノードに `hx-disinherit` が設定されている場合
  * `hx-disinherit="*"` この要素の属性継承はすべて無効になる。
  * `hx-disinherit="hx-select hx-get hx-target"` 指定した1つまたは複数の属性に対してのみ継承を無効にする。

```html
<div hx-boost="true" hx-select="#content" hx-target="#content" hx-disinherit="*">
  <a href="/page1">Go To Page 1</a> <!-- boosted with the attribute settings above -->
  <a href="/page2" hx-boost="unset">Go To Page 1</a> <!-- not boosted -->
  <button hx-get="/test" hx-target="this"></button> <!-- hx-select is not inherited -->
</div>
```

```html
<div hx-boost="true" hx-select="#content" hx-target="#content" hx-disinherit="hx-target">
  <!-- hx-select is automatically set to parent's value; hx-target is not inherited -->
  <button hx-get="/test"></button>
</div>
```

```html
<div hx-select="#content">
  <div hx-boost="true" hx-target="#content" hx-disinherit="hx-select">
    <!-- hx-target is automatically inherited from parent's value -->
    <!-- hx-select is not inherited, because the direct parent does
    disables inheritance, despite not specifying hx-select itself -->
    <button hx-get="/test"></button>
  </div>
</div>
```

## メモ

* [属性継承](@/docs.md#inheritance)の続きを読む
