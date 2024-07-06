+++
title = "hx-target"
+++

`hx-target`属性は、AJAXリクエストを発行する要素とは異なる要素をスワップの対象とすることができます。この属性の値には:

* 対象とする要素のCSSクエリーセレクタ。
* `this`は `hx-target` 属性が指定された要素がターゲットであることを示します。
* 最も近い`<CSSセレクタ>`は、与えられたCSSセレクタにマッチする[最も近い](https://developer.mozilla.org/docs/Web/API/Element/closest)祖先要素またはそれ自身を見つけます(例えば、`closest tr`は要素に最も近いテーブル行をターゲットにします)。
* `find <CSS selector>`は、与えられたCSSセレクタにマッチする最初の子の子孫要素を見つける。
* `next`は、[element.nextElementSibling](https://developer.mozilla.org/docs/Web/API/Element/nextElementSibling)に解決する。
* `next <CSS selector>` は、与えられた CSS セレクタにマッチする最初の要素を探すために DOM を前方にスキャンします。(例: `next .error` は `error` クラスを持つ最も近い兄弟要素をターゲットにします)
* `previous` は、[element.previousElementSibling](https://developer.mozilla.org/docs/Web/API/Element/previousElementSibling)に解決される。
* `previous <CSS selector>` は、与えられた CSS セレクタにマッチする最初の要素を探すために DOM を後方にスキャンします。(例: `previous .error` は `error` クラスを持つ最も近い兄弟要素をターゲットにします)

divをターゲットにした例です：

```html
<div>
    <div id="response-div"></div>
    <button hx-post="/register" hx-target="#response-div" hx-swap="beforeend">
        Register!
    </button>
</div>
```

URL `/register` からのレスポンスは `response-div` という id で `div` に追加されます。

この例では、`hx-target="this"`を使って、クリックされると自動的に更新されるリンクを作っています：

```html
<a hx-post="/new-link" hx-target="this" hx-swap="outerHTML">New link</a>
```

## メモ

* `hx-target` は継承され、親要素に置くことができます。
