+++
title = "hx-on"
+++

`hx-on*`属性を使うと、スクリプトをインラインに埋め込んで、要素上のイベントに直接応答することができます。HTMLにある `onClick` のような [`onevent` プロパティ](https://developer.mozilla.org/en-US/docs/Web/Events/Event_handlers#using_onevent_properties) に似ています。

`hx-on*` 属性は `onevent` を改良し、任意の JavaScript イベントを扱えるようにしたもので、[Locality of Behaviour (LoB)](/essays/locality-of-behaviour/)を強化し、非標準の DOM イベントを扱う場合にも対応します。例えば、これらの属性は[htmxイベント](/reference#events)を扱うことを可能にします。

`hx-on`属性では、コロンの後にイベント名を属性名の一部として指定します。したがって、例えば `click` イベントに応答したい場合は、`hx-on:click` 属性を使用します：

```html
<div hx-on:click="alert('Clicked!')">Click</div>
```

**Note** この構文は、標準的なDOMイベントだけでなく、すべてのhtmxイベントや他のほとんどのカスタムイベントを捕捉するために使用できます。

注意しなければならないのは、DOM属性は大文字と小文字を区別しないということです。つまり、残念ながら、`hx-on:htmx:beforeRequest`のような属性は**動作しません**。幸いなことに、htmxはキャメルケースのイベント名と[ケバブケースのイベント名](@/docs.md#events)の両方をサポートしているので、代わりに`hx-on:htmx:before-request`を使うことができます。

htmxベースのイベントハンドラを少し書きやすくするために、htmxイベントには省略記法のダブルコロン`hx-on::`を使い、"htmx "の部分を省略することができます：

```html
<!-- These two are equivalent -->
<button hx-get="/info" hx-on:htmx:before-request="alert('Making a request!')">
    Get Info!
</button>

<button hx-get="/info" hx-on::before-request="alert('Making a request!')">
    Get Info!
</button>

```

複数の異なるイベントを処理したい場合は、要素に複数の属性を追加すればよい：

```html
<button hx-get="/info"
        hx-on::before-request="alert('Making a request!')"
        hx-on::after-request="alert('Done making a request!')">
    Get Info!
</button>
```

最後に、HTMLの属性にコロン(`:`)を使うことを嫌うテンプレート言語(例えば[JSX](https://react.dev/learn/writing-markup-with-jsx))と互換性を持たせるために、長い形式でも省略形でもコロンの代わりにダッシュを使うことができます：

```html
<!-- These two are equivalent -->
<button hx-get="/info" hx-on-htmx-before-request="alert('Making a request!')">
    Get Info!
</button>

<button hx-get="/info" hx-on--before-request="alert('Making a request!')">
    Get Info!
</button>

```

### hx-on (旧式)

値はイベント名で、その後にコロン `:` が続き、その後にスクリプトが続く：

```html
<button hx-get="/info" hx-on="htmx:beforeRequest: alert('Making a request!')">
    Get Info!
</button>
```

複数のハンドラを定義するには、改行する：

```html
<button hx-get="/info" hx-on="htmx:beforeRequest: alert('Making a request!')
                              htmx:afterRequest: alert('Done making a request!')">
    Get Info!
</button>
```


### シンボル

`onevent`と同様に、イベントハンドラースクリプトでは2つのシンボルが利用できる：

* `this` - `hx-on` 属性が定義されている要素。
* `event` - ハンドラのトリガーとなったイベント

### メモ

* `hx-on` は継承されませんが、[イベントバブリング](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Building_blocks/Events#event_bubbling_and_capture) により、親要素の `hx-on` 属性は通常、子要素のイベントによってトリガーされます。
* `hx-on:*`と`hx-on`は同じ要素上で一緒に使うことはできません。`hx-on:*`が存在する場合、同じ要素上の`hx-on`属性の値は無視されます。`hx-on:*`が存在する場合、同じ要素の `hx-on` 属性の値は無視されます。
