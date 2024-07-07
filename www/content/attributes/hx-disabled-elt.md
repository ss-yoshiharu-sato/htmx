+++
title = "hx-disabled-elt"
+++

この属性の値には、`hx-disabled-elt` 属性は、リクエストの間 `disabled` 属性が追加される要素を指定することができます。この属性の値は:

* 無効にする要素のCSSクエリーセレクタ
* `this`で要素自体を無効にする
* 最も近い`<CSSセレクタ>`は、与えられたCSSセレクタにマッチする[最も近い](https://developer.mozilla.org/docs/Web/API/Element/closest)祖先要素またはそれ自身を見つけます(例えば、`最も近いfieldset`は、要素`fieldset`に最も近いものを無効にします)。
* `find<CSSセレクタ>`は、与えられたCSSセレクタにマッチする最初の子要素を見つける。
* `next` [element.nextElementSibling](https://developer.mozilla.org/docs/Web/API/Element/nextElementSibling)に解決する。
* `next <CSS selector>` 与えられたCSSセレクタにマッチする最初の要素をDOMの前方にスキャンします（例えば、`next button`は、最も近い次の兄弟要素`button`を無効にします）。
* `previous` [element.previousElementSibling](https://developer.mozilla.org/docs/Web/API/Element/previousElementSibling)で解決する。
* `previous <CSS selector>` 与えられた CSS セレクタにマッチする最初の要素を探すために DOM を後方にスキャンします。(例: `previous input` は最も近い前の兄弟要素 `input` を無効にする)

リクエストの間、それ自身を無効にするボタンの例です：

```html
<button hx-post="/example" hx-disabled-elt="this">
    Post It!
</button>
```

リクエストが処理中であるとき、ボタンに[`disabled`属性](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/disabled)をつけ、それ以上クリックされないようにします。 

`hx-disabled-elt` 属性は、リクエスト中に複数の要素を無効にするために、カンマで区切って複数の CSS セレクタを指定することもサポートしています。ここでは、リクエスト中に特定のフォームのボタンとテキスト入力フィールドを無効にする例を示します：

```html
<form hx-post="/example" hx-disabled-elt="find input[type='text'], find button">
    <input type="text" placeholder="Type here...">
    <button type="submit">Send</button>
</form>
```

## メモ

* `hx-disabled-elt` は継承され、親要素に置くことができる。

\[hx-trigger]: https://htmx.org/attributes/hx-trigger/
