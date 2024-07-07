+++
title = "hx-include"
+++

`hx-include` 属性を使うと、AJAXリクエストに追加要素の値を含めることができます。この属性の値は:

* 含める要素のCSSクエリーセレクタ。
* `this`は要素の子孫を含む。
* `closest <CSS selector>` 与えられたCSSセレクタにマッチする[最も近い](https://developer.mozilla.org/docs/Web/API/Element/closest)祖先要素またはそれ自身を見つけます(例えば、`closest tr`は要素に最も近いテーブル行をターゲットにします)。
* `find <CSS selector>` 指定された CSS セレクタにマッチする最初の子要素を探します。
* `next <CSS selector>` 与えられた CSS セレクタにマッチする最初の要素を探すために DOM を前方にスキャンします。(例: `next .error` は `error` クラスを持つ最も近い兄弟要素をターゲットにします)
* `previous <CSS selector>` 与えられた CSS セレクタにマッチする最初の要素を探すために DOM を後方にスキャンします。(例: `previous .error` は `error` クラスを持つ最も近い兄弟要素をターゲットにします)

別の入力値を含む例を示す：

```html
<div>
    <button hx-post="/register" hx-include="[name='email']">
        Register!
    </button>
    Enter email: <input name="email" type="email"/>
</div>
```

通常、これらの要素を`form`で囲み、自動的に値を送信するので、これは少し作為的ですが、概念を示しています。

非入力要素を含めると、その要素で囲まれたすべての入力要素が含まれることに注意してください。

## メモ

* `hx-include` は継承され、親要素に置くことができる。
* `hx-include` は継承されますが、リクエストのトリガーとなる要素から評価されます。`find`や`closest`のような拡張セレクタを使うと混乱しがちです。

  ```html
  <div hx-include="find input">
      <button hx-post="/register">
          Register!
      </button>
      Enter email: <input name="email" type="email"/>
  </div>
  ```
  上の例では、ボタンをクリックすると、`find input` セレクタがボタン自体から解決されますが、ボタンには `input` の子要素がないため、この場合はエラーになります。
* 標準的なCSSセレクタは[document.querySelectorAll](https://developer.mozilla.org/docs/Web/API/Document/querySelectorAll)に解決され、複数の要素を含めますが、`find`や`next`のような拡張セレクタは最大でも1つの要素しか返しません。