+++
title = "hx-indicator"
+++

`hx-indicator` 属性は、リクエストの間 `htmx-request` クラスが追加される要素を指定することができます。これは、リクエストの実行中にスピナーや進捗インジケータを表示するために使用できます。

この属性の値は、クラスを適用する要素または要素の CSS クエリーセレクタ、またはキーワード [`closest`](https://developer.mozilla.org/docs/Web/API/Element/closest) で、その後に CSS セレクタが続き、与えられた CSS セレクタにマッチする最も近い祖先要素またはそれ自身を探します（例えば `closest tr`）；

以下は、ボタンにスピナーを隣接させた例である：

```html
<div>
    <button hx-post="/example" hx-indicator="#spinner">
        Post It!
    </button>
    <img  id="spinner" class="htmx-indicator" src="/img/bars.svg"/>
</div>
```

リクエストが実行されると、`#spinner` 画像に `htmx-request` クラスが追加されます。この画像には `htmx-indicator` クラスも追加され、スピナーを表示する不透明度の遷移が定義される：

```css
    .htmx-indicator{
        opacity:0;
        transition: opacity 500ms ease-in;
    }
    .htmx-request .htmx-indicator{
        opacity:1
    }
    .htmx-request.htmx-indicator{
        opacity:1
    }
```

もしスピナーを表示する際に別の効果を使いたい場合は、独自のインジケータ CSS を定義して使うことができます。以下は opacity ではなく `display` を使用した例です (`htmx-indicator` ではなく `my-indicator` を使用していることに注意してください)：

```css
    .my-indicator{
        display:none;
    }
    .htmx-request .my-indicator{
        display:inline;
    }
    .htmx-request.my-indicator{
        display:inline;
    }
```

注 `hx-indicator`セレクタのターゲットは、表示したい要素そのものである必要はありません： インジケーターの親階層にあるどの要素でもかまいません。

最後に、デフォルトでは `htmx-request` クラスはリクエストの原因となる要素に追加されるので、その要素の中にインジケータを置くことができ、`hx-indicator` 属性で明示的に呼び出す必要がないことに注意してください：

```html
<button hx-post="/example">
    Post It!
   <img  class="htmx-indicator" src="/img/bars.svg"/>
</button>
```

## デモ

これは、そのような状況でスピナーがどのように見えるかをシミュレートするものだ：

<button class="btn" classes="toggle htmx-request:3s">
    Post It!
   <img  class="htmx-indicator" src="/img/bars.svg"/>
</button>

## メモ

* `hx-indicator` は継承され、親要素に置くことができる。
* 明示的なインジケータがない場合、`htmx-request`クラスはリクエストを引き起こす要素に追加される。
* 独自の CSS を使いたいが、クラス名として `htmx-indicator` を使いたい場合は、`includeIndicatorStyles` を無効にする必要がある。[htmxの設定](@/docs.md#config)を参照してください。最も簡単な方法は、HTMLの `<head>` にこれを追加することです：
 
```html
<meta name="htmx-config" content='{"includeIndicatorStyles": false}'>
```
